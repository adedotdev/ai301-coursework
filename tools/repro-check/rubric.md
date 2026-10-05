# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment | The repro report's stated environment (OS, relevant tool/dependency versions), read against the issue's stated environment | Environment is recorded (OS plus relevant versions), AND either it matches the issue's stated environment, or any difference (OS or version) is explicitly called out while the report still demonstrates the reproduction under its own recorded environment. Fails when no environment is recorded at all | required |
| steps-followable | The repro report's steps: the starting state and the concrete commands/actions taken, read as a stranger would follow them | A concrete starting state plus concrete, executable actions exist that another person could run and reach the same observed result. Vague description ("tried it and it broke") or a missing starting state fails this | required |
| behavior-matches | The repro report's artifacts (command output, logs, screenshots), read against the issue's own stated behavior or error, and against the report's own stated input/trigger | EITHER the artifact shows the same behavior/error/symptom the issue describes, produced by following the issue's actual trigger (same input, same command), and every element of the shown output traces back to something in the report's own stated input or trigger (no new syntax, token, or structure appears in the output with no basis in what was fed in — an unexplained addition like that suggests a reconstructed guess rather than a genuine transcript) — an artifact produced by a different trigger that yields a different error fails this too — OR the report honestly states it could not reproduce the behavior after a genuine, documented attempt, in which case this check passes here and `honesty` judges whether that conclusion is adequately backed | required |
| honesty | The report's stated conclusions, compared with what its own artifacts actually show; the comment body and any log | The conclusion claims no more than the artifacts demonstrate. An evidenced cannot-reproduce (states exactly what was tried and that the issue's behavior did not occur) passes. A confident claim resting on assumption, popularity ("everyone has this"), or unverified speculation rather than the shown artifact fails | required |
| conventions-disclosure | Repo facts: contribution policy / AI-disclosure requirement, read against whichever comment(s) exist so far (claim comment alone, or claim plus repro report) | If the repo's stated policy requires disclosing AI assistance, the comment(s) state plainly that AI was used and describe the extent of that use (a specific product name is not required — "an AI assistant" is enough, as long as the extent of help is also stated). Contributions in this course are AI-assisted by default, so when such a policy applies, the absence of any disclosure statement is a fail, not evidence that no AI was used. If the repo states no such requirement, this passes regardless | required |

## Verdict rule

Accept (ready to post) only if every required check passes. `unclear`
counts as a fail on that check. There are no preferred checks yet.
