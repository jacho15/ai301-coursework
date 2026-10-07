# Scan notes

One dated line per moment the wild surprised my tooling. Each line names the check or filter and quotes what confused it.

## Scan 1 (2026-10-07)

- 2026-10-07, setup: `gh` wasn't installed, so nothing in the scout could run. Installed it with winget, but this shell doesn't see it on PATH until a restart, so I called `C:\Program Files\GitHub CLI\gh.exe` by full path.
- 2026-10-07, all queries: Repos don't share a label name. tt-mlir has zero `good first issue` but uses `good-first-issue`, IREE uses `good first issue 🌱`, TVM uses `beginner-friendly`, and HIP uses `difficulty:A_Easy`. My first pass said tt-mlir, IREE, and TVM had nothing. Patched the strategy with Q2b and Q1b.
- 2026-10-07, Q2b: The comma-OR label form with quotes (`label:"good first issue",good-first-issue`) returned 0 for tt-metal, which has 20+ open. On Windows gh mangles the quoted part. Unquoted names work, so labels with spaces go in `--label` and the others go in the query text.
- 2026-10-07, Q1 and Q3: Both came back at exactly 100, the `--limit`. Search sorts by best match by default, so llvm-project's 200+ issues got cut at random before ranking saw them. Added `--sort updated` to both.
- 2026-10-07, ranking filter 1 (drop assignees): Dropped 140 of 273 unique results. Most were llvm-project, where people get assigned when they ask for an issue. The filter is doing its job, but llvm's open `good first issue` count looks a lot bigger than what's free.
- 2026-10-07, ranking: Tier ordering plus the 2-per-repo cap gave tt-metal 2, cccl 2, and circt 1. Q3 (inference runtimes) never reached the top five because Q2 and Q1 had enough survivors. That's what I asked for, but it means Q3 only matters if the first two tiers run dry.
- 2026-10-07, all five verdicts: Every one got rejected on Nobody else already on it. Three of the five had a stranger's claim or PR from the last two weeks. Ranking filter 6 (newest `updatedAt` first) pushes these up, because a fresh claim comment is what bumped `updatedAt`. The filter is rewarding the exact thing the rubric rejects.
- 2026-10-07, tt-metal#40699 and #42916: The same stranger (alexxony) claimed both within a day. One person sweeping a repo's good-first-issue list can take out a whole tier.
- 2026-10-07, AI-contribution policy allows this, circt#3662: CIRCT has no CONTRIBUTING.md. Its policy lives in docs/AIToolPolicy.md, linked from the README and the PR template, and says "Using AI tools to fix 'good first issue' labeled issues" is not allowed. My check only says to fail on "an outright AI ban". The grader failed it because the ban covers this exact issue, but a strict reading passes it. And if the grader had only looked at CONTRIBUTING.md, silence would have passed it.
- 2026-10-07, Q1: Checked llvm-project's llvm/docs/AIToolPolicy.md and it has the same rule: "Using AI tools to fix issues labelled as 'good first issues' is forbidden". My whole Q1 searches llvm repos by that exact label, so every llvm result is off-limits for an AI-assisted workflow. Q1 is mostly dead weight as written.
- 2026-10-07, Maintainer alive and Response speed, tt-metal and circt and cccl: Staff at Tenstorrent, LLVM, and NVIDIA show up as CONTRIBUTOR, not MEMBER (private org membership, probably). The OWNER/MEMBER/COLLABORATOR wording found zero maintainers in tt-metal's sample even though staff replied within an hour. Maintainer alive still passed through commits, but Response speed came out unclear on tt-metal#40699 and fail on circt#3662 on a technicality.
- 2026-10-07, Response speed, cccl#750 and #10093: The sample had issues opened minutes earlier with no reply yet. One grader left them out and one counted them, and the rubric doesn't say which. "Most" also isn't defined, so 2 of 4 went to fail.
- 2026-10-07, Nobody else already on it, cccl#10093: The feature already shipped in merged PR #10847, but that PR never said "Closes #10093", so the issue's still open. No check catches finished work. It only got rejected because an old claim was still inside 90 days. Around 2026-10-21 that claim ages out and this issue would pass.
- 2026-10-07, Nobody else already on it, circt#3662: Someone posted a finished patch as a comment instead of a PR. The check names claim comments and open PRs, and a patch in the thread is neither one exactly.

## Patches after scan 1 (2026-10-07)

Rubric:

- AI-contribution policy allows this: Widened the evidence to AI policy files in docs/ and .github/ plus whatever the README or PR template links, and made a ban scoped to the issue's label count as a fail. Responds to the circt#3662 line. This tightens the check. It doesn't loosen it.
- Nobody else already on it: Also fails when the work is already done, either a merged PR that delivers it or a finished patch in the thread. Responds to the cccl#10093 and circt#3662 lines.
- Added a Who counts as a maintainer line: an OWNER/MEMBER/COLLABORATOR association, or someone who authored one of the recent default-branch commits. Maintainer alive, Response speed, and Friendly-issue signal use it. Responds to the CONTRIBUTOR-badge line. It's a misread fix, since the staff were real and replying.
- Response speed: Leave out sampled issues younger than 14 days, and "most" now means more than half. Responds to the cccl sample line.

Strategy:

- Q1: Took out llvm-project, CIRCT, and torch-mlir because LLVM's AI policy forbids AI on good-first-issue issues. I'm not adding a different LLVM query to get around that.
- Filter 6: Changed the tie-break from newest to oldest `updatedAt`. Responds to the line about fresh claims floating to the top.

