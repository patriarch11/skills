---
description: Review an implemented change against the approved spec and plan. Use for final self-review before handoff and to decide whether another implementation-test-verify loop is needed.
---

# Dev Review

Review the resulting change against the approved specification and approved implementation plan. Treat this as a final self-check before handoff.

## Workflow

1. Compare the implementation against the approved specification line by line.
2. Check whether the approved plan was followed or consciously deviated from.
3. Review tests and verification evidence.
4. Identify gaps, edge cases, or mismatches.
5. If small corrections are needed and remain within scope, make them and rerun the relevant tests/checks before finalizing the review.
6. Return a final review report with a clear status.

## Boundaries of autonomy

You may make small in-scope corrections discovered during review. Ask the user before continuing if review reveals a need for:
- Materially expanding scope.
- Changing architecture, dependencies, or contracts.
- Revisiting product behavior that was previously approved.
- A major rewrite rather than a review-driven correction.

## Definition of done

Consider this phase done only when all of the following are true:
- Acceptance criteria were checked explicitly.
- Plan compliance or justified deviations were documented.
- Verification and test evidence were considered.
- Remaining risks or gaps are explicit.
- The final status is unambiguous.

## Output artifact

Always return a single markdown artifact using this exact structure:

```markdown
# Final Review Report

## Spec compliance
- [criterion] - [met / not met / partial]

## Plan compliance
- ...

## Test and verification evidence
- ...

## Remaining risks or gaps
- [none] or ...

## Final status
[ready / needs changes]
```

## Quality bar

Be strict and evidence-based. Do not mark the work ready if acceptance criteria are not clearly met. Prefer explicit gap lists over vague confidence language.
