# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: week 1 handed you this file
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
nobody else can execute; your operator swap showed you what that feels
like. Write the map you wish your executor had.
-->

## Environment

Where it lives: in a bundle, the repro report's own environment section. Live, the equivalent section of the student's draft report.

What good looks like: OS and the exact version of the software under test spelled out in plain English as explicit facts. A release version, tag, commit hash, or explicit date all count, and a stated release version can serve as both the version and the code-state marker. If the stated version differs from what the issue or repo docs target, the report mention it instead of staying silent.

## Steps

Where it lives: the repro report's numbered/ordered list in the bundle or draft.

What good looks like: Each step is a concrete command or action with every prerequisite spelled out and starting from a clean checkout. Also make sure that the last step performs the exact action the issue names as the trigger, regardless of whether the bug's effect actually appears; that part is judged elsewhere.

## Behavior shown

Where it lives: The report's output which includes a traceback, log line, or test result, next to the issue's own description of the failure (issue body, in the Issue section, or the issue thread).

What good looks like: The excerpt's error type and triggering input match what the issue describes, or the report states "could not reproduce" and shows the output it got when it tried. Some stuff that doesn't count is an excerpt showing a different error, different code, or a different environment does not count.

## Honesty

Where it lives: The gap between the report's stated conclusion and the output above, both inside the repro report.

What good looks like: The conclusion claims exactly what the output supports. A confident claim of reproduction, of certainty or of any result stated with no output artifact behind it is an invalid conclusion.

## Comms

Where it lives: The claim comment text read against the issue it names and against the repo-facts block's stated contribution/AI-use policy (bundle) or the repo's CONTRIBUTING/issue templates (live).

What good looks like: The claim names the issue and an issue-specific detail. Reporting progress already found, like already reproducing part of it, is fine as long as remaining work is still framed as ongoing, such as promising to keep investigating and report back. It should not declare the issue fully resolved or promise a specific fix or date. On disclosure specifically: pass if the repo's policy is silent, or if it requires disclosure and the comment disclose and fail only when disclosure is required and the comment gives none.
