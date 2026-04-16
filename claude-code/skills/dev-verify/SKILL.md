---
name: dev-verify
description: Run existing repository checks after implementation to verify nothing is broken. Use for regression checking after code changes or test additions.
disable-model-invocation: true
allowed-tools: Bash
---

# Dev Verify

Run the relevant existing repository checks after implementation and repair regressions introduced by the change when possible.

## Workflow

1. Identify the most relevant existing checks for the changed area.
2. Run targeted existing tests first; expand to broader checks only if needed or if project norms require it.
3. Run lint, typecheck, build, or equivalent checks when the project has them and they are relevant to the change.
4. If the change caused a failure, fix it and rerun the affected checks.
5. If failures appear unrelated or pre-existing, say so clearly instead of assuming ownership.
6. Return a verification report.

## Boundaries of autonomy

You may fix failures that are a direct consequence of the approved change. Ask the user before continuing if:
- Fixing the failure would require a broader refactor.
- The failing area appears unrelated to the approved scope.
- The repository has many pre-existing failures and the next step is unclear.
- Required commands are destructive, slow, or operationally risky.

## Definition of done

Consider this phase done only when all of the following are true:
- The relevant existing checks were identified and run, or their absence was stated.
- Any regression caused by the change was fixed when feasible within scope.
- Remaining failures are explicitly categorized as related, unrelated, or uncertain.
- The report states exactly what commands or checks were run.

## Output artifact

Always return a single markdown artifact using this exact structure:

```markdown
# Verification Report

## Checks run
- [command or check] - [result]

## Regressions fixed
- [none] or ...

## Remaining failures
- [none] or ...

## Assessment
[State whether the implementation appears stable against existing checks.]
```

## Quality bar

Prefer evidence over reassurance. Be precise about which checks were run and what they covered. Distinguish clearly between existing project failures and new regressions.
