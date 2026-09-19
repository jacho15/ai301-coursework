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

I'm a software engineer with quite a bit of enterprise level experience. I am in this repo because I want to start learning how to contribute to open source, particualrly in Python and lower level stuff like C++. Readers can expect me to have clean code and I'll have as little abstractions as possible, only the bare minimum (that is what I try to live by).

## Rules I write by

Rule: <Readability>
- Wrong: "Refactored the whole function while I was in there to make it cleaner"
- Right: "Kept the fix to the two lines the bug required; left the rest of the function untouched"

Rule: <Styling>
- Wrong: "Reformatted the file to match my usual style"
- Right: "Matched the file's existing formatting conventions"

Rule: <Verification>
- Wrong: "This should fix it"
- Right: "Ran the repro script five times after the fix; the error no longer appears"

## Things I never post

1. Never let a fix that hasn't been tested since no one will tolerate that.
2. Never suggest a rewrite in a thread about a bug fix, even if the code offends my minimal-abstraction guideline.
3. Never argue a design decision with a maintainer's history we haven't analyzed.
