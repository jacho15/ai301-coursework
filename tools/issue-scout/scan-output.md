# Scan outputs

## Scan 1 (2026-10-07)

Scan 1: 6 queries, 273 unique results. Ranking dropped 140 for assignees, 63 as stale (more than 60 days), and 2 for docs/CI labels, leaving 68 survivors. Graded the top 5. Accepted: 0. Rejected: 5.

**Accepted:** none.

**Rejected:**

1. tenstorrent/tt-metal#40699, "[DM] Remove non-posted semaphore NOC functions". Surfaced by Q2. Ranked #1: tier 1, 2 comments, updated 2026-10-01. Sunk by **Nobody else already on it**: alexxony on 2026-09-26, "I'd like to work on this if it's still wanted", unanswered.
2. tenstorrent/tt-metal#42916, "[QSR] Assert on unused parameters once runtime asserts are added". Surfaced by Q2. Ranked #2: tier 1, 2 comments, updated 2026-09-25. Sunk by **Nobody else already on it**: alexxony on 2026-09-25, "I'd like to take this one", unanswered.
3. NVIDIA/cccl#750, "Check for issues with -0 / +0 stable_sort issues". Surfaced by Q2. Ranked #3: tier 1, 3 comments, updated 2026-10-06. Sunk by **Nobody else already on it**: open PR #11897 from 2026-10-06 says "Fixes #750".
4. NVIDIA/cccl#10093, "[FEA]: Debugger pretty-printers: `cuda::std::optional`". Surfaced by Q2. Ranked #4: tier 1, 3 comments, updated 2026-08-11. Sunk by **Nobody else already on it**: unanswered claim from aminehd on 2026-07-23. Merged PR #10847 already shipped the feature, and the issue was never closed.
5. llvm/circt#3662, "[Comb] ICmp folds missing for CEQ/CNE/WEQ/WNE". Surfaced by Q1. Ranked #5: tier 2, 1 comment, updated 2026-09-05. The tier-1 picks below it in the list were skipped by the 2-per-repo cap. Sunk by **Nobody else already on it** (Deagle2 posted a patch on 2026-09-05, unanswered) and **AI-contribution policy allows this** (docs/AIToolPolicy.md: "Using AI tools to fix 'good first issue' labeled issues" is not allowed).

