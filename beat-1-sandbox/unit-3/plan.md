# Plan: issue #69, output parser crashes on a top-level JSON array fallback

## Diagnosis

`parse_review_output` in `rag/generator/output_parser.py` calls `_parse_json_output(data)` any time `json.loads` succeeds, without checking that `data` is a dict. `_parse_json_output` immediately calls `data.items()` at line 68, which raises `AttributeError: 'list' object has no attribute 'items'` when the parsed JSON is a top-level array instead of an object.

This matches my posted repro evidence exactly (https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69#issuecomment-5740015917):

> Direct call: `python3 -c "... parse_review_output(json.dumps(['First feedback item', 'Second feedback item']))"` raises `AttributeError: 'list' object has no attribute 'items'` at `rag/generator/output_parser.py:68`.
>
> Normal pytest run hides the crash behind the xfail marker: `test_json_array_fallback XFAIL`. `pytest --runxfail` forces it to run for real and produces the identical traceback, rooted at the same line.

The issue body asks for the same fix directly: "Fix the fallback path to handle array responses" and "Remove the `@pytest.mark.xfail` marker from the covering test." No maintainer thread comments beyond that.

## Scope

In scope: guard the two `json.loads` call sites inside `parse_review_output` (the code-fence branch and the raw-JSON branch) so a successfully-parsed non-dict value falls through to the existing plaintext fallback instead of being handed to `_parse_json_output`. Remove the `xfail` marker on `test_json_array_fallback` in `tests/unit/test_output_parser.py` once the fix makes it pass for real.

Not in scope: changing `_parse_json_output`'s signature or behavior (it keeps assuming a dict, which is now guaranteed by the caller), changing what the plaintext fallback produces, or touching the malformed-JSON path (already handled by the existing `except json.JSONDecodeError` blocks).

## Files

- `rag/generator/output_parser.py`, function `parse_review_output`
- `tests/unit/test_output_parser.py`, test `test_json_array_fallback`

## Approach

1. After `data = json.loads(json_str)` in the code-fence branch, check `isinstance(data, dict)` before calling `_parse_json_output(data)`. If it isn't a dict, log a warning the same way the file already does for the JSONDecodeError branches, and fall through instead of returning.
2. Do the same after `data = json.loads(raw)` in the raw-JSON branch.
3. Both branches now fall through to the existing `return _parse_plaintext_output(raw)` at the bottom of the function when the parsed JSON isn't a dict, so a top-level array (or any other non-dict JSON value) gets the same graceful handling a JSON decode failure already gets.
4. Remove the `@pytest.mark.xfail(...)` decorator from `test_json_array_fallback`.

## Test plan

Re-running my unit-2 repro steps against the built change:

- Direct call, `python3 -c "from rag.generator.output_parser import parse_review_output; print(parse_review_output(json.dumps(['First feedback item', 'Second feedback item'])))"`. Before: `AttributeError` at line 68. After: returns a one-item list, `result[0].section_name == "general_feedback"`, no crash.
- `pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback --runxfail`. Before: forces past the xfail marker and hits the same `AttributeError` trace. After (with the marker removed): a plain `pytest` run shows `PASSED`, not `XFAIL`.
- `pytest tests/unit/test_output_parser.py`. Before and after: every other test stays green; this one flips from `XFAIL` to `PASSED`.

## Risks and unknowns

The new `logger.warning` call adds a `data_type=type(data).__name__` field; every other `logger.warning` call in this file already logs plain string/int fields under structlog, so this isn't a new risk.

One real unknown: the issue doesn't say whether a JSON array's elements should become separate feedback sections instead of one combined plaintext blob. Nothing in the issue or the (empty) thread asks for that, so this plan treats a non-dict JSON value as a fallback-to-plaintext case, matching the module's existing decision not to special-case anything between "valid dict JSON" and "not JSON at all."

## Deviations

Nothing changed. The build matched the plan exactly: guarded the two `json.loads` call sites in `parse_review_output` with an `isinstance(data, dict)` check, added a `logger.warning` on each new fallback path, and removed the `xfail` marker on `test_json_array_fallback`. No other files touched, no follow-up needed on the thread.
