---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You're answering one thing about one PR package: is this pull request ready to submit? The package is the PR's title, description, commits, diff, and test evidence. Check all of that against the plan it says it implements and the issue the plan is for. Don't grade anything else and only grade one package per run.

## Inputs and modes

If someone hands you a package bundle, that's eval mode. If a student asks you to check their own branch, that's live mode.

In live mode you need five things:

1. The plan. The student's `plan.md` with any deviation notes. House-chain students use the house plan.
2. The diff. Everything the branch changes against the default branch. Get it with `git diff main...HEAD` (three dots, and use the real default branch if it isn't `main`). Also run `git log --oneline main..HEAD` for the commits and `git status` to catch files about to get committed.
3. The title and description. Usually in `pr_draft.md` with the title on the first line.
4. The test evidence. Usually in `test_evidence.md`. House-chain students take their repro steps from the house repro pack.
5. The issue URL. Get the thread, `.github/PULL_REQUEST_TEMPLATE.md`, CONTRIBUTING.md, and any AI policy from the actual repo.

If one is missing, say which one and let the verdict rule handle the checks that needed it. Don't make it up.

In eval mode the bundle is all you get. Every fact has to come from its sections (Repo facts, Issue, Thread highlights, Plan context, Candidate PR). Don't fetch anything or open other files. Grade every check with the full verdict rule. Assume every eval package was written with AI help.

## The scope seam (live mode only)

Read `scope.md` first. If the repo line is still a bracketed placeholder, stop and tell the student to get the scope file from their instructor. Don't guess one. If the issue or the PR's target repo isn't the one in scope, refuse and explain why. Otherwise use the house rules as evidence. Stuff like the PR coming from the student's fork on a `fix/<issue-number>-<slug>` branch, one PR per issue, the template always used, and AI disclosure always required since course work is AI-assisted. In eval mode skip `scope.md`.

## The voice seam (live mode only)

After grading, read `voice-guide.md`. Check the draft title and description against each rule and the "Things I never post" list. If the draft breaks a rule, quote the rule and the words that broke it in the summary. This doesn't change the verdict since no rubric check uses the voice guide. In eval mode skip `voice-guide.md`.

## Component reads

The checks and verdict rule are in `rubric.md` and those are the only checks. Don't add, remove, or loosen any while grading. `references/evidence-guide.md` says where to find each kind of evidence and what good looks like. `procedure.md` has the steps. Follow them in order.

If the procedure doesn't cover something, do the least the pass condition needs and call it out in the summary as a procedure gap.

If `rubric.md` is missing its checks or verdict rule, or `procedure.md` has no steps, stop and say which file is empty. Don't grade anything.

## Verdict and output

There are only two verdicts. `accept` means submit and `reject` means hold. Any concerns go in a check's evidence line, not the verdict.

Start with a short summary with one line per check (name, grade, and the evidence that decided it). On a reject, say which check decided it. In live mode add any voice guide problems. Then end with the JSON block below. It has to be valid and the very last thing. For `item`, use the PR URL in live mode (the issue URL if the PR isn't open yet) or the bundle id in eval mode. Add one entry per rubric check, in rubric order, using the rubric's check names.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Every grade needs the fact or quote that decided it. "Looks fine" doesn't count.
- Grade what the PR does, not how it's written. Compare the diff to the plan, the evidence to the test plan, and the description to the diff. A description that says "no changes beyond the plan" means nothing until the diff backs it up.
- The rubric makes the call. If a check passes on its condition but something feels off, it still passes. Put it in the summary.
- Follow `procedure.md` as written and point out where it falls short.
- Unclear counts as fail unless the verdict rule says something different.
- If the plan records a shortfall and the description mentions it again, the PR can still pass.
