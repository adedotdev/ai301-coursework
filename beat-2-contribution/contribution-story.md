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
**Pull Request:** [GitHub PR link, once opened]

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

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

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

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

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
