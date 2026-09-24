# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

Where it lives: in a bundle, the plan's stated cause and its approach's target file or location, read against the repro-evidence block. Live, the equivalent lines in the draft plan, read against the student's own posted repro comment (or, on the house issue, the house repro pack as quoted in the drafts).

What good looks like: the stated cause explains exactly the behavior the repro evidence shows, naming the same file, function, or code path. The approach then changes code at that same location. If the drafts quote no repro evidence at all, that absence is the fact this check fails on, not something to fill in from outside the package.

## Scope

Where it lives: the plan's in-scope statement and its not-in-scope line, plus any files or areas it names.

What good looks like: one bounded change, matching the diagnosed cause, with an explicit not-in-scope line. A scope that touches files unrelated to the cause, or carries no not-in-scope line at all, is a drive-by rewrite waiting to happen.

## Executability

Where it lives: the plan's approach section, its named files or areas, and its stated order of work.

What good looks like: a reader with no other context can name the first file to open and the first change to make, without asking the author anything. "Investigate the parser" is not executable; "change `_parse_json_output` in `output_parser.py` to branch on `isinstance(data, list)`" is.

## Test plan

Where it lives: the plan's test plan section, read against the repro-evidence block's steps and artifacts.

What good looks like: the test plan re-runs or adapts the exact steps the repro evidence used, and states the observable result that confirms the fix (an error that no longer raises, an assertion that now passes). A test plan that names no steps, or names steps unconnected to the repro evidence, proves nothing.

## Honesty

Where it lives: the plan's risks/unknowns section.

What good looks like: risks and unknowns the diagnosis or scope actually carries are named in plain language, not buried or omitted. A plan with no unknowns section, on a diagnosis that has any real uncertainty in it, is overconfident by omission. Stating that no further risks exist beyond the ones named is not itself overconfident; the overconfidence this check catches is claiming the fix will work without having tested it.

## Comms

Where it lives: the plan comment text, read against the issue's thread highlights and the repo-facts block's stated templates and contribution/AI-use policy (live: the issue thread and the repo's CONTRIBUTING or issue templates).

What good looks like: the comment states this plan's specific approach, not a generic "I'll fix this." If a maintainer already suggested a direction in the thread, the comment engages with it instead of ignoring it. On disclosure: pass if the policy is silent, or if it requires disclosure and the comment discloses; fail only when disclosure is required and the comment gives none.
