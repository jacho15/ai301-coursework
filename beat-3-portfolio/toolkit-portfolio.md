# Toolkit Portfolio

**Student:** Jacob Cho

## Featured Tools

The tools I'll be featuring are issue-scout, pr-precheck with the ship-gate addition, and the PR-monitor skills. The reason I'm featuring these three skills is because all of them changed because something went wrong. The issue-scout skill got fixed after every scan. The pr-precheck with the ship-gate caught real problems on my pyhf PR. The PR monitor playbook came from my pyhf's merge history.

**issue-scout**

**What it is, and the judgment hole I wrote:** The issue-scout searches GitHub for first-contribution issues, ranks them without using API credits, and then grades the top few selected issues against the rubric which were written in `rubric.md` and `search-strategy.md`. The strategy has queries for GPU, compiler, and inference repos since those are my main interests. The rubric has some required checks such as "Nobody else already on it" and "AI-contribution policy allows this." The policy row immediately stops the skill on anything that has an outright AI ban or no AI tools on GFIs when tackling a GFI.

**How it evolved, dated:**
- 2026-10-07: Built the skill based on the issue-select skill from unit 1 and it rejected all 5 issues it looked for. Made some changes to the rubric since CIRCT's AI policy bans AI on good first issue work, but my check only failed "an outright AI ban", so it only failed that issue on a strict reading. I made the check read policy files in `docs/` and `.github/` and fail a ban that covers the issue's label. I also took llvm-project, CIRCT, and torch-mlir out of Q1.
- 2026-10-07: cccl#10093 had already shipped in a merged PR that never said "Closes". I made "Nobody else already on it" fail finished work too.
- 2026-10-07: Scan 2 ranked the same four issues scan 1 had just rejected, so I added a filter that drops anything rejected in the last 30 days. IREE adopts the LLVM policy by reference, so I made the policy check follow adopted policies and bot notices, and dropped IREE's query.
- 2026-10-07: My tie-break put the newest `updatedAt` first. A fresh claim comment bumps that date, so the filter was ranking the exact thing the rubric rejects. I switched it to oldest first.
- 2026-10-14: I replaced "Scope fits a newcomer" with a scope-feasible row and a difficulty note. The sandbox issues were tidy and the wild ones aren't.

