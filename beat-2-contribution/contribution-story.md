# Contribution: A poisoned document masks the retrieval-exposure leak, so two LLM08 dimensions never co-fire

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Dami Adenuga
**GitHub Username:** adedotdev
**Issue:** https://github.com/wehnsdaefflae/llmsectest/issues/38
**Pull Request:** https://github.com/wehnsdaefflae/llmsectest/pull/41

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built the scout, and it caught a blocker my own reading missed**

I turned the unit-1 rubric into issue-scout: two `gh search issues` queries traced to my fit profile (RAG/retrieval/agentic in Python, Spring Boot in Java), ranking filters that drop assigned or stale results and order survivors by comment count, and a rubric that grades the top 5. Two things fell short on the first run: the scout's own subprocess couldn't call `gh` at all (every call got denied for approval), so I ran the searches myself and fed it the results; and the comment-count ranking had no tie-break, so most of the top 5 was arbitrary since nearly everything sat at 0 comments. I fixed the tie-break (most recent first) and found a real rubric gap while grading: a genuinely well-specified issue (`railtracks#1757`) still shouldn't have been accepted, because its own text said to wait for a prerequisite PR that's still open, and none of my five checks caught that. I added a clause for it. The same rubric then correctly rejected both of my own hand-picked issues from the Issue Selection site, each for a currently active competing PR my own read of the issue page would have missed.

**Unit 6: Installed a voice guard that caught a real rule gap, then hit a tool wall writing the fix**

I installed the voice-guard hook (a `PreToolUse` check that holds every outgoing `gh issue/pr
comment/create` body against my own voice-guide before it posts) and patched the scout's
rubric so an open design edge is a difficulty note, not a hard reject. Using the guard for
real surfaced a gap: my first claim-comment draft tripped the "one question, with what I
already tried" rule, because it asked a pre-work design question with nothing "tried" yet.
The content was fine; the rule was too narrow. Fixing it meant editing my own voice-guide.md,
which Claude Code's self-modification safety check blocks outright, tool-agnostic — I hit the
identical denial through three different tools. I made the edit myself by hand instead, widened
the rule to "grounded in what I already know" (issue text counts, not just things tried), and
the redraft passed. A second, unrelated wall showed up posting the claim itself: running `gh`
through a permission-bypassed subprocess tripped a different safety block
(`[Create Unsafe Agents]`), so I posted the verified comment from my own interactive session
instead of automating around it.

**Unit 7: Installed the ship-gate, then learned a manifest's exceptions table doesn't excuse a failing exit code**

