# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69

**Verdict output**

````
## Summary

**Repo-level facts** (apply to all three): not archived, last push Sep 16, 2026 (human-authored commits by Aburke225, within 30 days) — maintainer-alive and repo-in-use both pass across the board. `docs/CONTRIBUTING.md` says nothing about AI-assisted contributions — silence passes ai-policy-ok for all three.

**Accepted, ranked by fit:**

1. **#69 — Output parser crashes on a top-level JSON array fallback** (`rag/generator/output_parser.py`). Single bounded bug (`.items()` called on a list), no assignee, no comments, no linked PR. This is the best fit for you: it's directly in the RAG generation path, and you'll have to read the existing fallback logic to fix it correctly rather than just tweaking a number.
2. **#64 — Relevance scorer "partial overlap" test fixture has full overlap** (`tests/unit/test_relevance_scorer.py`). Single bounded fixture fix, no assignee, no comments, no linked PR. Still RAG-adjacent (retrieval scoring), but it's a test-only correction — less codebase depth than #69.

**Rejected:**

- **#68 — Keyword search raises `ZeroDivisionError` on empty index.** Otherwise clean (bounded scope, no assignee), but **nobody-on-it fails**: PR #74, opened today (Sep 24, 2026) by a different student, already implements this exact fix (empty-corpus guard, explicit empty-index state, un-skipped regression test) and is open. That's an active implementing PR, not a bare claim comment, so the Path Review house rule (which only exempts claim comments) doesn't rescue it.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Last commit Sep 16, 2026 authored by human account Aburke225, 8 days before capture date Sep 24, 2026"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "Not archived; last push Sep 16, 2026, within 180 days of Sep 24, 2026"},
      {"name": "scope-fits", "grade": "pass", "evidence": "Single bug in output_parser.py (`.items()` on a list) plus removing one xfail marker; one file, one deliverable"},
      {"name": "nobody-on-it", "grade": "pass", "evidence": "No assignees, no comments, no linked PRs"},
      {"name": "ai-policy-ok", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI-contribution policy; silence passes"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/64",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Last commit Sep 16, 2026 authored by human account Aburke225, 8 days before capture date Sep 24, 2026"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "Not archived; last push Sep 16, 2026, within 180 days of Sep 24, 2026"},
      {"name": "scope-fits", "grade": "pass", "evidence": "Single flawed test fixture in test_relevance_scorer.py; one file, one deliverable, reproduction command given"},
      {"name": "nobody-on-it", "grade": "pass", "evidence": "No assignees, no comments, no linked PRs"},
      {"name": "ai-policy-ok", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI-contribution policy; silence passes"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Last commit Sep 16, 2026 authored by human account Aburke225, 8 days before capture date Sep 24, 2026"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "Not archived; last push Sep 16, 2026, within 180 days of Sep 24, 2026"},
      {"name": "scope-fits", "grade": "pass", "evidence": "Single bug in KeywordSearcher.index() (ZeroDivisionError on empty corpus); one file, one deliverable"},
      {"name": "nobody-on-it", "grade": "fail", "evidence": "PR #74, opened Sep 24, 2026 by Momik-jpg, is open and already implements the fix (empty-corpus guard, empty-index state, un-skipped regression test) — an active implementing PR, not a bare claim comment"},
      {"name": "ai-policy-ok", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI-contribution policy; silence passes"}
    ],
    "verdict": "reject"
  }
]
```
````

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

Four full 20-issue runs, in order:

1. `agreement: 16/20 scored items (bar: 18/20: below the bar)`
2. `agreement: 19/20 scored items (bar: 18/20: PASS)`
3. `agreement: 19/20 scored items (bar: 18/20: PASS)`
4. `agreement: 20/20 scored items (bar: 18/20: PASS)`

(Between full runs I re-graded only the disagreeing issues with `--only`, plus 1-2
already-passing issues as regression canaries, before spending on the next full run.
Runs 2 and 3 have the same score but are not the same run: run 2 disagreed on
issue-20, run 3 fixed that but broke issue-09, which run 4 then fixed. The score
alone would have hidden that.)

**Issue analysis**

`issue-20` (a real GitHub issue titled "Add company logo shape to the toolbar",
opened by `cursor[bot]`). Gold label: `reject`. My rubric's decision: `reject`
(on the confirmed run — it briefly false-accepted this on an earlier rubric
wording). The issue was filed by an AI agent account, not a human, has zero
comments, and its own text leaves the actual deliverable undecided: "Logo
asset TBD", and "possibly app wiring... if needed" about which part of the
codebase would even change. Nobody — human, maintainer, or otherwise — has
confirmed this is wanted or settled how to build it. My `scope-fits` check
originally only handled "is this one bounded task," which this issue actually
passes (it names one feature). What it misses is a different failure: an idea
that is still being worked out by its own author, with no external
confirmation it is real or feasible.

**Check rationale**

```
scope-fits | Issue body, comment thread, and repo facts on linked PRs | Issue names one problem or one feature a single contributor could complete end to end. Multiple files, multiple contributing causes, several closely-related sub-parts of the same feature, or the reporter's own list of possible approaches do NOT by themselves fail this — that is still one deliverable with one owner. A terse body is not a scope failure either, especially from a maintainer/collaborator or under a "good first issue" label. Fails when: the issue explicitly asks for its sub-items to be split across separate contributors/PRs (a real tracking/umbrella issue); the design is still being actively argued with no maintainer sign-off; a maintainer says it touches core internals; the issue's age and history show multiple abandoned attempts (closed/unmerged linked PRs, or a thread showing repeated claim-then-unassign cycles) pointing to real difficulty beyond what the text suggests; or the request's own text leaves the actual deliverable undecided — what asset, output, or even which part of the codebase would change ("TBD", "not identified yet", "possibly X, if needed") — with no maintainer having weighed in to settle it. This is different from a clear problem with multiple candidate implementation approaches (normal for any bug; a contributor picks one and that does not fail this check) | required
```

This check took its current form because my first draft only asked "is this
one bounded task," and that single question can't tell apart five different
ways an issue fails to be a real first contribution: an umbrella meant to be
split across people, an unsettled design debate, something touching core
internals, an issue with a graveyard of abandoned attempts, and an idea its
own author hasn't finished deciding. Each clause exists because a specific
eval issue slipped through the version before it (issue-04 and issue-19 for
the "multi-file doesn't mean umbrella" clause, issue-15 for the
abandoned-attempts clause, issue-20 for the undecided-deliverable clause).

**Trade-offs**

The undecided-deliverable clause I added for issue-20 is deliberately narrow:
it only fires when the *deliverable itself* is unsettled ("TBD", "if
needed"), not when there are multiple candidate *implementation approaches*
to an already-clear problem. My first version of that clause was broader and
it broke `issue-19` (a UI-freeze bug where the reporter lists several
possible fixes) — the rubric read "here are some options" as "this isn't
decided yet" and rejected a genuinely good issue. Narrowing the clause to
target the deliverable specifically, not the approach, fixed issue-19 back
to `accept` while still catching issue-20. What this gives up: a rubric this
narrow would probably still accept a bare feature request that fully commits
to specifics without a maintainer ever blessing it (fully-specified but
never actually wanted) — `scope-fits` alone can't see whether anyone besides
the reporter wants the feature; that's a gap `nobody-on-it` and
`maintainer-alive` don't cover either, since neither checks for demand, only
for activity and claims.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. **Fit to interests/time.** #69 sits in the RAG generation path
   (`rag/generator/output_parser.py`), which is exactly the area I want to
   work in, and it's a single self-contained bug — a reasonable scope for a
   first unit's time budget.
2. **What the verdict caught vs. what I weighed.** The rubric confirmed it's
   unclaimed, the repo team is active, and there's no AI-contribution ban —
   things I'd have had to check by hand otherwise. What the rubric couldn't
   weigh: that this is the specific corner of the codebase (RAG output
   handling) I actually want more reps in, versus #64, which was equally
   "accepted" but is a test-only fix with less to learn from.
3. **Anticipated difficulty claiming it.** Moderate — I'll need to actually
   read the existing fallback-parsing logic in `output_parser.py` to
   understand why `.items()` gets called on a list before I can fix it
   correctly, not just patch a symptom.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
