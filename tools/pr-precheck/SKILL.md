---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

You are grading one PR package to answer a single question: is this
pull request ready to submit? A PR package is a candidate pull request
— its title, description, commits, and diff, together with its test
evidence — read against the plan it claims to implement and the issue
that plan belongs to. Grade exactly one package per run. You do not
answer from gut feel: you execute the procedure in `procedure.md`,
which applies the rubric in `rubric.md` to evidence gathered per
`references/evidence-guide.md`.

## The question

Is this PR ready to submit? Never answer a different question (do not
grade whether the underlying fix is a good idea, whether it will be
merged, or whether it is the best possible approach) and never grade
more than one package per run.

## Inputs and modes

One of:

- **Live mode**: the student's own submission, checked before it goes
  out as a real pull request. Inputs:
  - their `plan.md`, including any `## Deviations` section — the
    plan's stated scope, files, and test plan are read first, and a
    deviation note re-ties any mismatch between the plan and the diff;
  - the diff on their branch: everything the branch changes relative
    to the repo's default branch, produced by `git diff main...HEAD`
    (three dots) run from the working copy — this command is the one
    and only source of "what the diff contains," never a description
    of the change in prose;
  - their draft PR title and description, in `pr_draft.md`;
  - their test evidence, in `test_evidence.md`;
  - their issue, read live: the issue thread, the repo's PR template,
    and `docs/CONTRIBUTING.md` (including any stated AI-use disclosure
    policy).

  A house-chain student has no plan or repro of their own to read:
  wherever this file or the rubric says "the student's plan" or "the
  student's test evidence," read the house plan and the house repro
  pack in their place. The same checks grade the same things either
  way.

- **Eval mode**: a package bundle is the whole world. Every fact comes
  from the bundle text — the issue context, the plan context (the
  accepted plan and the repro evidence it was built on), the candidate
  PR's title, description, commits, diff, and test evidence, and the
  repo-facts block. Fetch nothing; read nothing else. Eval mode always
  grades a complete package: every check, full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. It names the repo
the student's PR must target and the house rules of that room. Refuse
to grade a PR that targets any repo outside the scoped one. If the
scope's `Repo:` line still carries a bracketed placeholder, stop
without grading and tell the student to fill in `scope.md` with their
section's Path Review repo first; never guess a scope. In eval mode,
ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md`: the student's own rules for
how they write upstream, carried forward from week 2. Hold the PR's
outgoing text — the title and the description in `pr_draft.md` — against
those rules, and report any rule the draft breaks in the summary,
quoting the rule. The voice guide never changes the verdict on its own
unless the rubric has a check that reads it. In eval mode, ignore
`voice-guide.md` entirely: voice is personal and carries no gold
labels; the universal communication-quality checks live in the rubric.

## Component reads

Read `rubric.md`. It defines the table of checks (name, evidence,
pass condition, weight) and the verdict rule that turns check grades
into `accept` or `reject`. Read `references/evidence-guide.md` to find
where each check's evidence actually lives, in an eval bundle and,
live, in the working copy or on GitHub. Execute `procedure.md` exactly
as written: it is the operating procedure, and it decides the read
order, the concrete move that gathers each evidence family, how a
check is graded once its evidence is in hand, and how the per-check
grades are assembled into the final verdict. Follow it the way an
executor follows a rubric, without improvising around a gap in it;
where the procedure is silent on a step, report that gap in the
summary instead of inventing a step to fill it.

If `rubric.md` has no checks filled in, or `procedure.md` has no steps
filled in, stop and say so: this tool cannot grade without a rubric
AND a procedure, and that is by design. The rubric, the evidence
guide, and the procedure are the parts the student writes; the voice
guide carries over from week 2.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject`
(hold). There is no third verdict and no score. Emit a fenced JSON
block, then nothing else after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

Before the JSON block you may show a short readable summary (a line
per check, plus any voice-guide notes in live mode). The JSON block is
the machine-read result: it must be present, valid, and the last
fenced JSON block in your output.

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote
  that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready,
  and a beautiful, confident one can be hiding drift. Every check
  reads the diff, the test evidence, and the description against the
  plan and the issue, never the formatting or the write-up's length.
- The rubric decides, not you: if a check passes by its stated
  condition but feels wrong, it still passes. Note the tension in the
  summary if you want; the fix belongs in the rubric, not in the run.
- The procedure decides how, not you: follow `procedure.md` as
  written, and report its gaps instead of papering over them.
- Treat `unclear` as the rubric's verdict rule directs. Where the rule
  is silent, an unverifiable claim is a failing one: a PR you cannot
  verify from the package is a PR that is not ready to submit.