```json
[
  {
    "item": "https://github.com/tenstorrent/tt-metal/issues/40699",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "Human commits on 2026-10-07 (e.g. amahmudTT, '[LLK][BH+WH] Make mailbox_read wait...'), well within 120 days."},
      {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-10-07T17:58:20Z."},
      {"name": "Nobody else already on it", "grade": "fail", "evidence": "alexxony (NONE) on 2026-09-26: 'I'd like to work on this if it's still wanted', followed up 2026-10-01 'Happy to take step (1)'; unanswered, not marked stale, within 90 days. Prior PR #42823 closed unmerged."},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Opener's 'How' gives a concrete 3-step plan (deprecate 30 days, remove non-posted APIs, reuse counter for posted atomics); no umbrella, debate, support question, core-internals warning, or TBD shape stated."},
      {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "CONTRIBUTING.md allows AI-assisted code 'provided they personally review, understand, and take responsibility'; only bans automated/AI claims of bug bounties (not a bounty issue)."},
      {"name": "Response speed", "grade": "unclear", "evidence": "8-issue sample had no OWNER/MEMBER/COLLABORATOR replies (staff show as CONTRIBUTOR); staff-looking replies came in ~1h, ~20h, ~9d."},
      {"name": "Friendly-issue signal", "grade": "pass", "evidence": "'good first issue' label added by rtawfik01 on 2026-03-25; opener association CONTRIBUTOR."}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/tenstorrent/tt-metal/issues/42916",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "Human commits on main today (2026-10-07), e.g. amahmudTT '[LLK][BH+WH] Make mailbox_read wait...' (#59202); sampled outside issues #59616/#59561 got replies within hours."},
      {"name": "Repo in use", "grade": "pass", "evidence": "archived=false, pushed_at 2026-10-07T17:58:20Z."},
      {"name": "Nobody else already on it", "grade": "fail", "evidence": "alexxony (NONE) 2026-09-25: 'Hi @rtawfik01, I'd like to take this one...' is 12 days old, unanswered, not marked stale; no assignees or linked PRs."},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single pattern (add LLK asserts that unsupported features aren't passed in older Quasar LLK compute APIs); rtawfik01: 'we have been doing this for the new LLK kernels but ... not ... the older LLK kernels for Quasar'."},
      {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "CONTRIBUTING.md allows AI-assisted development 'provided they personally review, understand, and take responsibility for all submissions'; only automated/AI claiming of bug-bounty issues is banned."},
      {"name": "Response speed", "grade": "pass", "evidence": "First-response sample: #59616 reply after ~1h, #59561 ~16h after opening (by CONTRIBUTOR-associated TT staff); all well under 14 days."},
      {"name": "Friendly-issue signal", "grade": "pass", "evidence": "'good first issue' label added by rtawfik01 on 2026-06-16 (opener gdsinghTT is CONTRIBUTOR, not MEMBER)."}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/NVIDIA/cccl/issues/750",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "5 human commits on main on 2026-10-07 (bernhardmgruber, davebayer); MEMBER replies in first-response sample"},
      {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-10-07T17:50:45Z"},
      {"name": "Nobody else already on it", "grade": "fail", "evidence": "Open PR #11897 'Keep -0.0 and +0.0 in order in Thrust's CPU stable_sort' by UnknownHacker1 (2026-10-06) says 'Fixes #750', following their unanswered claim comment the same day"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Body is a 3-item checklist for one deliverable: check other backends, document the guarantee, add regression tests; no design debate"},
      {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "docs/contributors/index.rst: 'We welcome the use of AI tools to assist in code authoring and code review' with a human-understanding condition"},
      {"name": "Response speed", "grade": "pass", "evidence": "Of 3 sampled issues with maintainer replies, 2 came within 14 days (2h, 1 day); 2 more were opened today with no reply yet"},
      {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Labeled 'good first issue'"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/NVIDIA/cccl/issues/10093",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "5 human commits on 2026-10-07 (bernhardmgruber, davebayer); MEMBER jrhemstad replied to #5661 within ~1 day"},
      {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-10-07T17:50:45Z; release v3.5.0 on 2026-10-07"},
      {"name": "Nobody else already on it", "grade": "fail", "evidence": "aminehd (NONE) 2026-07-23, 76 days ago: 'Hi, I would like to work on this...', no reply and not marked stale; also merged PR #10847 (2026-08-18) already shipped optional.py"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single specified deliverable: optional.py under libcudacxx/share/libcudacxx/<debugger>/ plus tests under libcudacxx/test/debugging/optional"},
      {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "docs/contributors/index.rst: 'We welcome the use of AI tools to assist in code authoring and code review.'"},
      {"name": "Response speed", "grade": "fail", "evidence": "2 of 4 sampled issues with a maintainer reply answered within 14 days (#4974 ~2h, #5661 ~1d; #10799/#10800 ~55d)"},
      {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Labels 'good first issue' and 'help wanted'; opener Jacobfaib is CONTRIBUTOR"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/llvm/circt/issues/3662",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "Human commits today: okekayode '[HW] Remove generic InOut port direction support (#11232)' 2026-10-07; SimonEbner 2026-10-07."},
      {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-10-07T17:05:03Z."},
      {"name": "Nobody else already on it", "grade": "fail", "evidence": "Deagle2 (NONE) 2026-09-05, 32 days ago, unanswered: 'I've written a fix for this... Attaching a patch since I haven't set up a PR yet.' No assignee, no linked PR."},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Bounded fold fix with named locations: 'applyCmpPredicate, applyCmpPredicateToEqualOperands, and ICmpOp::canonicalize' in CombFolds.cpp."},
      {"name": "AI-contribution policy allows this", "grade": "fail", "evidence": "docs/AIToolPolicy.md 'Not Allowed: Using AI tools to fix \"good first issue\" labeled issues'; this issue carries the good first issue label."},
      {"name": "Response speed", "grade": "fail", "evidence": "Only 1 of 5 sampled recent issues got an OWNER/MEMBER/COLLABORATOR reply (#9302, about 10 months); maintainers in this org show as CONTRIBUTOR."},
      {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Labeled 'good first issue' by fabianschuiki at creation, 2022-08-04."}
    ],
    "verdict": "reject"
  }
]
```

