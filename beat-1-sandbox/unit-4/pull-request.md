# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/242

**Branch**

fix/69-output-parser-array-fallback

## Eval iterations

**Run history**

Three full 20-package runs, in order:

1. `agreement: 13/20 scored items (bar: 18/20: below the bar; category floor unmet: no match in clear-accept)`
2. `agreement: 20/20 scored items (bar: 18/20: PASS)`
3. `agreement: 20/20 scored items (bar: 18/20: PASS)`

(Run 1 failed `test-evidence` on all 7 `clear-accept` packages at once — a
systematic wording bug, not noise. Run 2 fixed it and already hit 20/20;
run 3 re-confirmed the same rubric wording with a fresh grading pass before
I called it final.)

**Package analysis**

`pkg-19` (a yq single-quoted-scalar emitter bug). Gold label: `accept`. My
rubric's decision: `reject` on the first full run, `accept` from the second
run onward, with `test-evidence` as the deciding check both times. The
plan's test plan named three things: re-run the repro for a byte-identical
round-trip, two controls stay unchanged, and `go test ./...`. The PR's
evidence gives a full before/after transcript for the repro (including a
`diff <(...) source.yml && echo IDENTICAL` check) and the full `go test
./...` result, but only asserts the two controls are unchanged in one
closing line, with no separate transcript or named test for either one. My
first rubric wording demanded a transcript or a named test for every item
the plan named, with no exception, so it failed this PR for the two
uncovered controls. Gold reads it as sufficient: a full, passing test suite
is itself evidence that nothing broke in paths the change didn't touch,
even without a test specifically labeled for each one.

**Check rationale**

```
test-evidence | The PR's test-evidence section, read against every check the plan's test plan named by name, and against the repo's own stated checks (lint, typecheck, test suite) | Every check the plan's test plan named has verifiable evidence. The specific new behavior the fix targets needs either a literal before/after transcript or a specifically-named new automated test that exercises it, with the suite run confirming it passes. A plain "unchanged" or "no regression" claim about an existing/control behavior is adequately backed by the full test suite (or the relevant spec) passing with no reported failures — the untouched suite is itself the evidence nothing broke, so it needs no separate transcript or named test of its own. The repo's own stated checks (only the ones the repo-facts block actually names) are run and their outcome shown as-is, including an honestly disclosed failure. Fails only when some named check has nothing behind it at all — no transcript, no named test, and no passing-suite report | required
```

This check went through two rewrites before landing here. The first
version demanded a literal transcript or a named test for every item the
plan's test plan named, with no distinction between kinds of claim. That
version failed every `clear-accept` package in my eval set at once (7/7),
because real, good PRs routinely assert a control is "unchanged" and back
it with nothing but a passing full suite, never a transcript dedicated to
that one claim (`pkg-02`, `pkg-19`, and others all do this). I rewrote the
check to split "the new behavior being fixed," which still needs direct
evidence, from "an existing control stays unchanged," which a passing
suite backs on its own, since a regression there would show up as a suite
failure.

**Trade-offs**

Letting a passing suite stand in for a control's own evidence means this
check can't catch a control that broke in a way nothing in the existing
suite happens to exercise. A PR could claim "the other code path is
unaffected," the suite could pass, and the claim could still be false if
no existing test actually touches that path. I accepted this rather than
revert to demanding a dedicated transcript or named test for every control
a plan mentions, because the stricter version is the one that just failed
7 legitimate PRs in my own eval set for exactly this pattern: real,
accepted PRs lean on the existing suite for control claims far more often
than they add a dedicated test for each one. The canary that confirmed the
looser wording didn't overcorrect was `pkg-01`, a `standards-wall` reject
I re-ran with `--only` after the rewrite — it still correctly failed, so
the loosened check didn't accidentally let a bad PR through elsewhere.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
