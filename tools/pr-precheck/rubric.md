# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-fidelity | The diff's changed files and hunks, read against the plan's stated scope, boundary, and files, and against any `## Deviations` note; the PR description's claims about the change, read against the diff itself | Every changed hunk falls inside the plan's stated scope, or is covered by an explicit deviation note. The description claims no more and no less than the diff actually does — a description that says "no changes beyond the plan" while the diff contains an unrelated hunk fails this, even when that hunk looks harmless | required |
| test-evidence | The PR's test-evidence section, read against every check the plan's test plan named by name, and against the repo's own stated checks (lint, typecheck, test suite) | Every check the plan's test plan named has verifiable evidence. The specific new behavior the fix targets needs either a literal before/after transcript or a specifically-named new automated test that exercises it, with the suite run confirming it passes. A plain "unchanged" or "no regression" claim about an existing/control behavior is adequately backed by the full test suite (or the relevant spec) passing with no reported failures — the untouched suite is itself the evidence nothing broke, so it needs no separate transcript or named test of its own. The repo's own stated checks (only the ones the repo-facts block actually names) are run and their outcome shown as-is, including an honestly disclosed failure. Fails only when some named check has nothing behind it at all — no transcript, no named test, and no passing-suite report | required |
| diff-quality | The unified diff and the commit list | Every hunk is part of the claimed fix. No debug leftovers, no commented-out code, no formatting-only churn, and no drive-by edit to a file or function the plan did not name, unless an explicit deviation note covers it. One unrelated hunk fails this, however small | required |
| standards-comms | The repo-facts block's PR template sections and contribution policy (including any AI-use disclosure requirement), read against the PR's actual title and description; explicit maintainer direction visible in the thread | Every section the repo's PR template asks for is filled with real, specific content, not boilerplate that could paste onto any PR. If the repo's policy requires disclosing AI assistance, the description states plainly that AI was used and the extent of it — contributions in this course are AI-assisted by default, so silence under such a policy is a fail, not evidence that none was used. Explicit maintainer guidance already on the thread is engaged with, not ignored. If the repo has no PR template and no disclosure policy, this passes by default | required |

## Verdict rule

Accept (ready to submit) only if every required check passes.
`unclear` counts as a fail on that check. There are no preferred
checks yet.