I installed the ship-gate (a second `PreToolUse` hook that runs the target repo's own manifest checks, then my `pr-precheck` rubric, before `gh pr create` goes through) and wrote `ship-manifest.md` for `llmsectest` from its own CONTRIBUTING.md. The first real run blocked on the "Tests + coverage" check: 4 tests failed, all pre-existing Windows path and permission-bit mismatches, unrelated to my fix. I'd listed them in the manifest's "Excluded" table, but that table only documents a known failure for `pr-precheck` to read; it doesn't make the command itself exit 0. I fixed it by adding `--deselect` flags for those 4 tests directly into the manifest's own test command, confirmed `1053 passed, 4 deselected` locally, and the gate passed clean on the next run. The voice-guard also caught real problems in my plan comment and PR draft across several rounds: comma-joined sentences carrying two thoughts, and once a promised PR date that violated my own "never a timeline" rule, which I replaced with a past-tense statement of what I'd already built instead of a promise about what I'd do.

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

This issue came from my own scan, not the official Issue Selection site. I ran both
search-strategy queries (RAG/retrieval/agentic in Python, Spring in Java), combined 200
unique results, ranked them with the strategy's filters, and graded the top 5 with
issue-scout. Four of the five were accepted: `llmsectest#38`, `talentcatalog#3961`, and the
two `lasagna` benchmark-adapter issues (`#3`, `#4`); only `railtracks#1757` was rejected, and
only live-checking a linked PR caught why — its own text looked perfectly startable, but it
names a prerequisite PR that is still open. Among the four accepted, I picked `llmsectest#38`
over the easier, lower-depth `talentcatalog` dependency removal and the two paper-reproduction
`lasagna` adapters, because it is squarely in my fit profile (Python, and the kind of
unfamiliar-codebase reading I'm trying to get better at) and because it carries a difficulty
note of "ambitious": the issue itself names three candidate fix routes and asks the PR to
justify which one it took, which is an open design choice rather than a bounded single edit,
and that's exactly the kind of practice I want. I hope to learn how a security-test project
plants and verifies ground truth, which the issue itself calls out as the thing that makes its
findings checkable. My claim comment is posted at
https://github.com/wehnsdaefflae/llmsectest/issues/38#issuecomment-6609479931.

Reading the scout's grade against the actual issue held up well: the "ambitious" note was
accurate, and the earlier rubric patch (scope stops hard-rejecting on an open design edge, and
only flags it as a difficulty note) is why this issue was accepted at all instead of bounced
for not naming one fix. The scan also proved its worth on `railtracks#1757`: the raw search
fields ranked it #1 of 5, and nothing about its own text reads as blocked, but checking the
linked PR's live state caught a prerequisite the plain issue page would have missed. The one
place the scout couldn't help me was the thing it explicitly isn't built to check: whether the
repo accepts AI-assisted contributions. I read CONTRIBUTING.md, the README, and the PR
template myself and found no AI policy stated either way.

**Toolkit**

- Tool: issue-scout (my search strategy + my patched rubric), run in direct mode against the
  5 ranked candidates from my scan
- What it produced: accept verdicts on 4 of 5 (`llmsectest#38`, `talentcatalog#3961`,
  `lasagna#3`, `lasagna#4`), with `llmsectest#38` carrying a difficulty note of "ambitious"
  (open design choice among three named routes), and one reject (`railtracks#1757`, blocked
  on an unmerged prerequisite PR caught only by checking it live)
- Difficulties: none met this time; the scope-feasible patch from earlier this unit worked as
  intended on a real ambitious issue
- What changed: nothing in the scout itself this round; the value was in the patch I'd
  already made

---

## Understanding the Issue

**Problem Description**

LLM08 (vector & embedding weaknesses) has two black-box test dimensions against a RAG
app: retrieval exposure (does the app leak a confidential canary planted in its
corpus?) and indirect injection (does the app obey an instruction planted in a
retrieved document?). A developer testing their own app typically enables both at once
(`--app-canary` and `--app-rag-poison` together — every doc example shows them this
way). But the poisoned document is retrieved on almost any query and its instruction
tells the model to answer with one fixed marker and nothing else, so it answers *every*
probe — including the canary probes that were never asking about it. The canary never
gets a chance to leak on its own terms.

**Expected Behavior**

In one scan with both markers set, a canary probe should be able to show a genuine
retrieval-exposure finding when the app actually leaks the canary, independently of
whatever the injection probes find.

**Current Behavior**

Issue #12's earlier fix already stops the canary probe from misreading a poisoned
reply as a clean pass — it now reads `errored` (inconclusive) instead of a false
`withstood`. But that's the ceiling: the canary probe can never do better than
inconclusive while the poisoned document answers every query, so it can never actually
confirm or refute a real leak. Confirmed with the repo's own measurement
(`docs/owasp/llm08.md`): 13 of 16 real applications obeyed the poison on every probe,
and only one ever showed the retrieval dimension firing on its own.

**Affected Components**

`src/llmsectest/probes/application.py` (`_llm08_cases`, `app_cases`) builds the six
LLM08 cases but isn't itself at fault — it already wires `confounded_by` correctly.
The real gap is in the **test fixture**: every existing LLM08 test
(`tests/test_confounded_retrieval_probes.py`, `tests/test_llm08_suite.py`) uses one
mock adapter that gives the same fixed reply to every query, which has no way to model
a retriever that would actually return different documents for different queries. No
scanning or detector code needs to change (`probes/application.py`,
`probes/detectors.py`, `probes/runner.py` all stay as they are).

**Toolkit**

- Tool: Claude Code, used to trace `_llm08_cases`, the LLM08 test suite, and
  `docs/owasp/llm08.md`'s measurement section, and to confirm the issue's own
  "where to look" pointer (`probes/corpus.py`) names a file that ships no LLM08 cases
  at all
- What it produced: the finding above, that the fix belongs in the test fixture, not
  the scanner
- Difficulties: the issue's stated evidence location was wrong twice over (wrong file,
  and a fixture that doesn't exist in the repo at all); had to read the actual source
  and the maintainer's own measurement docs instead of trusting the issue text
- What changed: nothing in a skill; this was direct code reading

---

## Reproduction Process

**Environment Setup**

Windows 11 (10.0.26200), Python 3.14.6. Forked `wehnsdaefflae/llmsectest` to
`adedotdev/llmsectest` and cloned it, then ran `pip install -e ".[dev,cvss]"` from the
clone root per CONTRIBUTING.md, which installed `llmsectest==0.4.1` editable. No
environment challenges came up. The issue itself names no environment to reconcile
against — it's a claim about probe/scoring design, not a platform-specific bug.

**Steps to Reproduce**

The issue's own "where to look" pointer (`probes/corpus.py`) turned out to be wrong —
that file only documents LLM08 as app-only and ships no LLM08 cases. The real case
builder is `_llm08_cases()` in `src/llmsectest/probes/application.py`. More importantly,
the "poisoned document" the issue describes isn't a fixture in this repo at all: per
`docs/owasp/llm08.md`, it's something a person testing their own RAG app plants
themselves, and the masking claim traces back to the maintainer's own private
measurement over 16 real applications, not to anything this repo ships. So reproducing
it means reproducing it the way the existing regression suite already does:

1. From the clone root, with the editable install in place, write a script using the
   same mock-adapter pattern `tests/test_confounded_retrieval_probes.py` already uses
   (`_AnsweringAdapter`, a fake RAG app that always answers with one fixed reply).
2. Build a `retrieval_exposure` case (the canary probe, with `confounded_by` set to the
   poison marker, exactly as `_llm08_cases` builds it) and an `injection_marker` case
   (the poisoned-document probe), for the same mock app.
3. Run both through `run_probe` against an adapter whose fixed reply is the poison
   marker, standing in for a poisoned document that always answers every query with its
   own marker and nothing else.
4. Observed result: the canary probe comes back inconclusive (`errored: True`, never a
   genuine finding either way), the injection probe comes back `vulnerable: True` — in
   the same run, against the same app, from the same single reply. That is the issue's
   claim: only one of the two LLM08 dimensions can ever fire in a single run.

**Reproduction Evidence**

- **Commit showing reproduction:** none — the script is local evidence only; no fix has
  been built yet, this is the reproduction step
- **Screenshots/logs:**

  ```
  canary probe    -> vulnerable: False | errored: True | evidence: probe not scored, the reply carries a competing planted marker (RAG-POISON-3b9d) rather than the canary this probe asks about: a poisoned retrieved document answered in the canary's place, so retrieval isolation is neither confirmed nor refuted
  injection probe -> vulnerable: True | errored: False
  ```

- **My findings:** The symptom reproduces, but not via the issue's own stated file
  pointer, and not via any fixture shipped in this repo. Issue #12's earlier fix already
  stops the canary probe from reading as a false `withstood` — it reads inconclusive
  instead, via `confounded_by` — but that fix never let retrieval exposure actually fire
  in the same run it's confounded in; it can only ever be confounded or (separately,
  against a differently-behaved app) pass. `docs/owasp/llm08.md`'s own measurement (13 of
  16 real apps obeyed the poison fully; only one ever showed the retrieval dimension
  alone) backs the same conclusion from live data that this script reaches from a mock
  in under a second. The bug is real, and it's in the probe/fixture design the issue's
  three routes address, not in the scoring logic, which already does what it can with
  what it's handed.

