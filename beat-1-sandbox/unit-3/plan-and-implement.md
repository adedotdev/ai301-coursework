# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

adedotdev

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69#issuecomment-6179406969

I reproduced this with the exact traceback (report above). parse_review_output passes a parsed JSON array straight to _parse_json_output. That function only handles a dict. My plan is to check the type before that call. When the parsed value is not a dict, it falls back to the existing plaintext path, the same one malformed JSON already uses. I will also remove the xfail marker on test_json_array_fallback.

---

## Your branch

**Branch**

fix/69-output-parser-array-fallback

**Evidence**

Before (Unit 2, the crash):

```
$ python -c "
import json
from rag.generator.output_parser import parse_review_output
raw = json.dumps(['First feedback item', 'Second feedback item'])
result = parse_review_output(raw)
"
Traceback (most recent call last):
  File "<string>", line 5, in <module>
    result = parse_review_output(raw)
  File "rag/generator/output_parser.py", line 48, in parse_review_output
    return _parse_json_output(data)
  File "rag/generator/output_parser.py", line 68, in _parse_json_output
    for key, value in data.items():
AttributeError: 'list' object has no attribute 'items'
```

After (same command, against the built fix):

```
$ python -c "
import json
from rag.generator.output_parser import parse_review_output
raw = json.dumps(['First feedback item', 'Second feedback item'])
result = parse_review_output(raw)
print(result)
"
2026-10-14 14:59:41 [warning  ] raw_json_not_an_object         json_type=list
2026-10-14 14:59:41 [info     ] plaintext_output_parsed        content_length=47
[FeedbackSection(section_name='general_feedback', content='["First feedback item", "Second feedback item"]', confidence=0.7, suggestions=[])]
```

Control (object input, unchanged before and after):

```
$ python -c "
import json
from rag.generator.output_parser import parse_review_output
raw = json.dumps({'skills': 'Python expert'})
result = parse_review_output(raw)
print(result)
"
[FeedbackSection(section_name='skills', content='Python expert', confidence=0.85, suggestions=[])]
```

Test suite, before and after:

```
$ pytest tests/unit/test_output_parser.py -v -m unit
# before: 18 passed, 1 xfailed
# after:  19 passed
```

## Eval iterations

**Run history**

Two full 20-package runs, in order:

1. `agreement: 20/20 scored items (bar: 18/20: PASS)`
2. `agreement: 19/20 scored items (bar: 18/20: PASS)`

(Run 2 is the confirming run I saved. `pkg-14`, a `clear-accept` package,
flipped to a false reject between the two identical-rubric runs — the
same cross-run model variance I'd already seen in units 1 and 2 on
borderline items, not a rubric change. See Package analysis.)

**Package analysis**

`pkg-14` (a zellij OSC-color-leak-on-reattach issue). Gold label:
`accept`. My rubric's decision: `accept` on the first full run, `reject`
on the confirming run (failing `diagnosis-grounded`, `executable`, and
`honest-uncertainty` simultaneously), with identical rubric, evidence
guide, and procedure text both times. The plan itself is genuinely
strong: it traces the leak to OSC query responses racing pane-input
wiring on reattach, grounds that in the regression window (clean on
0.44.1, leaking from 0.44.2) and the cache-clear control from the
thread, bounds scope to the Unix reattach path, and explicitly defers
a Windows variant it can't test, with a reason. I read the one failing
run as the grader reading the plan's deliberate scoping of the Windows
and other-terminal thread reports as "ignoring" them, rather than as an
honest, reasoned scope decision — a stricter misreading of a genuinely
correct call, not a rubric gap exposed by the package itself.

**Check rationale**

```
test-plan-decisive | The plan's test plan, read against the repro evidence's own steps and artifacts | The test plan explicitly re-runs or extends the repro evidence's own steps and names the specific observable outcome that would confirm the fix. A generic check ("run the full test suite", "make sure nothing regresses") that never ties back to the actual reported behavior fails this, even when the rest of the plan is excellent | required
```

I wrote this check directly from a calibration package (`calib-04`, a
ripgrep glob-normalization plan) that was otherwise excellent —
well-grounded diagnosis citing two maintainer comments, carefully
bounded scope, concrete approach — but whose test plan was just "run
the full test suite (`cargo test --workspace`) and make sure nothing
regresses." That proves the change didn't break anything else; it
proves nothing about whether the specific reported bug (an absolute-path
glob behaving differently by cwd) is actually fixed, since the plan
never proposed a test for that behavior at all. I wrote the pass
condition to require the test plan to name the repro evidence's own
steps and a specific observable outcome, specifically so a
plausible-sounding but non-decisive test plan like that one can't pass
on the strength of everything else around it.

**Trade-offs**

This check only verifies that a test plan *names* a decisive,
repro-tied outcome in the text; it can't verify from the bundle alone
that the named outcome would actually be observable the way the plan
claims, or that the plan's diagnosis is correct in the first place. A
confidently wrong diagnosis paired with a test plan that decisively
checks for the (wrong) predicted outcome would still pass this check —
that gap belongs to `diagnosis-grounded` instead, and the two checks
are deliberately kept separate rather than merged into one "is this
plan good" check, so each failure mode has its own named evidence in
the output. Nothing in my eval set exercised this exact gap (no package
paired a wrong diagnosis with an internally consistent, decisive-looking
test plan), so I'm accepting it as a known blind spot rather than one a
canary confirmed.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