## Scan 2 (2026-10-07)

Scan 2: same 6 queries after the scan 1 patches (llvm repos out, oldest-first tie-break), 173 unique results. Ranking dropped 82 for assignees, 53 as stale, 2 for docs/CI labels, and 4 as scan 1 rejects (new filter 3), leaving 32 survivors. Graded the top 5. Accepted: 0. Rejected: 5.

**Accepted:** none.

**Rejected:**

1. NVIDIA/cccl#5405, "[FEA]: Headers that don't support NVRTC should emit diagnostic". Surfaced by Q2. Ranked #1: tier 1, 6 comments, updated 2026-08-07. Sunk by **Nobody else already on it**: open PR #10715 "addresses the Thrust portion of #5405", which is the part the maintainer reopened the issue for.
2. NVIDIA/cccl#7297, "[FEA]: Thrust vector's should provide `emplace_back(Args...) -> T&`". Surfaced by Q2. Ranked #2: tier 1, 6 comments, updated 2026-09-24. Sunk by **Nobody else already on it** (open PRs #11727 and #7981) and **Scope fits a newcomer** (miscco: "Are we really sure we want this?", never settled).
3. tenstorrent/tt-metal#20852, "[Blackhole] SFPABS + integer overflow". Surfaced by Q2b. Ranked #3: tier 1, 10 comments, updated 2026-08-28. The cccl result above it was skipped by the 2-per-repo cap. Sunk by **Nobody else already on it** (open PR #56045) and **Scope fits a newcomer** graded unclear (opener: "only open to investigate the other ops").
4. iree-org/iree#23210, "Suboptimal lowering for matmul-like ops on gfx1100". Surfaced by Q1b. Ranked #4: tier 2, 3 comments, updated 2026-08-27. Sunk by **Nobody else already on it** (open PR #24884 "Part of #23210"), **Scope fits a newcomer** (two competing approaches floated), and **AI-contribution policy allows this** (IREE bot notice: AI use on good first issue issues "is forbidden").
5. iree-org/iree#20213, "[Codegen] Port AMDGPU device lib implementations to MLIR rewrites". Surfaced by Q1b. Ranked #5: tier 2, 4 comments, updated 2026-09-02. Sunk by **Nobody else already on it** (merged PR #20598 already delivered it) and **AI-contribution policy allows this** (IREE adopts the LLVM AI Tool Use Policy, which forbids AI on good first issues).

