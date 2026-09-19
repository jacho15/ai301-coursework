# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | Repro report's environment section (OS, exact version of the software under test, some form of version control). | Pass if OS and the exact version of the software under test are both spelled out in plain English as explicit facts. A release version, tag, commit hash, or explicit date all count as the version marker, and a stated release version can serve as both the version and the code-state marker. Fail if OS or the version is missing, or the report just says something like "my machine". | required |
| Steps are followable | Repro report's numbered/ordered steps. | Pass if a stranger starting from a clean checkout could run the steps with every prerequisite spelled out, and the last step performs the exact action the issue names as the trigger, regardless of whether the bug's effect actually appears. Fail if a step relies on a prerequisite the report never states, or the steps stop short of attempting the trigger action itself. | required |
| Behavior matches the issue | The report's output (traceback, log line, or test result) next to the issue's own description of the failure. | Pass if the output's error type and triggering input match what the issue describes, or the report says "could not reproduce" and still shows what it got when it tried. Fail if the output shows a different error, different code path, or a different environment, even if the report narrates it as matching. | required |
| Outcome stated honestly | The report's stated conclusion, read against the output above. | Pass if the conclusion claims exactly what the output supports, including an honest "could not reproduce". Fail if the report claims a repro the output doesn't show, claims certainty with no repeated runs shown, or states a result with nothing behind it. | required |
| Claim comment scope | Candidate claim comment text. | Pass if the comment names the issue and at least one issue-specific detail. Reporting progress already found, such as "I can reproduce X," is fine as long as remaining work is still framed as ongoing, such as "next I want to check... and report back." Fail on generic boilerplate with no issue-specific detail, or a comment that declares the issue fully resolved or promises a specific fix or date. | required |
| Disclosure / conventions | Repo-facts block's stated AI-use policy, read against the claim and repro comment. | Pass if the policy is silent, or it requires disclosure and the comment discloses. Fail only if disclosure is required and neither comment discloses. | required |

## Verdict rule

Accept only if every required check passes. Any fail or unclear on a
required check rejects the package. Unclear counts as fail. No
preferred checks here.