Do the scan 1 verdicts flip? No. All five stay reject. cccl#10093 now also fails for the merged PR #10847. circt#3662 fails the AI check under the plain reading now, not just a judgment call. The maintainer change only moves preferred grades: Response speed on tt-metal#40699 would go from unclear to pass, which can't change a verdict.

Regression check (2026-10-07): Re-ran the unit-1 eval harness with the patched rubric and the issue-scout SKILL.md. It scored 18/20 and passed the bar, missing the same two items (issue-15, issue-19) as my original unit-1 run. The patches didn't break anything the sandbox tests.

## Scan 2 (2026-10-07)

- 2026-10-07, ranking, before grading: Scan 2's top four were the same four scan 1 rejected. Ranking is free and has no memory, so I'd have paid to regrade claimed issues. Added filter 3 (drop anything rejected in the last 30 days, using scan-output.md).
- 2026-10-07, all five verdicts: Five more rejects, ten out of ten across both scans. Nine of the ten failed Nobody else already on it. The vendor and compiler repos only have a handful of good-first-issue issues, and strangers grab them within days.
- 2026-10-07, AI-contribution policy allows this, iree#20213: IREE's contributing page says "We adopt the LLVM AI Tool Use Policy" and lists four conditions. The good-first-issue ban only shows up on the linked LLVM page. My check names policy files and README links, but doesn't say to follow a policy a repo adopts by reference.
- 2026-10-07, AI-contribution policy allows this, iree#23210: Another grader found the same ban in a github-actions bot comment on a newcomer's PR ("AI tool usage for resolutions to such issues is forbidden"). It isn't in CONTRIBUTING.md or the docs. So IREE's 🌱 issues are off-limits for me, the same as LLVM's.
- 2026-10-07, Who counts as a maintainer, cccl#5405 and tt-metal#20852: The last-50-commits fallback is too short on busy repos. cccl's last 50 commits cover a few days, so NVIDIA staff who replied within a day (nanan-nvidia, elstehle) didn't count, and Response speed failed. This only touches preferred grades.
- 2026-10-07, Nobody else already on it, cccl#7297: Two open PRs, one stale for 7 months. The check doesn't separate a stale open PR from a live one. The fresh PR decided it here.
- 2026-10-07, Nobody else already on it and Scope fits a newcomer, tt-metal#20852 and cccl#5405: Both issues changed shape after they were opened (narrowed or reopened). The graders had to decide whether to grade the original body or the latest maintainer comment. Both picked the latest, which seems right, but the rubric doesn't say.
- 2026-10-07, Q3: 25 untouched survivors in llama.cpp, SGLang, and vLLM sat below the cut both times, because tier order puts every Q2 and Q1 survivor first, even claimed ones.

## Patches after scan 2 (2026-10-07)

- Strategy, Q1b: Took out IREE's 🌱 query. IREE adopts LLVM's AI policy, so its good first issues are off-limits for my workflow. Responds to the iree#20213 and iree#23210 lines.
- Rubric, AI-contribution policy allows this: The evidence now covers a policy the repo adopts by reference and bot notices on a newcomer's PR. Responds to the same two lines. This tightens the check.
- Do the scan 2 verdicts flip? No. All five stay reject, and both IREE issues already failed this check.

## Scan 3 (2026-10-07)

- 2026-10-07, Q4: Passing the search terms as one quoted string ("cuda OR kernel OR inference OR gpu") returned 0 results on Windows. Unquoted works. `kernel` also pulled in OS-kernel and game-engine repos (FreeCAD, UZDoom), so I swapped it for `rocm`.
- 2026-10-07, ranking: The tier reorder did what I wanted. All five slots went to Q3 (sglang, llama.cpp, vllm), which never got graded in scans 1 and 2. Q4's on-target finds (HipKittens, cuda-quantum, Mooncake) sat below Q3, so they never got graded.
- 2026-10-07, all five verdicts: Five more rejects, 15 of 15 across three scans. All five failed Nobody else already on it. The inference repos are even more crowded than the vendor repos. sglang#28808 has four open PRs and eight total attempts, and llama.cpp#4574 has four open PRs.
- 2026-10-07, ranking filter 7 (fewer comments first): A claim is a comment, so even a 2-comment issue can be claimed (sglang#28808). The comment count is the only free signal for claims, but it's weak.
- 2026-10-07, Nobody else already on it, sglang#28808 and vllm#23957: Open PRs that have sat 1.5 to 3.5 months with no review still fail the check. Maintainers clearly aren't merging these, but the check can't tell a stale PR from a live one. I'm leaving it strict, since a newcomer PR would land in the same pile.
- 2026-10-07, Scope fits a newcomer, llama.cpp#4574: The issue never calls itself an umbrella, but it's worked like one for 2.5 years. The grader went by the history, which seems right.
- 2026-10-07, Who counts as a maintainer, sglang and vllm: vLLM merges about 50 commits in a few hours, so the last-50 fallback still misses staff. One grader only checked badges and skipped the commit list. Both only affect Response speed, which is a preferred check.
- 2026-10-07, AI-contribution policy allows this: llama.cpp ("AI-generated code is allowed. You are 100% responsible for every line") and vLLM ("Pure code-agent PRs are not allowed") set conditions, and sglang says nothing. All three are fine for my workflow as long as I follow the conditions.

What I take from three scans: My rubric's rejects are right every time, but the label `good first issue` in big GPU and inference repos gets claimed within days. Iterating the strategy fixed each scan's own friction (repeats, AI-banned repos, Q3 never graded), but it can't create unclaimed issues.