```json
[
  {"item": "https://github.com/NVIDIA/cccl/issues/5405", "checks": [
    {"name": "Maintainer alive", "grade": "pass", "evidence": "Latest main commit 2026-10-07 (today); bernhardmgruber has 12 of last 50 commits; COLLABORATOR jrhemstad commented on the thread 2026-07-30."},
    {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-10-07T17:59:26Z."},
    {"name": "Nobody else already on it", "grade": "fail", "evidence": "Open linked PR #10715 by SamJSui (2026-08-07, under review 2026-09-08) 'addresses the Thrust portion of #5405', which is exactly the reopened ask; thread: 'Submitted for the Thrust headers'."},
    {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Maintainer-specified pattern ('#error with an informative diagnostic when it detects compilation with NVRTC') applied to Thrust headers: similar small fixes sharing one pattern."},
    {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "docs/contributors/index.rst: 'We welcome the use of AI tools to assist in code authoring and code review' with an understanding condition, no ban."},
    {"name": "Response speed", "grade": "fail", "evidence": "1 of 5 sampled issues (#5661) got a reply within 14 days from someone the rubric counts as a maintainer; #10798/#10799/#10800 first maintainer reply after 55 days; #4974 only the opener's own comment early."},
    {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Opened by jrhemstad (COLLABORATOR); labeled 'good first issue'."}
  ], "verdict": "reject"},
  {"item": "https://github.com/NVIDIA/cccl/issues/7297", "checks": [
    {"name": "Maintainer alive", "grade": "pass", "evidence": "bernhardmgruber (last-50 commit author, issue opener) committed to main 2026-10-07 and replied in-thread 2026-02-21."},
    {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-10-07T17:59:26Z."},
    {"name": "Nobody else already on it", "grade": "fail", "evidence": "Open cross-referenced PR #11727 '[Thrust]: Implement vector::emplace_back' by rbourgeois33 (updated 2026-10-02), plus open stale PR #7981 by viralbhadeshiya."},
    {"name": "Scope fits a newcomer", "grade": "fail", "evidence": "Maintainer miscco: 'Are we really sure we want this? ... allows people to use a massively inefficient API'; opener: 'I see your point though.' Never settled."},
    {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "docs/contributors/index.rst: 'We welcome the use of AI tools to assist in code authoring and code review' (condition: maintainers must understand the change)."},
    {"name": "Response speed", "grade": "fail", "evidence": "2 of 4 eligible sampled issues (#4974, #5661) got a maintainer reply within 14 days; #10799/#10800 first maintainer reply came after 55 days."},
    {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Labels 'good first issue', 'help wanted'; opener bernhardmgruber is a recent commit author."}
  ], "verdict": "reject"},
  {"item": "https://github.com/tenstorrent/tt-metal/issues/20852", "checks": [
    {"name": "Maintainer alive", "grade": "pass", "evidence": "Newest default-branch commit 2026-10-07; last 50 commits by ~34 human authors (e.g. jasondavies, ijankowskiTT)."},
    {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-10-07T18:12:42Z."},
    {"name": "Nobody else already on it", "grade": "fail", "evidence": "Open PR #56045 by truongsontung ('fix(bh): clamp INT32_MIN before SFPABS...', 'Reported in #20852') cross-referenced 2026-09-10, under active staff review through 2026-09-30."},
    {"name": "Scope fits a newcomer", "grade": "unclear", "evidence": "Opener 2026-05-12: 'This issue is only open to investigate the other ops: SFPGT, LE & CAST' - remaining ask is an open-ended Blackhole HW investigation plus docs, no clear fix location."},
    {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "CONTRIBUTING.md bans AI only for claiming bug bounties; allows AI-assisted code 'provided they personally review, understand, and take responsibility'."},
    {"name": "Response speed", "grade": "fail", "evidence": "Sample #56664/#55767/#56710/#56798/#57205: only #56664 got a non-opener reply (8 days, nmilicevicTT, not a recent committer); rest are opener self-replies."},
    {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Labeled 'good-first-issue' (added 2026-01-05); opener rtawfik01 is CONTRIBUTOR, not in last 50 commits."}
  ], "verdict": "reject"},
  {"item": "https://github.com/iree-org/iree/issues/23210", "checks": [
    {"name": "Maintainer alive", "grade": "pass", "evidence": "kuhar (recent committer) committed 2026-10-07; opener efric (MEMBER) commented on the thread 2026-04-29."},
    {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-10-07T16:30:15Z."},
    {"name": "Nobody else already on it", "grade": "fail", "evidence": "Open PR #24884 by ryannyui (opened 2026-09-06) says 'Part of #23210'; unanswered claim comment 2026-08-27."},
    {"name": "Scope fits a newcomer", "grade": "fail", "evidence": "Opener: 'it's likely we can select a better tiling configuration'; later 'we may be able to lower to dot product like strategies'; claimant expects 'a PR or several PRs'."},
    {"name": "AI-contribution policy allows this", "grade": "fail", "evidence": "IREE bot policy notice: issues labeled 'Good first issue' -- 'AI tool usage for resolutions to such issues is forbidden'; this issue has 'good first issue' label."},
    {"name": "Response speed", "grade": "fail", "evidence": "After excluding 4 issues under 14 days old, 1 of 2 sampled got a maintainer reply within 14 days (#24932 yes in 3 days, #24930 no)."},
    {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Opened by efric (MEMBER); labeled 'good first issue 🌱'."}
  ], "verdict": "reject"},
  {"item": "https://github.com/iree-org/iree/issues/20213", "checks": [
    {"name": "Maintainer alive", "grade": "pass", "evidence": "Human commits on 2026-10-07 by kuhar, rodburns, jschuhmacher, ziereis."},
    {"name": "Repo in use", "grade": "pass", "evidence": "archived=false, pushed_at 2026-10-07T16:30:15Z."},
    {"name": "Nobody else already on it", "grade": "fail", "evidence": "Cross-referenced PR #20598 by keshavvinayak01, same title, merged 2025-06-16, adds FastMathPatterns (erf) and hasFastExp in MathTransformPass; last comment asks 'Can this issue be closed?'"},
    {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Fully specified two-step task: port OCML math impls to MLIR rewrites and add a has_fast_exp option to MathTransformsPass."},
    {"name": "AI-contribution policy allows this", "grade": "fail", "evidence": "contributing.md: 'We adopt the LLVM AI Tool Use Policy'; LLVM policy: 'Using AI tools to fix issues labelled as good first issues is forbidden' and this issue is labeled 'good first issue 🌱'."},
    {"name": "Response speed", "grade": "pass", "evidence": "Only eligible sampled issue #24932 got a first reply in ~3 days from recent commit author egebeysel; the other 4 were opened <14 days ago and left out."},
    {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Labeled 'good first issue 🌱' (opener qedawkins is CONTRIBUTOR)."}
  ], "verdict": "reject"}
]
```

