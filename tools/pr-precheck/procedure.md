# Procedure: how this tool grades a PR package

## Read order

1. Read the issue and sum what's broken in one line.
2. Read the plan before the PR. If you read the description first, you will just believe the description. Start with the plan, write down the files, the approach in one line, the not-in-scope line, each step promised, each repro or failure mode in the test plan, whether the test plan says to run the suite, and any deviation or deferral note exactly.
3. Go through the diff one hunk at a time and note the file and hunk function.
4. Read the commit list.
5. Read the test evidence and note the command, the before, and the after for each run.
6. Read the title and description last. Note every change and deferral they mention.
7. Read the repo facts block (live: the PR template, CONTRIBUTING.md, AI policy, and the house rules in `scope.md`). Note every ask and whether AI disclosure is required.

## Evidence gathering

- Diff inside plan: Match each hunk to the plan's files and approach. It's either planned, covered by a deviation note, or unplanned.
- Plan delivered: Find the hunk for each promised step. It's delivered, deferred with a note in both the plan and description, or missing. Do the same for each thing the description claims and write it down if there's no hunk.
- Test evidence: Find a run for each repro from the repro evidence. Note if it shows before and after, only says it works, tests a different path, or isn't there. For everything else in the test plan (controls, extra cases, smoke checks, the suite), just note if it's named with its result or missing.
- Debris: Look through every hunk for debug prints, commented-out code, unused functions, TODOs, and formatting or import changes the fix doesn't need. Quote anything you find.
- Repo asks: Find where the description or diff covers each ask. It's met, boilerplate, or missing. Copy the disclosure line or write none.

## Check execution

Run the checks in rubric order, starting with Diff stays inside the plan. It goes first since the later checks use the same hunk notes.

Grade each check from the notes above. One problem fails a check. Stuff like an unplanned hunk, a missing step, a claim with no hunk, a run that only says it works or tests the wrong path, debris, or a missed ask. Only go back to the package if two notes contradict each other.

If the evidence for a check isn't in the package, grade it unclear, write what's missing as the evidence, and move on. Don't guess and don't ask the author.

## Verdict assembly

Use the rubric's verdict rule. All five checks have to pass to accept. Unclear counts as fail.

On a reject, the first failing check in rubric order decides it. Quote the fact that failed it in the summary and in that check's evidence line.
