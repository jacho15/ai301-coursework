# Voice guide: how I talk upstream

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

Rule: <Committing to an approach>
- Wrong: "This should definitely fix it"
- Right: "Here's the approach I'm planning to build; I'll report back once it's tested"

Rule: <Engaging existing direction>
- Wrong: "I'll take a look and figure out the best fix"
- Right: "Building on what was suggested in the thread, I'll change X in file.py to do Y"

## Things I never post

1. Never let a fix that hasn't been tested since no one will tolerate that.
2. Never suggest a rewrite in a thread about a bug fix, even if the code offends my minimal-abstraction guideline.
3. Never argue a design decision with a maintainer's history we haven't analyzed.
4. Never promise a timeline or a merge date in a plan comment.
