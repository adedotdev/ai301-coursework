# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-alive | Repo facts: maintainer first-response sample, and last 5 default-branch commits (author + date) | At least one of: (a) a sample issue got an owner/member/collaborator comment within 30 days of the capture/today date, or (b) at least one of the last 5 default-branch commits was authored by a named human (not a `[bot]` account) within 30 days of the capture/today date | required |
| repo-in-use | Repo facts: last push to any branch, archived flag | Last push within 180 days of the capture/today date, and the repo is not archived | required |
| scope-fits | Issue body, comment thread, and repo facts on linked PRs | Issue names one problem or one feature a single contributor could complete end to end. Multiple files, multiple contributing causes, several closely-related sub-parts of the same feature, or the reporter's own list of possible approaches do NOT by themselves fail this — that is still one deliverable with one owner. A terse body is not a scope failure either, especially from a maintainer/collaborator or under a "good first issue" label. Fails when: the issue explicitly asks for its sub-items to be split across separate contributors/PRs (a real tracking/umbrella issue); the design is still being actively argued with no maintainer sign-off; a maintainer says it touches core internals; the issue's age and history show multiple abandoned attempts (closed/unmerged linked PRs, or a thread showing repeated claim-then-unassign cycles) pointing to real difficulty beyond what the text suggests; or the request's own text leaves the actual deliverable undecided — what asset, output, or even which part of the codebase would change ("TBD", "not identified yet", "possibly X, if needed") — with no maintainer having weighed in to settle it. This is different from a clear problem with multiple candidate implementation approaches (normal for any bug; a contributor picks one and that does not fail this check) | required |
| nobody-on-it | Repo facts: assignees, linked PRs, this issue's comment thread | No current assignee, no open linked PR, and no PR referenced in the thread that currently implements the fix. A closed/unmerged linked PR, or a claim comment with no continued activity since (no reply, no update, no follow-up PR), is an abandoned attempt, not a current claim, and does not fail this check | required |
| ai-policy-ok | Repo facts: contribution policy line | No outright ban on AI-assisted contributions. Disclosure, human-review, or understand-your-own-code conditions are not a fail; silence is not a fail | required |

## Verdict rule

Accept only if every required check passes. `unclear` counts as a fail
on that check. There are no preferred checks yet.