**Evidence:** From my scan notes on 2026-10-07 (iree#23210): "Another grader found the same ban in a github-actions bot comment on a newcomer's PR ("AI tool usage for resolutions to such issues is forbidden"). It isn't in CONTRIBUTING.md or the docs." The old check never looked at bot comments. The new one does.

After three scans, 15 of 15 graded issues were rejects. Nine of the first ten failed "Nobody else already on it". I re-ran the Unit 1 eval after the patches and it still scored 18/20 (bar 18/20), with the same two misses as before (issue-15 and issue-19). Commit `30b6c02` (2026-10-07) holds the skill and the scans.

**pr-precheck and the ship-gate**

**What it is, and the judgment hole I wrote:** pr-precheck grades a PR package: the branch diff, my plan, my test evidence, and the PR description. The ship-gate is a hook that runs before `gh pr create`. It runs the commands in my `ship-manifest.md` and then runs pr-precheck. The parts I wrote are the precheck rubric and the manifest. One rubric check is "Test evidence re-runs the plan's test plan". It passes "if each repro from the repro evidence is run again on the changed code with a before and after you can see". My pyhf manifest has three must-pass rows (ruff check, ruff format, and the tests my change touches) and dated exclusions for checks I can't run on Windows.

**How it evolved, dated:**

- 2026-10-04: pkg-05 was a clear accept, but my rubric rejected it on the test evidence check. A same-key case in the test plan only said "Same-key redefine prints the one-time warning", and the grader read it as a repro with no run shown. It was a new-behavior case, not a repro. I changed the check so only repros from the repro evidence need a before and after. Everything else just needs a name and a result. The eval ended at 19/20.
- 2026-10-22: I installed the gate and wrote the pyhf manifest. The first run failed my test row with 19 errors. The cause was file order. `test_init.py` ran before `test_pdf.py`, and unmodified main gives the same errors in that order. I moved `test_init.py` last and wrote the reason in the manifest. One edit didn't save, so a second run used the old order. I only caught it because the gate printed the old command.
- 2026-10-22: The third run passed all three repo checks and then stopped. My CLI had hit its spend limit, so pr-precheck never ran. I ran it by hand in a desktop session instead. It rejected the package once because my test evidence didn't show the new test failing on main. I added that run and it accepted.
- 2026-11-07: The CLI works again, so the gate's pr-precheck step ran on the branch for the first time.

**Evidence:** The gate log from 2026-11-07 15:41 on `perf/2649-lazy-scipy-imports`:

```
- Diff stays inside the plan [pass]
- Plan delivered and description truthful [fail]: Description table says `pyhf fit -<TAB>` is about 1.1 s on the PR, but test_evidence.md shows median 611 ms; ...
- Test evidence re-runs the plan's test plan [pass]
- Diff is free of debris [pass]
- Repo's stated asks are met [fail]: CONTRIBUTING.md step 7 asks to add your name to docs/contributors.rst, and the diff does not touch that file; ...
```

I checked both. My test evidence shows `option (pyhf fit -<TAB>)  median 611 ms`, and the PR #2779 description says about 1.1 s. `CONTRIBUTING.md` step 7 does say "Make sure that you've added your name to `docs/contributors.rst`". The live PR description matches my local draft, so the same problems are on the PR. I opened that PR on 2026-10-23 without a gate pass, so this is what the gate would have said before I did.

**PR monitor**

**What it is, and the judgment hole I wrote:** The monitor reads my PR on GitHub (its checks, reviews, comments, and how long it's been quiet) and asks Claude to draft my next move into a file. It never posts anything. The part I wrote is `playbook.md`. It has four sections: response rules, staleness thresholds, nudge etiquette, and walk-away criteria. One rule I can quote: "Bot comments and my own comments don't count as activity."

**How it evolved, dated:**

- 2026-10-28: I wrote the playbook from the last 80 merged PRs in pyhf. Maintainers merge their own PRs the same day. Outside PRs wait much longer. The one outside PR that merged after a wait took 47 days, and two open ones had been quiet for 6 and 9 days. So I set 21 days of quiet before a first nudge, 14 days after a maintainer reply, one nudge ever, and a walk-away at 45 days of silence after that nudge.
- 2026-11-07: The playbook text is the same as on 2026-10-28. What changed is that I could finally run the monitor. The CLI was logged out on 2026-10-28, so the full run drafted nothing.

This tool barely changed, and the reason is that I haven't had a maintainer reply to answer yet.

**Evidence:** On 2026-10-28 the free `--state` check said "feedback-in: review feedback is in". The only other comment on the PR is CodeRabbit's bot summary, so that label was wrong. The full run couldn't draft anything. On 2026-11-07 the full run drafted this (from `drafted-move.md`):

```
MOVE: Jacob, nothing to answer yet, so this is a wait note and not a reply

Wait note (not for posting): No human has reviewed PR #2779. The only other comment is CodeRabbit's summary, which says "No actionable comments were generated" and found no bug. Post nothing. Next check: 2026-11-13.
```

It still got the label wrong, but it quoted my bot-comment rule and reached the right move. The first nudge on PR #2779 is possible on 2026-11-13 under my own rule, and only if I have something new to report.

## Inventory

- **repro-check:** Grades a claim comment and repro report before I post. Scored 20/20 on its eval on 2026-09-19. My one change was to "Steps are followable", so an honest can't-reproduce report passes. I swapped it to the wild scope on 2026-10-14.
- **plan-check:** Grades a plan and its plan comment before I build. Scored 20/20 on 2026-09-24. I narrowed "Unknowns stated honestly" so a plan that says "no other risks beyond X" doesn't fail for it.
- **voice-guard:** A hook that checks every `gh` comment or PR body I post through Claude Code against my voice guide and its five upstream rules. It passed my OpenVINO claim on 2026-10-14. It never saw the pyhf PR, because I opened that one from the browser.
- **issue-select:** The Unit 1 version of the scout. It became issue-scout (above).

## The Arc

**Beat 1**
Date: 2026-10-07
Friction: The scout's first three scans rejected all 15 issues. Most already had a claim or a PR, and some repos banned AI on their good first issues, which I only found by luck.
Change: I patched the rubric to follow adopted policies and to fail finished work. I changed the strategy to skip banned repos and anything I'd already rejected.
Result: The eval still scored 18/20 after the patches. The scout still never found me a free issue. I took pyhf #2649 from the course issue site instead.

**Beat 2**
Date: 2026-10-14
Friction: OpenVINO bars AI-written communication. I needed something to check what I post against my own voice before it goes out.
Change: I installed the voice-guard hook, merged my three voice guides into one, and wrote five upstream rules for claims, questions, and pings.
Result: The wiring test stopped `gh issue comment --help` as it should. My OpenVINO claim passed the guard and posted at 17:13 that day.

**Beat 3**
Date: 2026-10-22
Friction: The ship-gate blocked my pyhf branch on 19 test errors. They came from the order of the test files, and main gives the same errors in that order.
Change: I put `test_init.py` last in the manifest and wrote the reason there. I excluded the checks I can't run on Windows, each with a date.
Result: The third run passed all three repo checks. Then my CLI hit its spend limit and pr-precheck never ran. I opened PR #2779 from the browser on 2026-10-23 without a gate pass.

**Beat 4**
Date: 2026-10-28
Friction: My voice guide says not to ping until the usual reply time has passed, but I had no number for how long pyhf takes.
Change: I installed the PR monitor and wrote my playbook from pyhf's last 80 merged PRs, with a 21-day first nudge.
Result: The `--state` check called the PR "feedback-in" because of a bot comment. The full run couldn't draft anything because the CLI was logged out. I posted nothing.

**Beat 5**
Date: 2026-11-07
Friction: PR #2779 had been open 15 days with no human reply, and the gate had never judged it.
Change: I logged the CLI back in, ran the monitor, and ran the gate with its pr-precheck step.
Result: The monitor drafted a wait note until 2026-11-13. The gate rejected the PR on two checks, a 1.1 s timing in the description that my evidence shows as 611 ms, and a missing contributors.rst entry.

## Limitations and What's Next

My toolkit checks my work. It doesn't find me work or make a maintainer answer. The scout couldn't find a free issue in four scans, and the PR monitor can only tell me to wait. The gate is the weakest part of my own term. It depends on one logged-in account with credits. When that failed I shipped around it, and the gate later found two problems in a PR that was already open.

Next I'd fix the PR description and add my name to `docs/contributors.rst`. After that I'd make the gate fail loudly, so I can't open a PR without a pass. I'd also teach the scout to look at issues that don't have a good first issue label, since the OpenVINO issue I found by hand never showed up in a scan.

**Tool limits.**

issue-scout: It only finds issues labeled for newcomers, so it missed an unlabeled OpenVINO bug I found by hand. It also can't tell a stale claim or PR from a live one, so a three-month-old open PR still fails an issue.
pr-precheck and the ship-gate: It only judges the evidence I write, and it trusts a named command's result, so a made-up "passes" gets through. It needs a working Claude login, and when that broke I could open a PR with no gate pass at all.
PR monitor: Its `--state` check labels a bot comment as review feedback. It only drafts, and it can't tell me whether the maintainers are slow or gone.
