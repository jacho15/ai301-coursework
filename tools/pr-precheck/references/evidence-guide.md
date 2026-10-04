# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Where it lives: Look at the plan context block. You want its file list, the approach, the not-in-scope line, and any deviation notes. Check them against the PR's diff and description. Live, that's `plan.md` against `git diff main...HEAD` and `pr_draft.md`.

What good looks like: Each hunk is in a file the plan names and does what the approach says. Every step the plan promised is in the diff too. Any drift can go over the plan. Stuff like an extra file, a new flag, renaming things, or rewriting code around the fix. It can also go under the plan when a promised step isn't there and nobody wrote down why. Watch the description as well. If it says docs were updated and there's no docs hunk, that's drift. Same thing for "no changes beyond the plan" and the diff touches a file the plan never mentions. If the plan defers something and the description says so again, that's fine.

## Test evidence (harness category: not-tested)

Where it lives: The test evidence section of the PR, checked against the plan's test plan and the repro steps. Live, it's `test_evidence.md` and the test plan in `plan.md`.

What good looks like: Each repro from the repro evidence gets run again with the command, what happened before, and what happens now (real output, an error, or an exit code). It has to run through the code the diff changed. Controls, extra cases, smoke checks, and the suite don't need a before and after, but they can't be skipped. Naming the command with its result is enough, like "`pytest tests/unit` passes". "Tested locally" or "works now" on the repro itself doesn't count. Same thing for only running the control case or running something the diff never touched.

## Diff quality (harness category: unreviewable)

Where it lives: The diff and the commit list. Live, `git diff main...HEAD`, `git log --oneline main..HEAD`, and `git status`.

What good looks like: The diff is just the fix, its tests, comments about the fix, and anything the plan or repo asked for. Stuff that shouldn't be there: debug prints, commented-out code or old attempts, functions nothing calls, leftover TODOs, and reformatting or import changes on lines the fix didn't need. Commit messages like "wip" or "cleanup while debugging" mean you should look closer. Live, `plan.md`, `pr_draft.md`, or `test_evidence.md` in the diff counts as debris.

## Standards and comms (harness category: standards-wall)

Where it lives: The repo facts block. The "pull requests" line has the template asks and the "contribution policy" line has the AI policy. Check both against the description and diff. Live, read the repo's `.github/PULL_REQUEST_TEMPLATE.md`, CONTRIBUTING.md, any AI policy, and the house rules in `scope.md`, then check them against `pr_draft.md`.

What good looks like: Anything the repo asks for is there and filled in. That could be a "closes #123" line, a changelog or whatsnew entry in the diff, or sections like Problem and Solution. If the AI policy says to disclose, the description has to say how AI was used in the author's own words. A policy that just allows AI with a human in the loop is covered by an honest disclosure line. No AI policy means no disclosure needed in eval mode. Live mode always needs one because the course requires it. Whether the description matches the diff is a plan fidelity question, not this one.
