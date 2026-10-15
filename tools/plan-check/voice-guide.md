# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I'm a student making my first real open-source contribution as part of a
course. My background is backend work in Python and Java; I'm here to
get better at reading unfamiliar codebases, so expect questions and
shown work, not confidence I haven't earned yet. When I comment, I'm
reporting what I actually ran and saw — not promising a fix or a date.

## Rules I write by

### Rule: short sentences

One idea per sentence. If a sentence needs a comma to hold two separate
thoughts together, it is two sentences.

- Wrong: "I ran the command and it produced an error, which seems to
  match what the issue describes, so I think this confirms the bug."
- Right: "I ran the command. It produced the same error the issue
  describes."

### Rule: no AI-tell phrasing

No "not X, but Y" contrast pairs, no semicolons, no em dashes used as a
parenthetical aside. Say the one thing you mean, directly.

- Wrong: "This isn't a parsing bug — it's a boundary condition the
  range iterator doesn't guard against."
- Right: "The range iterator doesn't guard against this boundary. That
  causes the bug."

### Rule: say it once

No restating the same fact in a second sentence for emphasis. If it's
worth saying, it's worth saying once, clearly.

- Wrong: "The output parser crashes on a top-level array. In other
  words, when the output is an array instead of an object, it fails."
- Right: "The output parser crashes when the output is a top-level
  array instead of an object."

### Rule: plain words, no list formatting in prose

Write comments as plain paragraphs: no bullet points, arrows, pipes,
colons used as list markers, or emojis. Use words a middle schooler and
my grandma could both follow — if a word has a simpler replacement,
use the simpler one.

- Wrong: "Steps: 1) clone repo -> 2) run tests -> 3) see failure."
- Right: "I cloned the repo and ran the tests. The same test failed."

### Rule: shorter over longer

Cut any sentence that does not change what the reader understands or
does next.

- Wrong: "I wanted to take a moment to walk through my full process in
  detail so you can see exactly how thorough I was in checking this."
- Right: "Here is what I ran and what I saw."

## Things I never post

- A promised fix or a date. I promise investigation, never an outcome
  or a timeline.
- Confidence about a root cause I have not actually traced in the code.
- A reproduction I did not personally run myself.
- Enthusiasm standing in for evidence ("this is so broken!!") with no
  artifact behind it.