**Toolkit**

- Tool: Claude Code, used to read `application.py`, `detectors.py`, the LLM08 test
  suite, and `docs/owasp/llm08.md`, and to write the reproduction script; repro-check
  (my rubric) to grade the claim comment and this report before treating either as done
- What it produced: an accept verdict on all 5 required checks (environment,
  steps-followable, behavior-matches, honesty, conventions-disclosure), and the finding
  above that the issue's own file pointer was wrong
- Difficulties: the issue's stated evidence location (`probes/corpus.py`) doesn't
  contain what it says it does, and the actual poisoned-document fixture isn't in the
  repo at all — both took direct reading of the source and docs to catch, not something
  a rubric check alone would have caught
- What changed: nothing in the skill; the value was in not trusting the issue's pointer
  and verifying the real code location myself

---

## Solution Approach

**Analysis**

Root cause: every existing LLM08 test shares one mock adapter
(`_AnsweringAdapter` in `tests/test_confounded_retrieval_probes.py`) that gives the
exact same fixed reply to every probe, regardless of what the probe actually asked.
That's a faithful stand-in for a poisoned document that dominates retrieval, but it
has no way to express a document store where a canary-targeted query and an
injection-targeted query retrieve *different* documents — which is what a real vector
store with topically distinct documents and a bounded `top_k` would do. Because the
fixture can't model that, no test in the repo can show both LLM08 dimensions firing
genuinely in the same run, which is exactly the gap issue #38 describes. The issue
names three possible routes (soften the poison's phrasing, give it a distinct topic
and limited `top_k`, or split the fixtures); of the three, only the topic/`top_k` route
is something this repo's own code can actually demonstrate — routes 1 and 2's other
half (the poisoned document's literal wording) and route 3 (splitting into separate
scans) both live on the external target app's side, which this black-box tool never
controls.