## Scan 3 (2026-10-07)

Scan 3: 7 queries (new broad Q4; tiers reordered to Q3, then Q2/Q2b, then Q4, then Q1/Q1b), 224 unique results. Ranking dropped 92 for assignees, 63 as stale, 3 for docs/CI labels, 7 as earlier rejects, and 0 from AI-banned orgs, leaving 59 survivors. Graded the top 5. Accepted: 0. Rejected: 5.

**Accepted:** none.

**Rejected:**

1. sgl-project/sglang#28808, "Refactor: TRTLLMHAAttnBackend should not inherit from FlashInferAttnBackend when reuse is small". Surfaced by Q3. Ranked #1: tier 1, 2 comments, updated 2026-09-30. Sunk by **Nobody else already on it**: four open PRs (#28820, #32948, #35219, #35913) plus an unanswered claim on 2026-09-30.
2. ggml-org/llama.cpp#4574, "llama : integer type consistency in `llama.h`". Surfaced by Q3. Ranked #2: tier 1, 4 comments, updated 2026-08-10. Sunk by **Nobody else already on it** (four open PRs) and **Scope fits a newcomer** (open-ended incremental ask, split across 8+ PRs, unanswered objection).
3. sgl-project/sglang#19612, "[Feature] Unified JIT / Precompilation Cache Directory". Surfaced by Q3. Ranked #3: tier 1, 4 comments, updated 2026-08-18. Sunk by **Nobody else already on it**: open PRs #33424 and #35621, and merged #32434 delivers most of it.
4. ggml-org/llama.cpp#17488, "GGUF convert support for Vibevoice". Surfaced by Q3. Ranked #4: tier 1, 6 comments, updated 2026-09-01. Two sglang results above it were skipped by the 2-per-repo cap. Sunk by **Nobody else already on it** (unanswered claim on 2026-09-01) and **Scope fits a newcomer** (needs a whole new MTMD model).
5. vllm-project/vllm#23957, "[Feature]: Support `Phi4Flash` model in V1". Surfaced by Q3. Ranked #5: tier 1, 9 comments, updated 2026-09-24. Sunk by **Nobody else already on it**: open PR #44963 plus an unanswered claim on 2026-09-22.

