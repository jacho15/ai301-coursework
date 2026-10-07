# Search strategy: where your scout looks, and why

<!--
THIS IS THE PART YOU WRITE. The scout in SKILL.md executes whatever
queries and filters you define here. It ships empty on purpose: the
strategy is your judgment about where YOUR first contribution lives,
and a scan without authored queries is just someone else's defaults.

A filled strategy must contain:

1. At least one query in the Queries section. Each query is a real
   `gh search issues` invocation, and each should trace to a sentence
   of your fit profile in scope.md: if you cannot say which sentence
   produced a query, the query is probably not yours. Search breadth
   is the point at this stage: prefer generous limits and let the
   ranking filters do the narrowing.

2. At least one ranking filter in the Ranking filters section. A
   filter is a condition or an ordering over fields the search
   results already carry (last activity date, assignee presence,
   label set, comment count, repo). It must be checkable from the
   result fields alone: if deciding it would need opening the issue
   page, it belongs in your rubric, not here. Ranking is the free
   stage; keep it free. Make at least one filter an ordering, or
   state your tie-break: with drop conditions alone, the scout takes
   the top of whatever order the searches happened to return, and
   the graded candidates stop being traceable to you.

3. The top-N line, kept or deliberately changed.
-->

## Queries

<!-- Real gh search invocations, one per line, each with a comment
naming the fit-profile sentence it came from. Example SHAPE (write
your own; these values belong to nobody):

gh search issues --label "good first issue" --language python --state open --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url
-->

Repos don't agree on a label name. Most use `good first issue`, but Tenstorrent uses `good-first-issue`, TVM uses `beginner-friendly`, and IREE uses `good first issue 🌱` (dropped, see Q1). Q2b and Q1b pick those up. On Windows, put a label with spaces in `--label`, not in the query text, or gh mangles the quotes.

Q2, vendor GPU and accelerator stacks. From "The companies I'm most interested in are NVIDIA, AMD, Annapurna Labs (AWS), and Etched" and "CUDA and ROCm libraries ... accelerator software stacks". Etched has no public repos, so Tenstorrent stands in as the closest open AI-chip company.

```
gh search issues --label "good first issue" --repo NVIDIA/cccl --repo NVIDIA/cutlass --repo NVIDIA/TensorRT-LLM --repo ROCm/composable_kernel --repo ROCm/HIP --repo aws-neuron/nki-samples --repo tenstorrent/tt-metal --repo tenstorrent/tt-mlir --state open --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url
```

Q2b, same repos, the other label names. Same profile sentences as Q2.

```
gh search issues --repo ROCm/HIP --repo tenstorrent/tt-metal --repo tenstorrent/tt-mlir --state open --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url -- "label:good-first-issue,difficulty:A_Easy"
```

Q1, AI compilers. From "AI compilers like MLIR, Triton, and IREE" and "I'd rather take an issue in a kernel, compiler pass, runtime, or performance path". I took out llvm-project, CIRCT, and torch-mlir after scan 1. LLVM's AI tool policy forbids using AI tools on issues labeled good first issue, and that label is the only thing this query searches for. I'm not going to search LLVM some other way just to get around that. After scan 2 I took IREE out too. Its contributing page adopts the LLVM AI Tool Use Policy, and its bot tells newcomers AI use on good first issues is forbidden.

```
gh search issues --label "good first issue" --repo openxla/xla --repo triton-lang/triton --state open --sort updated --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url
```

Q1b, compiler repos with their own label names. Same profile sentences as Q1.

```
gh search issues --label "beginner-friendly" --repo apache/tvm --state open --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url
```

Q3, inference runtimes. From "I want issues close to model inference and performance. Stuff like profiling, latency optimization, kernels, and efficient deployment" and "Python is fine when it's inference or kernel work".

```
gh search issues --label "good first issue" --repo ggml-org/llama.cpp --repo microsoft/onnxruntime --repo openvinotoolkit/openvino --repo vllm-project/vllm --repo sgl-project/sglang --state open --sort updated --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url
```

Q4, broad GPU and inference search across all of GitHub. From "CUDA and ROCm libraries" and "I want issues close to model inference and performance". Added after scan 2: the named repos only have a few good first issues each and strangers claim them fast, so this looks for smaller repos in the same area. The search terms go in unquoted. Passing them as one quoted string returns nothing on Windows.

```
gh search issues cuda OR gpu OR inference OR rocm --language "C++" --label "good first issue" --state open --sort updated --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url
```

Not searched: GCC. It tracks bugs in its own Bugzilla and takes patches over a mailing list, so there's no GitHub issue or PR page for the assignment to link. Clang is also out, since it lives in llvm-project (see Q1).

## Ranking filters

<!-- Conditions and orderings over the free result fields, applied in
the order written. State each so a stranger could apply it and get
your ordering. Example SHAPES (write your own):

- drop any result with an assignee
- drop any result not updated in the last 60 days
- prefer fewer comments over more
-->

Apply these in order.

1. Drop any result with one or more assignees.
2. Drop any result whose `updatedAt` is more than 60 days before the scan date.
3. Drop any result whose `url` was graded reject in a scan from the last 30 days (the JSON blocks in `scan-output.md`). Scan 2's top four were the same four scan 1 rejected for fresh claims, and a claim doesn't go away in a day.
4. Drop any result with a docs, CI, or packaging label. Split each label name on spaces, `-`, `_`, `:`, and `/`, and drop the result if any piece (case-insensitive) is exactly `doc`, `docs`, `documentation`, `ci`, `infra`, `build`, or `packaging`. This comes from "I'd rather take an issue in a kernel, compiler pass, runtime, or performance path than docs, CI, or packaging."
5. Drop any result from the `llvm` or `iree-org` orgs. They forbid AI tools on good first issues, and Q4 can pull them back in.
6. Order by query tier: Q3 first, then Q2 and Q2b, then Q4, then Q1 and Q1b. If a result shows up in more than one query, it takes its best tier. Before scan 3 the order was Q2, Q1, Q3, which matched how much I care about the companies, but two scans showed the Q2 and Q1 good first issues get claimed within days. Q3's repos still fit my inference and performance sentence and had 25 unclaimed survivors that never got graded.
7. Within a tier, put fewer `commentsCount` first. A short thread usually means nobody's claimed it and there's no long design debate.
8. Tie-break by oldest `updatedAt` first (still inside the 60-day window from filter 2). In scan 1 the newest updates were mostly fresh claim comments, so a quiet thread is the better bet.
9. Cap at 2 results per repo in the top N. When a repo hits the cap, skip its next results and keep walking down the list. Without this, one big repo can fill all five slots.

## How many to grade

Grade the top **5** ranked results per scan.

<!-- Five is the default because grading is the only stage that costs
money: about $0.20 per candidate, so a scan is about $1, and you can
iterate the strategy several times for less than one full regression
run. You need one good issue, not ten. Raising this number is
allowed, but it is a decision you state here in a sentence, with the
cost you are accepting; it is not a number you bump because a scan
disappointed you once. -->
