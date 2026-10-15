# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. Read the issue context first: title, body, labels, and thread
   highlights. Note anything a maintainer explicitly asked for or
   ruled out.
2. Read the plan context next: its stated scope, its not-in-scope
   line, the files it names, and its test plan (every check it names,
   by name). This is read before the diff on purpose — it is the
   promise the diff gets checked against, so it must not be colored by
   what the diff ends up containing.
3. In live mode, also read `plan.md`'s `## Deviations` section at this
   point if one exists; treat it as part of the plan's promise from
   here on, not as a separate afterthought.
4. Read the candidate PR's diff and commit list next, in full, before
   reading the description. Note every changed file and every hunk
   that is not a pure deletion matching something the plan named.
5. Read the PR's title and description last, holding it against the
   diff from step 4, not the other way around: the diff is ground
   truth, the description is a claim about it.
6. Read the test-evidence section, holding it against the test plan
   noted in step 2.
7. In live mode, if the student has no plan or repro of their own (a
   house-chain case), use the house plan and house repro pack in place
   of steps 2 and 6's sources.

## Evidence gathering

For each check, pull exactly this fact and record it before grading:

1. `plan-fidelity`: for every file and hunk in the diff (step 4), note
   whether it falls inside the plan's stated scope (step 2) or is
   covered by a deviation note (step 3); separately, note any claim in
   the description about what the diff does or does not include, so it
   can be checked against the diff directly rather than taken at its
   word.
2. `test-evidence`: list every check the plan's test plan named by
   name (step 2), then find each one's before/after in the
   test-evidence section (step 6); note any named check with no
   matching evidence. Separately note the outcome of the repo's own
   stated checks (lint, typecheck, test suite) as reported in the
   test-evidence section.
3. `diff-quality`: from the same pass over the diff as `plan-fidelity`,
   separately flag any hunk that reads as debris regardless of scope —
   a debug leftover, commented-out code, pure formatting churn, a
   version bump — even one already flagged there.
4. `standards-comms`: pull the repo-facts block's PR template
   sections/checklist and contribution policy/AI-disclosure line, and
   any explicit maintainer direction from the thread highlights (step
   1); read these against the title and description (step 5).

## Check execution

1. Grade `plan-fidelity` first, since `diff-quality` and
   `test-evidence` both read the same diff and plan pairing it
   establishes.
2. Grade `diff-quality` next, from the same gathered pass over the
   diff; do not re-read the diff from scratch.
3. Grade `test-evidence` next, strictly against the list of named
   checks gathered above — a check passes only when every named item
   has matching evidence, not when most of them do.
4. Grade `standards-comms` last, since it is the one check that reads
   the title and description against the repo's own asks rather than
   against the plan.
5. If the evidence a check needs is genuinely absent from the package
   (not merely thin), grade that check `unclear` and name what is
   missing. Never infer evidence that was not actually written down,
   and never let a strong grade on one check soften another's.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every required
   check passes; `unclear` counts as a fail on that check.
2. For the JSON output, quote the single piece of evidence that
   decided each check, preferring the diff's, the plan's, or the test
   evidence's exact words over a paraphrase.
3. When the verdict is `reject`, name the first-listed failing
   required check, in the rubric table's own row order
   (`plan-fidelity`, `test-evidence`, `diff-quality`,
   `standards-comms`), as the deciding one in the summary, even when
   more than one check failed.