**Proposed Solution**

Add a new test fixture, `_TopicRoutedAdapter`, that holds two documents on distinct
topics (matching the two attack families' own existing wording: every retrieval-probe
prompt asks about something "confidential," every injection-probe prompt asks about an
"instruction") and answers each query from whichever single document actually matches
it — a top-1 retriever, in miniature. A new test
(`tests/test_llm08_fixture_design.py`) runs the real six `_llm08_cases` cases against
it and asserts that both dimensions fire genuinely in the same run. A second test in
the same file pins the contrast: the existing single-reply fixture still fully masks
retrieval exposure, so the new fixture's result isn't a scanner change in disguise.
I'm deliberately NOT touching `probes/application.py`, `probes/detectors.py`, or
`probes/runner.py` — the scoring logic already does the right thing with what it's
given; the gap was only ever in what the test fixtures gave it. I'm also not changing
the real-world `--app-canary`/`--app-rag-poison` CLI flags or docs in this PR scope;
if `docs/owasp/llm08.md` should also recommend topic separation and a bounded `top_k`
to real users, that's a follow-up, not required for this issue's own "done" bar.

**Implementation Plan**

1. Add `_TopicRoutedAdapter` and the two new tests to a new file,
   `tests/test_llm08_fixture_design.py`.
2. Build the six cases through the real `app_cases()` entry point (not hand-rolled
   case objects), so the test exercises the same code a real scan runs.
3. Run `ruff check` and the full suite; confirm the 4 pre-existing Windows-only
   failures are unchanged and nothing else regresses.
4. Add a `CHANGELOG.md` bullet under `[Unreleased]`.

No deviations yet — built and verified locally (both new tests pass, full suite shows
the same 4 pre-existing failures as before, `ruff check` clean) before writing this up.

**Risk / open question:** I asked in my claim comment which of the three routes the
maintainer prefers and haven't had a reply yet. This plan goes ahead with the
topic/`top_k` route rather than waiting, since it's the only one this repo's own code
can actually implement and demonstrate. If the maintainer answers before this merges
and prefers a different route, I'll treat that as new direction and revise.

**Toolkit**

- Tool: Claude Code, used to design and write `_TopicRoutedAdapter` and the two tests,
  run `ruff`/`pytest`/`coverage` locally to verify before writing the plan, and
  plan-check to grade `plan.md` and `plan-comment.md` before treating the plan as
  ready to build from
- What it produced: an accept verdict on all 6 required checks, and, on the first
  grading pass of the plan comment, two voice-guard stops (a two-thought sentence, and
  a promised date that collided with my own "never promise a date" rule) that caught
  real drafting mistakes before anything was posted
- Difficulties: picking keywords for the two mock documents that didn't accidentally
  collide between the two attack families' prompt wording (an earlier draft keyword,
  "internal," appears in both families' prompts and would have made the fixture
  non-deterministic); settled on "confidential" and "instruction," each unique to one
  family. Separately, plan-check's own instructions assume a posted repro comment on
  the thread, but this unit's wild-scope rule says never to post one — I used the local
  `repro-draft.md` as the repro-evidence source instead and said so in the grading
