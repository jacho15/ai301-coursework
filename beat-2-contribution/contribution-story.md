# Contribution: Improve speed of Click autocompletions (pyhf #2649)

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Jacob Cho
**GitHub Username:** jacho15
**Issue:** https://github.com/scikit-hep/pyhf/issues/2649
**Pull Request:** https://github.com/scikit-hep/pyhf/pull/2779

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

**Unit 7: Installed the ship-gate and wrote my first manifest**

2026-10-22: I installed ship-gate which runs the manifest checks and then my own pr-precheck before any `gh pr create` goes out. The install swapped pr-precheck to the real-world scope and kept the old one as scope.md.sandbox. The wiring test stopped `gh pr create --help` twice, once from the voice-guard and once from the gate. My manifest has one row that runs, the copyright header check from OpenVINO's CI. I have no Visual Studio or CMake here, so I excluded the build, the C++ tests, and clang-format with a date and that reason. I excluded the PR commit check too, since it needs a PR number and a token. My first real gate run stopped because I was on master with no fix branch. My old issue looks claimed by someone else, so I need a new one before the gate can grade anything.

Later the same day I ran the gate on my pyhf branch. The first run stopped on my manifest's test row with 19 minuit errors. They came from the order of the test files. `test_init.py` ran before `test_pdf.py`, and on unmodified main that order gives the same 11 errors. I put `test_init.py` last and wrote the reason in the manifest. One of my edits to the manifest did not save, so a second run used the old order. I only noticed because the gate printed the old command. The third run passed all three repo checks (ruff lint, ruff format, and the tests my change touches, 138 s). Then it stopped before my pr-precheck could run. The claude CLI said I had hit my individual spend limit. So the gate has no pr-precheck verdict on this branch yet. That spend limit is on the CodePath account that my `claude` command line tool is logged into, not on my personal account. Since I could not run the gate's rubric step, I ran my pr-precheck by hand in my desktop session. It rejected my package the first time. My plan said the new test must fail on main and pass on the branch, but my test evidence only showed it passing. I added the run on main and graded again, and it accepted. This is a manual pass. It does not count as a gate pass. Because I could not get a gate pass, I forked, pushed, and opened the pull request myself from the browser (pull request #2779, 2026-10-23). I shipped around my own gate. I am writing that down here instead of leaving it out.

**Unit 8: Installed the PR-monitor, wrote my playbook, and waited**

2026-10-28: I installed the PR-monitor and wrote my playbook from pyhf's own merge history. Maintainers merge their own PRs the same day, but outside contributors wait much longer. The one outside PR that got merged after a wait took 47 days, and two outside PRs are open at 6 and 9 days with no review. So I set 21 days of quiet before a first nudge, 14 days after a maintainer reply, one nudge ever, and 45 days of silence after that nudge before I walk away. The free `--state` check read my PR as open, 5 days old, mergeable but behind main, review required, checks passing, and it called the state feedback-in. That was wrong. The only other comment is CodeRabbit's bot summary. The full run could not draft anything because the `claude` CLI said it was not logged in, so I have no drafted move. I did not post anything or send a nudge. My own rule says the first nudge is possible on 2026-11-13, so the move is to wait.

---

## Why I Chose This Issue

I picked this issue because I like making stuff run faster, and there were no signs that someone was on this issue (comments or PRs) when I picked it. The repo itself is close to ML and data tooling which is something I'm realatively interested in. I actually started with an OpenVINO bug, but I deleted my claim after I was told I should pick from the issue site. I also spent a lot of time on a Pytorch bug but reproducing it on my GPU would've taken hours that I did not have.

**Toolkit**

- Tool: The course issue site, read through Claude in Chrome, plus `gh` to check each candidate on GitHub. My issue-scout skill was not used for this pick.
- What it produced: A list of 2,323 Python issues, a filter for repos in data and ML, and four unclaimed pyhf issues with no comments and no linked pull request.
- Difficulties: The site shows labels, not activity. Almost every issue I checked in Dask, Hugging Face datasets, Airflow, Ray and cuDF already had a pull request from its own reporter or a thread of people asking to take it. The site page text is long, so I loaded the data through the page and filtered it there.
- What changed: I stopped relying on labels and checked comments and linked pull requests for every candidate before picking. A cheap check of linked pull requests would be a good addition to my scout.

---

## Understanding the Issue

**Problem Description**

Every time someone presses Tab to complete a `pyhf` command, the shell runs the `pyhf` program again. On my laptop that takes about 3 seconds each time. The issue asks to restructure how Click is used so completions are fast.

**Expected Behavior**

Tab completion for `pyhf` feels instant, or at least fast.

**Current Behavior**

Each completion takes about 3.0 s. The time is the same for `pyhf <TAB>`, `pyhf fit -<TAB>` and `pyhf patchset <TAB>`, so it is not about which command is completed.

**Affected Components**

Not Click, as the issue guessed. The slow part is `import pyhf`. Any `pyhf.*` import runs `pyhf/__init__.py` first, which imports the tensor backends and optimizers. In that import, SciPy is the big cost. The files involved are `src/pyhf/tensor/numpy_backend.py`, `src/pyhf/infer/intervals/upper_limits.py`, and the optimizer files `src/pyhf/optimize/opt_scipy.py` and `opt_minuit.py`.

**Toolkit**

- Tool: `python -X importtime`, a small benchmark script I wrote that runs the real completion command 7 times, and Claude Code to read the code.
- What it produced: The profile showed `import pyhf.cli` takes about 2.8 s, with scipy.stats about 1.1 s, scipy.special about 0.6 s and scipy.optimize about 0.3 s. That moved the problem from Click to imports.
- Difficulties: The import-time output is noisy and the first run is slower because Python compiles files. The first benchmark script also failed on a relative path on Windows.
- What changed: I used the median of 7 runs from the real command, and I fixed the script to use an absolute path.

---

## Reproduction Process

**Environment Setup**

Windows 11, Python 3.14.7, click 8.5.0, numpy 2.5.4, SciPy 1.18.1. I made a shallow clone of `scikit-hep/pyhf` (main at commit 8b8c3e6), made a `.venv`, and installed with `pip install -e .`.

Challenges: The shallow clone has no git tags, so the version tool failed to read a version. I set `SETUPTOOLS_SCM_PRETEND_VERSION=0.8.0` to get past it. pytest would not start until I installed `iminuit`, because `pyproject.toml` imports it in a warning filter. `src/conftest.py` is a symlink that Windows checked out as a text file, so ruff and the doctests fail on it. Also 19 in-process CLI tests in `tests/test_scripts.py` fail on main on Windows, because `shlex` strips backslashes. The repo's own Windows CI ignores that file.

**Steps to Reproduce**

1. Install pyhf in a venv: `pip install -e .`
2. Run one completion by hand: `_PYHF_COMPLETE=bash_complete COMP_WORDS="pyhf " COMP_CWORD=1 pyhf`. On Windows I set those variables from Python and ran `pyhf.exe`.
3. Time it. It takes about 3.0 s and prints the 14 subcommands.
4. Run `python -X importtime -c "import pyhf.cli"` to see where the time goes.

**Reproduction Evidence**

- **Commit showing reproduction:** There is no commit for the reproduction, since it is a measurement. My fix is commit https://github.com/jacho15/pyhf/commit/6b586cdf647aeba8789d77f2e2a18aab3a80e152 on the branch `perf/2649-lazy-scipy-imports` in my fork.
- **Screenshots/logs:** On main, the median of 7 runs: `pyhf <TAB>` 3109 ms, `pyhf fit -<TAB>` 3108 ms, `pyhf patchset <TAB>` 3103 ms. Import time for `pyhf.cli`: about 2.8 s, of which `pyhf.tensor.manager` is 2.3 s (SciPy inside the numpy backend), `pyhf.pdf` 0.23 s, `pyhf.infer` 0.12 s.
- **My findings:** The issue guesses that Click needs restructuring, but the time is in the package import. Click's part is small (about 0.04 s). No restructuring of Click can fix this, because the `pyhf` package import runs first.

**Toolkit**

- Tool: Claude Code ran the clone, the install and the benchmark. I did not use my repro-check skill on this issue.
- What it produced: The numbers above, and the three-case benchmark script that I reuse for the before and after comparison.
- Difficulties: Windows problems: the version tool, the symlink, relative paths for the launcher, and tests that write stray files named like `UsersjacobAppData...` into the repo root when they fail.
- What changed: I moved the stray files out of the repo after each test run and kept the clone's `git status` clean. I wrote the Windows setup steps into my `CLAUDE.local.md` for this repo.

---

## Solution Approach

**Analysis**

pyhf's console script is `pyhf.cli:cli`. Python must import the `pyhf` package before `pyhf.cli`, and `pyhf/__init__.py` imports the numpy backend, which imports `scipy.stats`, `scipy.special` and others at the top of the file. Upper limits import `scipy.optimize.toms748` at the top too. Nothing in a completion needs any of these.

**Proposed Solution**

Import SciPy where it is used, inside the functions, so `import pyhf` stays cheap. I am deliberately NOT changing `pyhf/__init__.py`, the public API, the jax, torch and tensorflow backends, or the jsonschema import (about 0.16 s, used in many places). Making `pyhf/__init__.py` lazy would help more but changes import behavior for every user, so that is the maintainers' call. I will offer it as a follow up.

**Implementation Plan**

1. `numpy_backend.py`: move `scipy.stats` and `scipy.special` imports into the methods that use them.
2. `upper_limits.py`: import `toms748` inside `toms748_scan`.
3. `opt_scipy.py` and `opt_minuit.py`: import `scipy.optimize` explicitly.
4. Add a test that `import pyhf.cli` does not load `scipy.optimize`, `scipy.special` or `scipy.stats`.

Deviations, in the order they happened:

- I made `scipy.special` lazy as well. It was not in my first list, but the profile showed it costs about 0.6 s.
- The review found `tests/test_init.py::test_missing_optimizer[scipy]` failed when run alone. It read `sys.modules["scipy"]`, which only existed because something else had imported SciPy. I made it import the module first.
- The review also showed why `opt_minuit.py` needed `import scipy.optimize`. The old bare `import scipy` only worked because the numpy backend had imported `scipy.stats` already.
- I removed a check for bare `scipy` from the new test, so it does not break if a future dependency imports scipy.
- A cost I found: each lazy import adds about 1.3 microseconds to every call of the numpy backend functions. I accepted it and say so in the pull request.

**Toolkit**

- Tool: Claude Code with an `executor` subagent to write the change and a `reviewer` subagent to check it. My plan-check skill was not used for this plan.
- What it produced: A four-file change plus tests, and a review with one real finding (the `test_init.py` test) and a few notes.
- Difficulties: The executor said the failing test lists were identical before and after. I checked, and its baseline comparison was not reliable the first two times I tried it myself, because an export of main was missing the generated version file and the test data. I redid it in a proper checkout.
- What changed: I wrote the plan down in `plan.md` with the deviations, and I now compare tests against a full checkout of main, not an export.

---

## Testing Strategy

I measured the actual user problem, then ran the tests, then checked the cost of the change.

- **Before and after, the real completion command, median of 7 runs:** main takes about 3.1 s for all three cases. The branch takes about 1.1 s. After the change `import pyhf.cli` loads no SciPy modules at all.
- **A test that fails on main and passes on the branch:** `tests/test_scripts.py::test_cli_import_does_not_load_scipy`. I ran it on both. On main it fails and prints the SciPy modules it found loaded.
- **The repo's own tests:** I ran `tests/test_tensor.py`, `test_scripts.py`, `test_infer.py`, `test_pdf.py` and `test_init.py` without the jax, pytorch and tensorflow backends. The branch has 21 failures and 213 passes. Main has 23 failures and 210 passes. Every failure on the branch also fails on main: 19 Windows path tests and 2 jax tests. The 2 extra failures on main are `test_patchset_download` tests that fetch from hepdata.net. They passed on main in an earlier run, so I treat them as flaky.
- **By hand:** a fit with both the scipy and minuit optimizers, `toms748_scan` for an upper limit, poisson and normal sampling, `erf` and `erfinv`.
- **The cost:** `poisson_logpdf` goes from 5.1 to 6.5 microseconds for one element, 8.4 to 9.7 for 100, and 215 to 223 for 5000.
- **Not run:** the jax, pytorch and tensorflow backends, `tests/test_optim.py` and `tests/test_validation.py` (they need those packages), the doctests (the symlink problem), mypy, and the lowest-SciPy CI job.

**Toolkit**

- Tool: The benchmark script, `pytest` against a full checkout of main as a baseline, `ruff`, and the ship-gate (see the Unit 7 entry above).
- What it produced: The before and after table, a new test that really catches the problem, and a comparison of failure lists. Ruff check and format pass on all six changed files.
- Difficulties: A baseline in a copy of main failed to import until I copied the generated version file. The first comparison also showed 23 failures on main and 21 on the branch. I looked into the 2 extra and they were network tests.
- What changed: I wrote the extra network tests into my test evidence and the PR text as flaky. I did not claim the lists were identical.

---

## Implementation Notes

**2026-10-22**

I cloned pyhf, set up a venv, and measured. One completion took 3.1 s. Profiling showed SciPy imports dominate. I wrote the approach (lazy SciPy imports) and had an executor implement it on the branch `perf/2649-lazy-scipy-imports`.

**2026-10-22**

The executor's version cut a completion to about 1.2 s. I checked it myself instead of trusting the report. I moved the `toms748` import to the top of its function, made the optimizers import `scipy.optimize` explicitly, and loosened the new test. A reviewer then found that `test_missing_optimizer[scipy]` failed when run alone. I fixed it.

**2026-10-22**

Committed locally as `perf: Lazily import SciPy to speed up CLI shell completions`. I wrote the pull request text, `plan.md`, `test_evidence.md` and a ship manifest in the clone, kept out of the diff. The branch was not pushed yet at that point.

**2026-10-23**

I forked pyhf, pushed the branch to my fork, and opened pull request #2779 from the browser. The gate could not run its rubric step on my account, so I shipped without a gate pass. I wrote what the manual pr-precheck found in the Unit 7 entry.

**Toolkit**

- Tool: Claude Code, with an `executor` for edits and a `reviewer` for the diff. I told the executor exactly what to change and what not to touch.
- What it produced: The change, a review, and my own checks.
- Difficulties: The executor's report had two gaps. It left `opt_scipy` and `opt_minuit` depending on SciPy submodule loading, and its comparison with main was not valid.
- What changed: I fixed both myself and wrote the real comparison.

---

## Pull Request

**PR Link:** https://github.com/scikit-hep/pyhf/pull/2779 (branch `perf/2649-lazy-scipy-imports` in my fork)

**PR Description:** Title: `perf: Lazily import SciPy to speed up CLI shell completions`. The description follows pyhf's template. It says what the issue found (SciPy imports, about 2.8 s of the 3.0 s), what the PR changes (lazy imports in four files, plus two test changes), the before and after measurements (about 3.0 s to about 1.1 s), the cost (about 1.3 microseconds per call to the numpy backend functions), what I tested and what I could not run, and an AI disclosure. It also offers to look at making `pyhf/__init__.py` lazy as a follow up.

**Maintainer Feedback:**

- 2026-10-23: none yet. The pull request opened on 2026-10-23 (06:24 UTC). The checks that ran so far passed: the PR title check, pre-commit.ci and CodeFactor. The main CI workflows (CI/CD, Lint, Docs, CodeQL) say `action_required`, which I think means a maintainer has to approve them for a first-time contributor. CodeRabbit, a bot, posted a summary.
- 2026-10-28: still none from a human. Five days after opening, the pull request has no reviews and no comments except CodeRabbit's summary and my own. GitHub says review is required. The checks that ran are passing (7 passing, 1 cancelled). The branch is mergeable but behind main. pyhf's other outside pull requests have waited 6 to 9 days with no review too, so this is normal quiet for the repo.

**Status:** Awaiting review as of 2026-10-28. The pull request is open and not a draft. I have not nudged anyone. My playbook allows the first nudge on 2026-11-13.

**Toolkit**

- Tool: The ship-gate wrapping my pr-precheck and a manifest I wrote for pyhf.
- What it produced: Three runs on my pyhf branch. Two blocked on the manifest's test row (the same 11 minuit errors that main has when the test files run in that order). The third passed all three repo checks and then stopped before pr-precheck, because the claude CLI said I had hit my individual spend limit. I have no gate verdict from pr-precheck. A manual run of pr-precheck in my desktop session rejected the package once (my test evidence did not show the new test failing on main), then accepted it after I added that run.
- Difficulties: The gate's checks run in `cmd.exe` on Windows, so the manifest rows use Windows paths. The full test file cannot be a must-pass row, since 19 of its tests fail on main on Windows. The order of test files mattered, and I only learned that from a gate block. The rubric pass needs the claude CLI, and my account hit its spend limit, so the gate stays shut until I can run it.
- What changed: The manifest has three must-pass rows (ruff check, ruff format, and the tests the change touches, with `test_init.py` last and the reason written in the source column) and dated exclusions for the rest. I opened the pull request from the browser anyway, because the gate's rubric step could not run on the CodePath account. So the gate did not pass before I shipped. The manual pr-precheck pass was my substitute, and it is not the same thing. I should rerun the gate once the `claude` command line tool is on an account with credits.
- Tool (2026-10-28): The PR-monitor and my playbook, run from my pyhf clone on the PR branch.
- What it produced: The free `--state` read, which printed the PR's checks, review decision, mergeability, and quiet days. The full run produced no draft.
- Difficulties: On Windows the first `--state` run crashed with a `UnicodeDecodeError`, because Python read `gh`'s output as cp1252 and the CodeRabbit comment has characters that are not in it. Setting `PYTHONUTF8=1` fixed it without editing the monitor. The monitor also called the state feedback-in because CodeRabbit's bot comment is newer than my last commit, so it would have drafted a review response to a bot. Last, the full run stopped because the `claude` CLI said it was not logged in, the same CLI that hit the spend limit in unit 7.
- What changed: I set my own thresholds from pyhf's merge history (21 days for a first nudge). I wrote "bots are not reviews" into my playbook's response rules. I would change the monitor to ignore bot authors when it decides what counts as feedback. I did not draft or send a nudge by hand, because my own rule says to wait until 2026-11-13.

---

## Learnings and Reflections

**Technical Skills Gained**

How to read `python -X importtime` output and tell import cost from runtime cost. How shell completion works in Click 8 (`_PYHF_COMPLETE=bash_complete`). Why a console script imports its whole package first. How function-level imports trade startup time for a small cost on each call, and how to measure that cost. How a bare `import scipy` plus `scipy.optimize.minimize` depends on side effects from other imports.

**Challenges Overcome**

The hard part was finding a free issue. I went through three picks (OpenVINO, PyTorch, pyhf) before one fit my time. Checking linked pull requests for every candidate, not just labels, is what finally worked. The second was trusting numbers. I re-measured the executor's results and found the failure-list comparison was wrong the first two times.

**What I'd Do Differently Next Time**

Check linked pull requests and reporter intent before reading a candidate in detail. Pick the target before building tooling for it. I spent hours on a CUDA build route before I asked how long a test would take.

---

## Resources Used

- pyhf issue #2649, "Improve speed of Click autocompletions": https://github.com/scikit-hep/pyhf/issues/2649
- pyhf pull request #2639, which added Click's native shell completion: https://github.com/scikit-hep/pyhf/pull/2639
- pyhf CONTRIBUTING.md and the pull request template, for the branch, title and description rules
- `python -X importtime`, the Python option that prints import times, which found the SciPy cost
- Click 8.5.0's `_PYHF_COMPLETE=bash_complete` mechanism, which I used to time one real completion
