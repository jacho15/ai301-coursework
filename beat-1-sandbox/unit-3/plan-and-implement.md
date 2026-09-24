# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

jacho15

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69#issuecomment-5822692848

I reproduced the crash (report above): `parse_review_output` hands a parsed JSON array straight to `_parse_json_output`, which calls `.items()` on it and raises `AttributeError: 'list' object has no attribute 'items'` at output_parser.py:68.

Plan: guard both `json.loads` call sites in `parse_review_output` with an `isinstance(data, dict)` check, so a non-dict value falls through to the existing plaintext fallback instead of reaching `_parse_json_output`. That's the fallback path the issue asks for, and it reuses the graceful handling already in place for a JSONDecodeError. Then I'll remove the `xfail` marker on `test_json_array_fallback` in tests/unit/test_output_parser.py, since it should pass for real once this lands.

Nothing outside those two call sites and that one test marker. I'll report back once it's built and tested.

---

## Your branch

**Branch**

fix/69-json-array-fallback

**Evidence**

Before (checked out at the commit prior to the fix, f89c06f):

```
$ python3 -c "
import json
from rag.generator.output_parser import parse_review_output
raw = json.dumps(['First feedback item', 'Second feedback item'])
result = parse_review_output(raw)
print(result)
"
Traceback (most recent call last):
  File "<string>", line 5, in <module>
    result = parse_review_output(raw)
  File "rag/generator/output_parser.py", line 48, in parse_review_output
    return _parse_json_output(data)
  File "rag/generator/output_parser.py", line 68, in _parse_json_output
    for key, value in data.items():
                      ^^^^^^^^^^
AttributeError: 'list' object has no attribute 'items'

$ python3 -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -v
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback XFAIL [100%]
1 xfailed in 0.28s
```

After (on fix/69-json-array-fallback, commit 70d247c):

```
$ python3 -c "
import json
from rag.generator.output_parser import parse_review_output
raw = json.dumps(['First feedback item', 'Second feedback item'])
result = parse_review_output(raw)
print(result)
"
[FeedbackSection(section_name='general_feedback', content='["First feedback item", "Second feedback item"]', confidence=0.7, suggestions=[])]

$ python3 -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -v
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback PASSED [100%]
1 passed in 0.14s

$ python3 -m pytest tests/unit/test_output_parser.py -v
... 19 passed in 0.20s
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. `--limit 3` smoke test: 2/2 scored items agree (pkg-01 reject/reject, pkg-03 accept/accept). `pkg-02` errored on a Windows subprocess encoding bug in the harness's `subprocess.run(text=True)` call (falls back to cp1252 instead of UTF-8), unrelated to the rubric.
2. `--only pkg-02` with `PYTHONUTF8=1` (workaround for the encoding bug, forces Python's UTF-8 mode so the subprocess pipe doesn't hit cp1252): 1/1 agree.
3. First full run: 19/20 scored items agree; category floor holds (clear-accept 6/7, every other category full). Sole miss: `pkg-05`, failed "Unknowns stated honestly."
4. `--only pkg-05` (after loosening "Unknowns stated honestly" from "claims certainty on a point it has not verified" to "claims the fix will work without having tested it"): 1/1 agree.
5. Full run with `--save-run eval-run.txt`: 20/20 scored items agree (bar: 18/20: PASS). Saved to `eval-run.txt`.

**Package analysis**

`pkg-05` is gold `clear-accept` (accept). My rubric first graded it `reject` on "Unknowns stated honestly," because that check's pass condition originally read "Fail if the plan claims certainty on a point it has not verified," and the grading model read the plan's line "Risk: none identified beyond one extra network request per channel per 24h" as an unverified certainty claim. pkg-05's plan is a well-grounded, thread-aware fix (adding a max cache age using a constant the thread already agreed on) that honestly names its one real risk and says there are no others — that's ordinary honest engineering writing, not overconfidence. Penalizing "no other risks beyond X" duplicated a failure mode ("claims the fix works without testing it") the check was never meant to catch. I reworded the pass condition to target that specific claim and re-ran `pkg-05` to confirm it now grades `accept`.

**Check rationale**

| Unknowns stated honestly | Plan's risks/unknowns section. | Pass if the plan names its actual unknowns and risks in plain language. Fail if the plan claims the fix will work without having tested it, or leaves out a risk the diagnosis or scope clearly carries. | required |

I revised this from an earlier version that failed a plan for confidently stating "no other risks beyond X" (see Package analysis above), which conflated stating there are no further risks with claiming untested certainty. I rejected dropping the check to `preferred` instead, since honesty about unknowns is exactly the failure family the lecture named (unknowns dressed up as certainty), and it's the check backing the required disclosure of real risk; I only narrowed what counts as the violation, not whether the check gates the verdict.

**Trade-offs**

Loosening "Unknowns stated honestly" flipped `pkg-05` from reject to accept. I skipped canary-checking specific packages with `--only` before the confirming run and went straight to a full run instead, since only one check changed and a full run catches any new flip directly. It came back 20/20, so nothing else moved, including every other `clear-accept` package that also has its own risks/unknowns section.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