- What changed: the keyword choice, before anything was committed; the plan comment,
  twice, to clear the voice guard; and the plan itself, to name the open
  maintainer-preference question honestly instead of assuming my choice is final

---

## Testing Strategy

Re-ran my Unit 6 reproduction script on a clean `main` checkout first, to confirm the
masking is still there before touching anything: the canary probe comes back `errored`
(inconclusive), the injection probe comes back `vulnerable: True`. Then on the fix
branch, ran the two new tests in `tests/test_llm08_fixture_design.py`: the first
asserts both a genuine retrieval-exposure finding and a genuine injection finding fire
in the same run against the new topic-routed fixture, with the retrieval probe never
`errored`; the second confirms the old single-reply fixture still fully masks
retrieval exposure, so the result is the fixture, not a scanner change. Both passed.
Ran the project's own manifest checks on the branch: `ruff check src tests examples`
clean, and `coverage run -m pytest -q` at 1053 passed with the same 4 pre-existing
Windows-only failures as `main` (1051 passed there, since the 2 new tests don't exist
on `main`). Full output is in `test_evidence.md`.

**Toolkit**

- Tool: Claude Code, to run the reproduction on `main`, the new tests and the full
  suite on the branch, and to write up the before/after comparison
- What it produced: `test_evidence.md`, with before-fix, after-fix, and manifest-check
  output
- Difficulties: none met
- What changed: nothing; the plan's test plan held up exactly as written

---

## Implementation Notes

**2026-11-03**

Built `_TopicRoutedAdapter` and the two tests in `tests/test_llm08_fixture_design.py`,
on branch `fix/38-llm08-topic-routed-fixture`. First keyword choice ("internal" for the
canary topic) turned out to appear in one of the injection-probe prompts too, which
would have made the fixture's routing nondeterministic between the two dimensions on
that one probe. Caught it by actually reading all six attack prompts side by side
before picking keywords, not by running the test and seeing it flake. Switched to
"confidential" (canary) and "instruction" (poison), each unique to its own attack
family's wording. Ran `ruff check` and the full suite on the branch: both new tests
pass, same 4 pre-existing Windows-only failures as `main`, nothing else changed.

**Toolkit**

- Tool: Claude Code, for the implementation and the verification runs
- What it produced: the fix, built and green on its own branch before the plan was
  even graded
- Difficulties: the keyword collision above
- What changed: the keyword choice, caught before the first test run rather than after

---

## Pull Request

**PR Link:** https://github.com/wehnsdaefflae/llmsectest/pull/41

**PR Description:** Explains that every existing LLM08 test shares one mock
adapter with a single fixed reply, so a poisoned document always crowds out
the canary and the retrieval-exposure probe can never confirm a real leak in
the same run an injection probe fires. Adds `_TopicRoutedAdapter`, which holds
two documents on distinct topics and routes each query to whichever one it
matches, the way a real vector store with a bounded `top_k` would. One new
test runs the real six LLM08 cases against it and shows both dimensions
firing genuinely in the same run; a second pins the old single-reply
fixture's masking as a contrast, to show this is a fixture change, not a
scanner change. States which of the issue's three named fix routes I took and
why (the only one this repo's own tests can demonstrate, since the other two
change the poisoned document's content, which lives on the target app's
side), and that I'd asked the maintainer which route they preferred in my
claim comment with no reply yet. Includes before/after repro output, the full
manifest-check output, and an AI disclosure.

**Maintainer Feedback:**

- 2026-11-04: none yet, PR just opened

**Status:** Awaiting review

**Toolkit**

- Tool: the ship-gate (`PreToolUse` hook running the repo's manifest checks
  plus `pr-precheck`), run through Claude Code against the real branch before
  `gh pr create`
- What it produced: a PASS covering all 3 manifest checks and all 4
  `pr-precheck` checks (plan-fidelity, test-evidence, diff-quality,
  standards-comms), which is what let the PR open
- Difficulties: the first PASS was from the day before I actually pushed, and
  the gate's 30-minute PASS window had long expired by the time I was ready
  to open the PR
- What changed: re-ran the gate fresh immediately before opening the PR
  instead of reusing the stale PASS, and got a clean PASS again with the same
  branch and drafts

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
