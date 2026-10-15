# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the issue context first: title, body, labels, and thread
   highlights. Note what the reporter originally described and what
   any maintainer said about it.
2. Read the repro evidence block next. Note the exact environment, the
   steps, and the actual-versus-expected outcome it establishes. This
   is read before the plan on purpose: it is the ground truth every
   later check compares the plan against, so it must not be colored by
   the plan's own framing of the bug.
3. In live mode, if the student has no posted repro comment of their
   own (a house-issue case), use the house repro pack as quoted in the
   drafts in place of step 2. If the drafts quote no repro evidence at
   all, record that absence now; it is what several checks below will
   grade.
4. Read the candidate plan in full, in its own section order
   (diagnosis, scope, approach, test plan, risks/unknowns), before
   grading anything.
5. Read the candidate plan comment last, holding it against both the
   thread from step 1 and the plan from step 4.

## Evidence gathering

For each check, pull exactly this fact and record it before grading:

1. `diagnosis-grounded`: the plan's stated cause, plus the repro
   evidence's actual/expected lines, plus any thread comment that
   already names a root cause.
2. `scope-bounded`: the plan's in-scope and not-in-scope statements,
   and any files or areas it names.
3. `executable`: the plan's named files/functions/areas and its
   ordered approach steps.
4. `test-plan-decisive`: the plan's test-plan section, placed directly
   next to the repro evidence's own steps and artifacts so they can be
   compared line by line.
5. `honest-uncertainty`: any risks/unknowns the plan states, and any
   confidence language ("should", "will", "probably") it uses.
6. `comms-conventions`: the plan comment's text, the thread highlights
   from step 1, and the repo-facts block's contribution policy / AI-
   disclosure line.

## Check execution

1. Grade `diagnosis-grounded` first. A failing diagnosis makes every
   downstream check's evidence suspect, but still grade every other
   check independently and report its own evidence; do not short-
   circuit the rest of the table.
2. Grade `scope-bounded`, `executable`, and `test-plan-decisive` next,
   in that order, each strictly against the evidence gathered for it
   above — not against evidence gathered for a different check.
3. Grade `honest-uncertainty` by comparing the plan's stated confidence
   to what `diagnosis-grounded` and `test-plan-decisive` already
   established. Do not re-read the whole package again for this; the
   earlier grades carry the needed facts forward.
4. Grade `comms-conventions` last, since it is the one check that reads
   the plan comment rather than the plan itself.
5. If the evidence a check needs is genuinely absent from the package
   (not merely thin), grade that check `unclear` and name what is
   missing. Never infer evidence that was not actually written down.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every required
   check passes; `unclear` counts as a fail on that check.
2. For the JSON output, quote the single piece of evidence that
   decided each check, preferring the plan's or repro evidence's exact
   words over a paraphrase.
3. When the verdict is `reject`, name the first-listed failing
   required check (in the table's own row order) as the deciding one
   in the summary, even when more than one check failed.
