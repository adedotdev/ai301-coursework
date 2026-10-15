# Plan: issue #69 — output parser crashes on a top-level JSON array fallback

## Diagnosis

`_parse_json_output` in `rag/generator/output_parser.py` assumes its input is
always a dict and calls `data.items()` on it unconditionally (line 68). When
the parsed JSON is a top-level array instead of an object, `data.items()`
raises `AttributeError: 'list' object has no attribute 'items'`, because
`parse_review_output` passes whatever `json.loads()` returns straight through
without checking its type first.

Grounded in my week-2 repro evidence:

> ```
> Traceback (most recent call last):
>   File "<string>", line 5, in <module>
>     result = parse_review_output(raw)
>   File "rag/generator/output_parser.py", line 48, in parse_review_output
>     return _parse_json_output(data)
>   File "rag/generator/output_parser.py", line 68, in _parse_json_output
>     for key, value in data.items():
> AttributeError: 'list' object has no attribute 'items'
> ```

and the control run, which shows the same function works fine once the
parsed value actually is a dict:

> ```
> $ python -c "... raw = json.dumps({'skills': 'Python expert'}) ..."
> [FeedbackSection(section_name='skills', content='Python expert', confidence=0.85, suggestions=[])]
> ```

The two together isolate the cause to the type check that's missing before
the `_parse_json_output(data)` call, not to anything inside
`_parse_json_output` itself.

## Scope

**In scope:** `parse_review_output`'s dispatch logic in
`rag/generator/output_parser.py` — adding a check for whether the parsed
JSON is a dict before routing it to `_parse_json_output`, and falling back
to `_parse_plaintext_output` when it is not (the same fallback path already
used for malformed JSON).

**Not in scope:**
- Any change inside `_parse_json_output` itself. It can keep assuming a
  dict; the fix is to stop calling it with something else.
- Giving array-shaped output its own structured handling (e.g., treating
  each array item as its own section). My own repro report already named
  the minimal expectation — "likely by falling back to plain text parsing
  the way it already does for malformed JSON" — and a richer interpretation
  of array items is a separate design decision for whoever wants it.
- `_parse_plaintext_output` itself, and the regex that finds the fenced
  JSON block. Both already work correctly per the control run.

## Files

- `rag/generator/output_parser.py` — the fix itself, in `parse_review_output`.
- `tests/unit/test_output_parser.py` — remove the `@pytest.mark.xfail` marker
  on `test_json_array_fallback` once the fix makes it pass (the repo's
  `CONTRIBUTING.md` is explicit that a PR fixing a seeded bug must also drop
  the marker, since `strict=True` means an unexpectedly-passing xfail fails
  CI), and tighten its assertion so it checks the actual fallback behavior,
  not just "does not crash."

## Approach

1. In `parse_review_output`, after each `json.loads(...)` call succeeds (both
   the fenced-JSON branch and the raw-JSON branch), check
   `isinstance(data, dict)` before calling `_parse_json_output(data)`.
2. If `data` is not a dict, skip `_parse_json_output` and fall through to
   `_parse_plaintext_output(raw)`, the same path already used when JSON
   parsing fails outright.
3. Leave `_parse_json_output`'s own body untouched.
4. Remove the `xfail` marker from `test_json_array_fallback` and tighten its
   assertion to check that the result is a single `general_feedback` section
   built from the raw text, matching what the plaintext fallback already
   does for other non-dict cases.

## Test plan

Re-running my week-2 repro steps against the fix:

- The exact command that crashed before:
  `python -c "... raw = json.dumps(['First feedback item', 'Second feedback item']) ..."`
  Before: `AttributeError: 'list' object has no attribute 'items'`.
  After: returns `[FeedbackSection(section_name='general_feedback', ...)]`
  with no exception.
- The control command (object input) must produce identical output to my
  week-2 run, confirming no regression to the working path:
  `python -c "... raw = json.dumps({'skills': 'Python expert'}) ..."` still
  returns `[FeedbackSection(section_name='skills', content='Python expert', confidence=0.85, suggestions=[])]`.
- `pytest tests/unit/test_output_parser.py -v -m unit`. Before: `18 passed,
  1 xfailed`. After, with the marker removed: `19 passed`, with
  `test_json_array_fallback` now a normal passing test instead of an
  expected failure.

## Risks and unknowns

- The only other caller of `parse_review_output` is
  `rag/generator/review_generator.py`, which does `if sections: return
  sections[0]`. I checked this directly: it already handles an empty list,
  and the fix only changes a crash into a non-empty list, so this caller
  needs no change. I have not run the full integration suite against it,
  since that needs the Docker/DB stack this bug itself doesn't require.
- I have not decided exactly what `section_name` and `content` the
  plaintext fallback should carry for an array input beyond what
  `_parse_plaintext_output` already does by default (the whole raw string
  as `content`, `general_feedback` as the name). If a reviewer wants
  array items surfaced more specifically, that is a scope question I'd
  rather raise in review than guess at here.

## Deviations

None. The build matched the plan: an `isinstance(data, dict)` check before
each `_parse_json_output(data)` call, falling through to the existing
`_parse_plaintext_output` path otherwise, plus dropping the `xfail` marker
on `test_json_array_fallback` and tightening its assertion. No other file
needed touching, and the one other caller of `parse_review_output`
(`rag/generator/review_generator.py`) needed no change, as anticipated in
Risks and unknowns.
