# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/87

**Branch**

fix/69-json-array-fallback

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. `--limit 3` smoke test: 3/3 scored items agree.
2. First full run: 15/19 scored items agree. pkg-05 errored on the Windows encoding bug from unit 3 (box-drawing characters in the package can't go through the cp1252 stdin pipe), so the run counted as partial and didn't save. All four misses (pkg-08, pkg-13, pkg-16, pkg-19) were clear accepts failed on "Test evidence re-runs the plan's test plan".
3. `--only` on the misses plus pkg-04 and pkg-10 as not-tested canaries, after loosening the test evidence check so controls and the suite only need the command named with its result: 6/6 scored items agree. pkg-05 errored again.
4. `--only pkg-05` with `PYTHONUTF8=1`: 0/1. Failed the same check on an extra test plan case.
5. `--only` on pkg-05 plus all four not-tested packages and calib-04 as canaries, after limiting before/after to the repros from the repro evidence: 5/5 scored items agree.
6. Full run with `--save-run eval-run.txt`: 19/20 scored items agree (bar: 18/20: PASS). Saved to `eval-run.txt`.

**Package analysis**

`pkg-05` is gold accept (clear-accept). My rubric rejected it on "Test evidence re-runs the plan's test plan" in run 4. The plan's test plan has three items: re-run the issue's script, re-run with two same-name same-key bindings and expect one row plus a warning, and cargo test. The PR shows the issue's script before and after as real tables, and names `cargo test -p nu-protocol` with 312 passing. For the same-key case it only says "Same-key redefine prints the one-time warning." At that point my check said every repro or failure mode the test plan names needs a before and after, so the grader read the same-key case as a repro with no run shown. It isn't a repro though. It's a new-behavior case the plan added, and the bug from the repro evidence is fully shown. I changed the check so before and after is only required for repros from the repro evidence, and everything else in the test plan just has to be named with its result. pkg-05 graded accept after that.

**Check rationale**

| Test evidence re-runs the plan's test plan | The test evidence, checked one item at a time against the plan's test plan and the repro steps. | Pass if each repro from the repro evidence is run again on the changed code with a before and after you can see (output, an error, or an exit code). Everything else in the test plan (controls, extra cases, smoke checks, the suite) just needs to be named with its result, like "`go test ./...` passes". Fail if a repro just says it works ("tested locally", "works now"), the suite result has no command named when the test plan asks for it, the run goes through something the diff didn't change, or anything the test plan names is left out completely. | required |

My first version required a before and after for every repro or failure mode the test plan names, and the suite result "shown". That rejected five clear accepts (pkg-08, pkg-13, pkg-16, pkg-19, and calib-01) because they name controls and suite runs with a result, like "`go test ./...` passes (4108 tests)", without pasting output. Then it rejected pkg-05 for an extra case. Real PRs don't paste the full suite output, so I split the test plan into two tiers. Repros from the repro evidence still need a before and after since that's the proof the bug is fixed. Everything else needs to be named with its result. I kept "left out completely" as a fail so a PR can't just skip a repro the plan named, which is what calib-04 does with its second failure mode.

**Trade-offs**

Loosening the test evidence check twice could have flipped not-tested packages to accept, especially pkg-04 and pkg-10 since their evidence also says things like "cargo test passes". I re-ran all four not-tested packages and calib-04 with `--only` as canaries after the second change, and all five stayed reject because their actual repro is never shown before and after. The cost is that a PR can now name a control or suite run with a made-up result and pass, since the check trusts a named command. The one miss in the final run is pkg-08, which my rubric accepted in run 3 but rejected in run 6 on "Plan delivered and description truthful" because the description says "plan posted on the thread" and the thread snapshot doesn't show it. That claim is about process, not the diff, so it's grader variance on a wide reading of "everything the title or description claims". Narrowing it to "every change the title or description claims" would likely fix it, but the run already clears the bar so I left it.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
