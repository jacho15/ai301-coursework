# Procedure: how this skill grades a plan package

## Read order

1. Read the issue's context. Summarize the broken feature in one line.
2. Read the repro-evidence block. Summarize the exact behavior it proves and the file, function, or code path it points to. This serves as the anchor for every other check.
3. Read the candidate plan in this order: stated cause, scope statement, approach, test plan, risks/unknowns.
4. Read the candidate plan comment. Check what it promises and to whom.
5. Read the repo-facts block and check for stated templates and the AI-use policy before grading Comms.

## Evidence gathering

- Diagnosis: pull the plan's stated cause as one line. Then pull the repro-evidence block's behavior and location as one line and compare the two side by side.
- Scope: pull the in-scope line and the not-in-scope line word for word. Mark either one "missing" if it isn't there.
- Executability: pull the named files or areas and the first concrete step. Record "no file named" if nothing is named.
- Test plan: pull the test plan's stated outcome. Pull the repro-evidence block's steps. Check whether the test plan reuses or adapts them.
- Honesty: pull the risks/unknowns section word for word. Record "none stated" if it's missing.
- Comms: pull the plan comment text. Pull the thread highlights and the repo-facts block's policy line.

## Check execution

Run the checks in this order: Diagnosis, Scope, Executability, Test plan, Honesty, Comms. Diagnosis goes first because Scope and Executability both check against the same cause it sets up.

If evidence for a check is genuinely missing, apply the rubric's fail condition for that and move on. Don't guess and don't ask the author. Log the gap as the check's evidence note instead.

Grade each check off the notes from evidence gathering. Only reread the full package if a check's notes contradict each other.

## Verdict assembly

Apply the rubric's verdict rule. Accept only if all six checks pass. Unclear counts as fail. Any fail or unclear rejects the package.

For whichever check decides a reject, quote the exact fact from that check's evidence note in the output. If more than one required check fails, quote whichever one ran first in check execution order.
