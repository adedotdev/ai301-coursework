# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

Where it lives: eval bundle — the plan's "Cause"/"Diagnosis" heading,
read against the repro evidence block's Actual/Expected lines and any
thread comment that already names a root cause. Live — the student's
`plan.md` diagnosis section, read against their posted repro comment
(or the house repro pack) and the live issue thread.

What good looks like: the stated cause explains exactly the behavior
the repro evidence pins down, not a related-but-different one, and
it's traceable to a specific mechanism (a function, a callback, a
registration order) rather than a restatement of the symptom — "it
doesn't refresh" is the symptom, "the view isn't rebuilt after push
because X" is a cause. A diagnosis built on pure speculation
("probably," "maybe," with nothing cited) fails even if it later turns
out to be right.

## Scope

Where it lives: eval bundle — the plan's "Scope" heading or equivalent
in-scope/not-in-scope statement. Live — the same section of `plan.md`.

What good looks like: one bounded change, named concretely (a file, a
function, a specific behavior), with an explicit not-in-scope line
that rules out adjacent temptations. A plan with no scope statement,
or one that reads as "I'll poke around," fails.

## Executability

Where it lives: eval bundle — the plan's "Change"/"Approach" heading,
naming files and ordered steps. Live — `plan.md`'s approach section.

What good looks like: a stranger could start working immediately — a
named file or function, and steps in an order that makes sense without
asking the author anything. "I'll dig into the code" names no starting
point and fails.

## Test plan

Where it lives: eval bundle — the plan's "Test"/"Test plan" heading,
read against the repro evidence block's own steps and artifacts. Live
— `plan.md`'s test plan, read against the student's posted repro
comment.

What good looks like: the test plan explicitly re-runs or extends the
repro evidence's own steps and names the specific observable outcome
that would confirm the fix ("step 3 must show the pushed color without
leaving the view"). "Run the full test suite and make sure nothing
regresses" proves the change didn't break anything else; it proves
nothing about whether the actual reported bug is fixed, and fails this
check even when everything else about the plan is excellent.

## Honesty

Where it lives: eval bundle — any risks/unknowns the plan states, and
confidence language ("should," "will," "probably") compared with what
the diagnosis and test plan actually established. Live — the same, in
`plan.md` and the draft comment.

What good looks like: unknowns are named as unknowns, not dressed up
as settled fact — a plan that says "I'm not yet sure whether X," where
X is genuinely unresolved, is honest, not weak. A plan that promises
an effort estimate or a guaranteed fix before the cause is even
established is false confidence, and so is a plan that stays silent
about a risk the issue or thread already flagged (a maintainer's own
note that "the fix is hard," for instance).

## Comms

Where it lives: eval bundle — the plan comment, read against the
issue's "Thread highlights" and the repo-facts block's contribution
policy/AI-disclosure line. Live — the draft comment, the live thread,
and the repo's CONTRIBUTING docs.

What good looks like: the comment responds to what the thread or a
maintainer actually said (a review-bandwidth note, a prior root-cause
comment, a "the deep fix is hard" caveat), not generic enthusiasm that
could paste onto any issue. When the repo's policy requires disclosing
AI assistance, the comment states plainly that AI was used and the
extent of it; since this course's contributions are AI-assisted by
default, silence under such a policy is a fail, not evidence that no
AI was used.