```json
[
  {"item": "https://github.com/sgl-project/sglang/issues/28808", "checks": [
    {"name": "Maintainer alive", "grade": "pass", "evidence": "Human commits on 2026-10-07 (niehen6174, mmangkad); opener merrymercy is among the last 50 commit authors."},
    {"name": "Repo in use", "grade": "pass", "evidence": "archived=false, pushed_at 2026-10-07T18:10:52Z."},
    {"name": "Nobody else already on it", "grade": "fail", "evidence": "Open cross-referenced PRs #28820, #32948 ('Fix #28808'), #35219, #35913, plus an unanswered claim comment by asp616848 on 2026-09-30."},
    {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Maintainer-written single refactor: 'well-scoped, localized to trtllm_mha_backend.py (plus the base classes)'."},
    {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "No AI rule in contribution_guide.mdx, docs/CONTRIBUTING.md, MAINTAINER.md, PR template or first-timer PR bot notices; silence."},
    {"name": "Response speed", "grade": "fail", "evidence": "1 of 5 sampled issues (#36711, Fridge003 COLLABORATOR in ~5h) got a maintainer reply within 14 days."},
    {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Opened by merrymercy (recent committer) and labeled 'good first issue'."}
  ], "verdict": "reject"},
  {"item": "https://github.com/ggml-org/llama.cpp/issues/4574", "checks": [
    {"name": "Maintainer alive", "grade": "pass", "evidence": "Latest default-branch commits by humans dated 2026-10-07 (am17an, aldehir, pwilkin); ggerganov (MEMBER) commented on the thread 2023-12-21."},
    {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-10-07T18:07:50Z."},
    {"name": "Nobody else already on it", "grade": "fail", "evidence": "Open cross-referenced PRs #22277, #22440, #25892, #27125 (draft); #4577 merged 2024-01-02 and #28631 merged 2026-09-09."},
    {"name": "Scope fits a newcomer", "grade": "fail", "evidence": "Open-ended incremental ask ('As code changes try to prefer signed integers... lower-impact slower changes'), roadmap-labeled, split across 8+ PRs, with an unanswered objection ('I don't agree with this issue as-written... need to be size_t')."},
    {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "CONTRIBUTING.md: 'AI-generated code is allowed. You are 100% responsible for every line'; only conditions (disclosure, manual review, explain every line, no AI-written PR text)."},
    {"name": "Response speed", "grade": "pass", "evidence": "2 of 3 eligible sampled issues got a maintainer reply within 14 days (#21547 CISC 1 day, #25129 ServeurpersoCom same day; #28734 none)."},
    {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Labeled 'good first issue' (opener MarcusDunn is CONTRIBUTOR, not a recent commit author)."}
  ], "verdict": "reject"},
  {"item": "https://github.com/sgl-project/sglang/issues/19612", "checks": [
    {"name": "Maintainer alive", "grade": "pass", "evidence": "Newest default-branch commit 2026-10-07 by ~37 human authors in last 50; COLLABORATOR opener whybeyoung replied 'just do it.' on 2026-03-01."},
    {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-10-07T18:10:52Z."},
    {"name": "Nobody else already on it", "grade": "fail", "evidence": "Open linked PRs #33424 'Fix #19612: Unified JIT and Precompilation Cache Directory' (2026-08-03) and #35621 (updated 2026-09-28); merged #32434 (2026-08-05) already consolidates Triton/Inductor/FlashInfer/CUDA/DeepGEMM caches under SGLANG_CACHE_DIR."},
    {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single fully-specified deliverable (one cache root env var plus a subdir table), collaborator-opened, 'good first issue' label, no design debate in thread."},
    {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "No AI rules in docs/CONTRIBUTING.md, developer_guide/contribution_guide.mdx or PR template; repo ships AGENTS.md and .claude/rules; no bot notice on a first-timer PR that disclosed AI-assisted revision (#35621)."},
    {"name": "Response speed", "grade": "fail", "evidence": "2 of 6 sampled issues older than 14 days got an OWNER/MEMBER/COLLABORATOR reply within 14 days (#17050, #40995); #41077, #41076, #41070, #41038 had none."},
    {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Opener author_association COLLABORATOR; labeled 'good first issue'."}
  ], "verdict": "reject"},
  {"item": "https://github.com/ggml-org/llama.cpp/issues/17488", "checks": [
    {"name": "Maintainer alive", "grade": "pass", "evidence": "Commits on 2026-10-07 (Terrencezzj, am17an); pwilkin [MEMBER] commented on the thread 2025-11-25."},
    {"name": "Repo in use", "grade": "pass", "evidence": "archived=false, pushed_at 2026-10-07T18:07:50Z."},
    {"name": "Nobody else already on it", "grade": "fail", "evidence": "LeonxLJX 2026-09-01 (36 days ago): 'I'd like to take this one ... I'll ... follow up with a PR' - unanswered, not marked stale."},
    {"name": "Scope fits a newcomer", "grade": "fail", "evidence": "Opener: 'Can anyone help me with that?' (support request); MEMBER: 'real VibeVoice support requires adding a proper MTMD model' - open-ended new architecture, not a specified one-PR deliverable."},
    {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "CONTRIBUTING.md: 'AI-generated code is allowed. You are 100% responsible for every line' - disclosure/review conditions only, no label-scoped ban."},
    {"name": "Response speed", "grade": "fail", "evidence": "2 of 5 eligible sampled issues (#21547, #25129) got a reply from a recent commit author within 14 days; #28734, #28090, #27638 did not."},
    {"name": "Friendly-issue signal", "grade": "pass", "evidence": "'good first issue' label added by pwilkin [MEMBER] 2025-11-25."}
  ], "verdict": "reject"},
  {"item": "https://github.com/vllm-project/vllm/issues/23957", "checks": [
    {"name": "Maintainer alive", "grade": "pass", "evidence": "50 human commits in the last day (latest 2026-10-07T18:04Z jinzhen-lin); opener tdoublep is MEMBER and committer robertgshaw2-redhat applied the labels."},
    {"name": "Repo in use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-10-07T18:04:44Z."},
    {"name": "Nobody else already on it", "grade": "fail", "evidence": "Open non-draft PR #44963 'fix: [Feature]: Support Phi4Flash model in V1' (cross-referenced 2026-06-09, +1131 lines), plus unanswered claim by AmanBhattShorthillsAI on 2026-09-22."},
    {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "MEMBER-opened single deliverable: port the custom Mamba layer (MambaMixer2 as reference) and the differential attention backend to V1; not an umbrella, no design debate, no core-internals warning."},
    {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "AGENTS.md: 'Pure code-agent PRs are not allowed. A human submitter must understand and defend the change'; plus disclosure and Co-authored-by trailer rules. Conditions, not a ban."},
    {"name": "Response speed", "grade": "fail", "evidence": "0 of 5 sampled issues older than 14 days (#57149, #55600, #47172, #54961, #53286) got a first reply within 14 days from an OWNER/MEMBER/COLLABORATOR or recent committer."},
    {"name": "Friendly-issue signal", "grade": "pass", "evidence": "Opened by tdoublep (MEMBER); labeled 'good first issue'."}
  ], "verdict": "reject"}
]
```
