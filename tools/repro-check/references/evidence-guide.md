# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Where it lives: the repro report's own "Environment" line or section (in
a bundle, inside the candidate repro report; live, the student's draft).
Compare it against the issue's stated environment (the issue body, or the
repo-facts block's "this issue" details).

What good looks like: the OS and the relevant tool/dependency versions
are named explicitly, not implied. A difference from the issue's own
environment (different OS, newer version) is fine as long as it is
stated out loud and the report still shows the bug under its own
recorded setup — "the issue was filed on Termux; same behavior here on
Ubuntu" is a pass, silence about environment entirely is not.

## Steps

Where it lives: the repro report's steps/commands section (in a bundle,
inside the candidate repro report's "Steps" or equivalent; live, the
draft).

What good looks like: a concrete starting state (a fresh repo, a specific
file, a specific input) followed by concrete, copy-pasteable actions
(commands run, buttons pressed with their context) that land on the
observed result. "I tried it and it broke" names no starting state and
no action a stranger could repeat.

## Behavior shown

Where it lives: the repro report's command output, log excerpt, or
screenshot description (candidate repro report), read against the
issue's own description of the bug (issue body: the error text, the
panic trace, the described symptom).

What good looks like: the artifact's actual output (the literal error
message, panic line, or observed symptom) matches what the issue
describes, produced by following the issue's actual trigger (the same
input or command the issue used, not a substituted one). Watch
specifically for a different trigger than the issue's own (a typo'd
input, a different command) producing a different error that the
write-up nonetheless calls "the same class of failure" — read the
artifact's literal text, never the write-up's claim about it.

## Honesty

Where it lives: the gap between the repro report's stated conclusion
(usually its closing "Expected/Actual" or summary lines) and what its
own artifacts, two sections above, actually show.

What good looks like: the conclusion claims exactly what the artifact
demonstrates, no more. "I ran X, got Y, which is not the issue's
described behavior, so I cannot reproduce it" is a pass — an honest,
evidenced miss. A conclusion built on assumption ("it's obviously the
null-result bug"), on popularity ("everyone I know hits this"), or on
enthusiasm rather than a shown artifact is a fail, however confident its
tone.

## Comms

Where it lives: the repo's own stated contribution policy and any
AI-disclosure requirement (repo-facts block's "contribution policy"
line, or CONTRIBUTING.md/issue templates in live mode), read against the
claim comment and, once it exists, the repro comment.

What good looks like: when the repo's policy requires disclosing AI
assistance, the comment actually discloses it, specifically (not a
generic "AI was used somewhere"). When the repo states no such
requirement, silence about AI use is not a failure. Separately from
disclosure, a comment that is specific to this issue (names the actual
behavior, the actual command) reads as real; a comment built from
boilerplate that could paste onto any issue unchanged does not.
