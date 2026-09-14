# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69

**Verdict output**

```
Ranked live-mode grading of 3 candidates from codepath/pathreview-ai301-fa26-s1:

1. #69: Output parser crashes on a top-level JSON array fallback (rag/generator/output_parser.py)
  - closest fit: it's code that actually touches some AI/ML scaffolding (RAG/LLM-output-handling code), instead of just backend code
2. #72: verify_password raises UnknownHashError on malformed stored hashes (core/security.py)
  - a real fail-closed-vs-fail-open bug, but it is still mostly backend work
3. #61: Health check DB probe fails under SQLAlchemy 2.x (api/routes/health.py)
  - just a simple API-version fix

The reason that all of these issues were selected/made it past the criteria was because they were marked as "good first issue, tier-1" bugs, had zero people working on them as well as zero comments and zero PRs. There was also obviously no AI-contribution policy stated anywhere (README, .github/, PR template) so it made it past all the checks.

[
  {"item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69",
   "checks": [
     {"name": "Maintainer alive", "grade": "pass", "evidence": "human commits by Andrew Burke within the last 30 days"},
     {"name": "Repo in use", "grade": "pass", "evidence": "not archived, last push 2026-09-10, 4 days before today"},
     {"name": "Nobody else already on it", "grade": "pass", "evidence": "no assignee, 0 comments, 0 PRs anywhere in the repo"},
     {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "one named bug, one file, manifest id H-02, 2-4h estimate"},
     {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "no AI policy anywhere in README/.github/PR template"}
   ], "verdict": "accept"},
  {"item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
   "checks": [
     {"name": "Maintainer alive", "grade": "pass", "evidence": "same repo-level evidence"},
     {"name": "Repo in use", "grade": "pass", "evidence": "same repo-level evidence"},
     {"name": "Nobody else already on it", "grade": "pass", "evidence": "no assignee, 0 comments, 0 PRs"},
     {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "one named bug, one file, manifest id H-05, 1-2h estimate"},
     {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "no AI policy stated"}
   ], "verdict": "accept"},
  {"item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/61",
   "checks": [
     {"name": "Maintainer alive", "grade": "pass", "evidence": "same repo-level evidence"},
     {"name": "Repo in use", "grade": "pass", "evidence": "same repo-level evidence"},
     {"name": "Nobody else already on it", "grade": "pass", "evidence": "no assignee, 0 comments, 0 PRs"},
     {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "one named bug, one file, exact error message given"},
     {"name": "AI-contribution policy allows this", "grade": "pass", "evidence": "no AI policy stated"}
   ], "verdict": "accept"}
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. `--limit 3` smoke test: `agreement: 2/3 scored items`
2. `--only issue-01,issue-20` (after fixing the scope-check wording): `agreement: 2/2 scored items`
3. `--only issue-05,issue-08,issue-09,issue-12,issue-14,issue-17`: `agreement: 6/6 scored items`
4. Full confirming run (`--save-run eval-run.txt`): `agreement: 18/20 scored items (bar: 18/20: PASS)`

**Issue analysis**

`issue-19`: golden file `accept` vs. mine `reject`
- It's a maintainer-diagnosed UI-freeze bug listing two root causes plus three "additional suggestions." My scope check reads that numbered structure as umbrella-shaped even though it's one bug with several possible causes for the same fix.

**Check rationale**

Quoting `rubric.md` verbatim, "Scope fits a newcomer":

> Fail on an umbrella that invites many contributors to split the work into separate PRs, an unsettled design debate, a support question, a maintainer saying it needs core-internal changes, or a feature request where the opener admits the concrete shape is still undetermined ("TBD", "not identified yet"). A fully-specified deliverable for one contributor in one PR passes even across several files or with no maintainer reply yet, as does a plain bug report with a clear fix location or a list of similar small fixes sharing one pattern.

An earlier version's last clause was just "any feature idea with no maintainer-approved spec," which falsely rejected issue-01 (a fully-specified, zero-comment docs task), so I narrowed it to "the opener admits the shape is undetermined" to fix that without reopening issue-20.

**Trade-offs**

That fix left issue-19 unresolved; I re-ran `--only issue-01,issue-20` as a canary before tightening the umbrella clause further and chose not to, since issue-01's multi-part structure sits close enough to the same pattern that a stricter rule risked re-breaking it, so I accepted issue-19's miss instead.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Fit: 
- The reason I chose issue #69 was that it was the only AI/ML-adjacent issue (that was evaluated at least) rather than generic backend work. Given my interests, I figured that working on this type of issue could be a good learning experience as I have never really worked with this kind of thing before. Also, it was marked as a GFI and also didn't seem like it would take too long.
2. What the rubric caught vs. what I weighed:
- One thing I confirmed is that issue #69 was unclaimed with my own eyes (the agent was having trouble) as well as being marked with a GFI. I also checked to make sure that there was no AI policy and that it was scoped to one file with a pre-written failing test. The rubric caught most of these, but it also helped me decide between issue #69 and #34 because it noted that issue #34 was not a GFI so I chose issue #69 instead.
3. Anticipated difficulty
- I think that the anticipated difficulty is pretty low, since the fix is pre-specified with a failing test already written and I just have to check all my fixes against that test.

---

Related paths: `eval-run.txt` in this directory; your skill's files in `tools/issue-select/`.
