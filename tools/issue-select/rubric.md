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
| Maintainer alive | Last 5 commit authors, first-response sample, issue thread (repo-facts block). | A human commit in the last 120 days, any real reply in the first-response sample, or an OWNER/MEMBER/COLLABORATOR comment on the thread. Fail if none of those hold. | required |
| Repo in use | `archived:` flag, last push date (repo-facts block). | Not archived, and last push within 120 days. Fail otherwise. | required |
| Nobody else already on it | Assignees, linked PRs, claim comments (repo-facts block + thread). | Fail on an assignee, an open linked PR, or an unanswered claim comment from the last 90 days nobody's marked stale. An old claim with no open PR passes. | required |
| Scope fits a newcomer | Issue body and thread. | Fail on an umbrella that invites many contributors to split the work into separate PRs, an unsettled design debate, a support question, a maintainer saying it needs core-internal changes, or a feature request where the opener admits the concrete shape is still undetermined ("TBD", "not identified yet"). A fully-specified deliverable for one contributor in one PR passes even across several files or with no maintainer reply yet, as does a plain bug report with a clear fix location or a list of similar small fixes sharing one pattern. | required |
| AI-contribution policy allows this | Contribution policy line (repo-facts block / CONTRIBUTING.md). | Fail only on an outright AI ban. Conditions (disclosure, review, testing) pass; silence passes. | required |
| Response speed | First-response sample. | Prefer issues where most sampled responses came within 14 days. Ranks accepted issues only. | preferred |
| Friendly-issue signal | Opener's author association, issue labels. | Prefer maintainer-opened issues or a "good first issue" label. Ranks accepted issues only. | preferred |

## Verdict rule

Accept if and only if all five `required` checks grade `pass`. If any required check grades `fail` or `unclear`, the verdict is `reject`. Make sure `unclear` is treated as `fail`. Ensure that `preferred` checks never change the verdict; simply report their grades, and for an accepted issue use them (together with the fit profile in `scope.md`) only to rank it against other accepted candidates.
