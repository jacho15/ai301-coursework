# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis follows from evidence | Plan's stated cause and its approach's target location, read against the repro-evidence block. | Pass if the cause explains exactly the behavior the repro evidence shows, and the approach changes code at that cause's location. Fail if the cause contradicts or ignores the evidence, the approach patches a symptom while the cause points elsewhere, or there is no repro evidence to read the cause against. | required |
| Scope is bounded | Plan's in-scope statement, not-in-scope line, and files or areas named. | Pass if the plan names one bounded change and states what it will not touch. Fail if there is no not-in-scope line, or the change spans files or areas beyond the diagnosed cause. | required |
| A stranger could start executing it | Plan's approach, files or areas, and order of work. | Pass if the files are named, the first concrete step is stated, and nothing requires asking the author a question first. Fail if the approach stays vague ("investigate and fix"), names no file or location, or skips a step a stranger would need. | required |
| Test plan names an observable outcome | Plan's test plan section, read against the repro-evidence block's steps and artifacts. | Pass if the test plan re-runs or adapts the repro steps and states the result that confirms the fix. Fail if the test plan is vague ("verify the fix works") or does not map to the repro evidence at all. | required |
| Unknowns stated honestly | Plan's risks/unknowns section. | Pass if the plan names its actual unknowns and risks in plain language. Fail if the plan claims the fix will work without having tested it, or leaves out a risk the diagnosis or scope clearly carries. | required |
| Comms respects the thread and repo | Plan comment text, read against the issue's thread highlights and the repo-facts block's stated templates and contribution/AI-use policy. | Pass if the comment states this plan's specific approach, engages with any direction a maintainer already suggested, and discloses AI use when the policy requires it. Fail on generic boilerplate, a comment that ignores a maintainer's stated direction, or missing disclosure when the policy requires it. | required |

## Verdict rule

Accept only if every required check passes. Any fail or unclear on a required check rejects the package. Unclear counts as fail. No preferred checks here.
