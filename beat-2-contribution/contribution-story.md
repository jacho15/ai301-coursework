# Contribution: [Issue Title]

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Jacob Cho
**GitHub Username:** jacho15
**Issue:** [GitHub issue link]
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built issue-scout and ran the first wild scan**

2026-10-07: I turned the issue-select skill from Unit 1 into another skill called issue-scout and had the search strategy aimed at GPU, compiler, and inference repositories (NVIDIA, AMD, Tenstorrent, IREE, llama.cpp, vLLM). The skill ran three scans that graded 15 issues, and all 15 issues end up being rejected. They were mostly all rejected because someone else had already claimed the issue or opened a PR. However, for LLVM and IREE specifically, the scans found that they both forbid AI tool usage on their good first issues which my AI policy check actually only found by luck. I had to fix my rubric to follow adopted policies and to fail issues that are already completed. I then changed the strategy to skip banned repos and anything that had already been rejected. The "fixed" rubric still scores 18/20 on the unit-1-eval.

**Unit 6: Installed the voice-guard and posted my first claim**

2026-10-14: I added a voice check before I post which is just a hook that reads every `gh` comment that I post through Claude Code and checks it against my own voice guide. There is a singular voice guide that I created from merging my other 3 voice guides into one. I wrote 5 rules total for claims, questions, and pings. I swapped repro-check and plan-check I merged my three voice guides into one, wrote five upstream rules for claims, questions, and pings, and swapped repro-check and plan-check to the wild scopes. The wiring test blocked `gh issue comment --help` as it should, and my claim for the OpenVINO issue passed the guard and posted. Windows symlinks made copies of the guide instead of links, so I used pointer files. The guard checks my rules and not who wrote the words. OpenVINO's policy bars AI-generated communication, so I rewrote the first claim draft in my own words before posting. The only stop in the guard log is the wiring test, and every real check passed, so my rules held and nothing got blocked. I haven't written the repo memory file yet.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I picked an OpenVINO bug in the FakeConvert op. Constant folding gives different answers than the CPU kernel for small float8 values and for NaN. It's C++ numerics in an inference runtime, and it doesn't need a GPU.

I didn't find it through my scout. I found it offline while I was looking at repos my first scans never reached. My first four scans graded 20 good first issues and rejected all 20. Eighteen of them failed on "Nobody else already on it," because strangers grab those issues within days. After that I added a query, Q5a, for fresh bugs with zero comments and no linked PR from the last 7 days, and split it by my fit profile so inference runtimes come first. Scan 5 graded this issue in its top five and accepted it with a moderate difficulty note. The note says the reference function is named in the report, but I'd need to confirm which result is the source of truth. The scout also graded it directly earlier, and that grade is saved next to the scans. I changed the query order after I'd already picked the issue, and the strategy file says so.

The scout flagged two things. The "Friendly-issue signal" check failed, because the issue has no good first issue label and the opener isn't a maintainer. That check only ranks accepted issues, so it didn't change the verdict. The reporter also wrote an AI-generated summary. OpenVINO's AI policy bars auto-generated issues that don't describe first-hand observations, but the report has output from a real run, so my new "Written by a person who ran it" check passed it. OpenVINO's policy allows AI help if I understand and verify the work and disclose it in the PR.

I hope to learn how a real inference runtime is organized and how bit-level rounding bugs get fixed and tested.

Claim comment: https://github.com/openvinotoolkit/openvino/issues/38799#issuecomment-6181345301

My read of the scout: It rejected correctly every time, but searching by good first issue just finds what everyone else finds. Patching the strategy fixed that. I also added a bot-ticket check to the rubric and took llama.cpp out because its policy bans AI-written PR text and replies, and I'd be working against it.

**Toolkit**

- Tool: issue-scout, my scout with my strategy and rubric. I ran a direct grade on the issue and a funnel scan.
- What it produced: Scan 5 accepted this issue with a moderate difficulty note, along with a second OpenVINO issue and a TensorRT-LLM issue. It rejected two vLLM issues for existing fixes and an offered claim.
- Difficulties: The label-based queries couldn't find an unlabeled issue. The ranking also capped this issue out of the top five until I split Q5. The Friendly-issue check fails fresh unlabeled bugs and the Response speed check came out unclear again.
- What changed: Added Q5a and Q5b, dropped Q1 and Q1b, and dropped llama.cpp. Added the "Written by a person who ran it" check and replaced my scope row with the scope-feasible row and difficulty note. I didn't re-run the unit-1 regression after these patches.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
