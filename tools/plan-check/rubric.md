# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | The plan's stated cause, read against the repro evidence's actual/expected lines and any thread comment that already names a root cause | The stated cause explains exactly the behavior the repro evidence pins down, traceable to a specific mechanism (a function, a callback, a registration order), not a restatement of the symptom. Fails when the diagnosis contradicts or ignores the repro evidence, or rests on unverified speculation ("probably", "maybe", "must be") with nothing cited | required |
| scope-bounded | The plan's in-scope/not-in-scope statement and the files or areas it names | One bounded change, named concretely, with an explicit not-in-scope line ruling out adjacent temptations. Fails when scope is unstated, open-ended ("I'll poke around"), or wider than the diagnosis requires | required |
| executable | The plan's named files/functions/areas and its ordered approach steps | A stranger could start working immediately: a named file or function plus steps in a sensible order, with nothing left for the author to clarify. Fails on vague intent ("dig into the code") with no concrete starting point | required |
| test-plan-decisive | The plan's test plan, read against the repro evidence's own steps and artifacts | The test plan explicitly re-runs or extends the repro evidence's own steps and names the specific observable outcome that would confirm the fix. A generic check ("run the full test suite", "make sure nothing regresses") that never ties back to the actual reported behavior fails this, even when the rest of the plan is excellent | required |
| honest-uncertainty | The plan's stated risks/unknowns and its confidence language ("should", "will", "probably"), read against what diagnosis-grounded and test-plan-decisive actually established | Unknowns are named as unknowns, not dressed up as settled fact. Fails when the plan asserts an effort estimate or a guaranteed fix before the cause is established, or stays silent about a risk the issue or thread already flagged (e.g. a maintainer's own "the fix is hard") | required |
| comms-conventions | The plan comment, read against the issue's thread highlights and the repo-facts block's contribution policy / AI-disclosure requirement | The comment responds to what the thread or a maintainer actually said, not generic enthusiasm that could paste onto any issue. If the repo's policy requires disclosing AI assistance, the comment states plainly that AI was used and the extent of it — contributions in this course are AI-assisted by default, so silence under such a policy is a fail, not evidence that no AI was used. If no such policy exists, this passes regardless | required |

## Verdict rule

Accept (ready to post and build from) only if every required check
passes. `unclear` counts as a fail on that check. There are no
preferred checks yet.
