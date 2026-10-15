# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

Where it lives: eval bundle — the "Plan context" block's scope, files,
and test-plan lines, read against the candidate PR's "Diff" and
"Commits" sections; the PR's "Description" read against that same
diff. Live — `plan.md`'s scope/files sections and any `## Deviations`
note, read against `git diff main...HEAD`; `pr_draft.md`'s description
read against that same diff.

What good looks like: every changed file and hunk traces to something
the plan named, or to a deviation note that explains the gap. Drift
runs both directions — a diff that does *more* than the plan (an
unrelated refactor, a dependency bump, formatting churn riding along)
is drift with no note to cover it; a diff that does *less* than the
plan promised, with no note saying why, is drift too. A description
that asserts fidelity ("implements the plan exactly, no changes
beyond it") while the diff contains something extra is this family's
sharpest trap: read the diff itself, never the description's claim
about it.

## Test evidence (harness category: not-tested)

Where it lives: eval bundle — the candidate PR's "Test evidence"
section, read against the "Plan context" block's test-plan line
(which often names more than one check or failure mode by name).
Live — `test_evidence.md`, read against `plan.md`'s test plan and the
student's week-2 repro steps.

What decisive looks like: every check the plan's test plan named has
verifiable evidence, in the plan's own terms (if the plan named two
failure modes, both get verified — one demonstrated and one left
silent is still an unverified claim about the other). The specific new
behavior being fixed needs a literal before/after transcript, or a
specifically-named new automated test that exercises exactly that
check with the suite run confirming it passes (a PR text that says
"see the new test's second assertion" and that test is actually there
and actually passing is decisive, not a dodge). A plain "control
unchanged" or "no regression" claim about existing behavior is
different: the full test suite (or the relevant spec) passing with no
reported failures is itself adequate evidence for it, since a
regression there would surface as a suite failure — it does not also
need its own transcript or named test. "Tests pass" with no specifics
and no suite result behind it at all is not evidence. The repo's own
stated checks — only the ones the repo-facts block actually names,
such as lint or typecheck — are run and their actual outcome pasted
in, not summarized; an honestly reported failure counts as evidence, a
hidden one does not.

## Diff quality (harness category: unreviewable)

Where it lives: eval bundle — the candidate PR's "Diff" and "Commits"
sections. Live — `git diff main...HEAD` and `git log main..HEAD`.

What a reviewable change looks like: every hunk is legible as part of
the one claimed fix, with nothing else riding along. The debris tells:
a commit message like "cleanup" or "gofmt" next to the fix commit, a
hunk touching a file the plan never named, a reformatted block with no
logic change, a bumped dependency version with no stated reason. One
such hunk is enough to fail this, however small or well-intentioned —
reviewability is about what a stranger has to read, not about whether
the extra change is itself correct.

## Standards and comms (harness category: standards-wall)

Where it lives: eval bundle — the repo-facts block's "pull requests"
line (template sections, any checklist) and "contribution policy" line
(including AI-use disclosure), read against the candidate PR's "Title"
and "Description"; the issue's "Thread highlights" for any explicit
maintainer direction. Live — the repo's actual PR template file and
`docs/CONTRIBUTING.md`, read against `pr_draft.md`; the live issue
thread.

What compliant looks like: every section the template asks for carries
real, specific content — a checklist item ticked because it is
actually true, not left unticked or checked by reflex. When the repo's
policy requires disclosing AI assistance, the description says plainly
that AI was used and how much; course contributions are AI-assisted by
default, so silence under such a policy reads as non-disclosure, not
as proof no AI was used. A maintainer's explicit direction already on
the thread (a stated preference, a named constraint) is addressed, not
quietly dropped. A repo with no template and no disclosure policy has
nothing to fail this on, and this passes by default. (Whether the
description's claims match the diff itself is plan fidelity, above,
not this family.)
