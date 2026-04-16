---
name: dev-workflow
description: Orchestrate a full development workflow from freeform request to final review with phased artifacts and approval gates. The default entry point for end-to-end coding work.
disable-model-invocation: true
argument-hint: "[task description or paste task text]"
---

# Dev Workflow

Orchestrate the full development workflow from freeform request to final review. Use phased artifacts. Enforce approval gates. Do not skip directly to code unless the user has already provided approved phase artifacts.

## Canonical sequence

Run phases in this order:
1. Specification
2. Planning
3. Implementation
4. Verification of existing checks
5. Tests for changed behavior
6. Verification again if new tests or fixes were added
7. Final review

## Entry rules

Choose the starting phase from available context:
- If the user gives only a freeform request or pasted task text, start at Specification.
- If the user provides an approved specification, start at Planning.
- If the user provides an approved specification and approved plan, start at Implementation.
- If code changes already exist and the user only wants regression checking, start at Verification.
- If code changes exist and the user only wants tests, start at Test.
- If the user wants a final self-check, start at Review.

When in doubt, start earlier rather than later.

## Approval gates

Require explicit user approval after:
- Specification.
- Implementation Plan.

Do not continue past either gate on implied approval.

## Phase artifacts

Produce these exact artifacts at the end of each phase:
- `# Specification`
- `# Implementation Plan`
- `# Implementation Summary`
- `# Verification Report`
- `# Test Coverage Report`
- `# Final Review Report`

If an earlier artifact already exists in context, reuse it instead of regenerating it unless the user asked to revise it.

## Global boundaries of autonomy

Pause and ask the user before proceeding if the work requires:
- A new dependency.
- A new architectural layer or large restructuring.
- An API or data contract change.
- A persistence schema change.
- Materially broader scope than the approved spec or plan.
- Destructive or risky operational actions.

## Global definition of done

Treat the end-to-end workflow as done only when all of the following are true:
- Specification approved by the user.
- Implementation plan approved by the user.
- Code implemented within the approved boundaries.
- Relevant existing checks run and regressions addressed.
- New or changed behavior covered by tests.
- Final review reports whether the implementation is ready or still needs changes.

## Orchestration behavior

At the end of each phase:
- Summarize the phase briefly.
- Emit the phase artifact.
- Either stop for approval or continue to the next phase according to the sequence above.

If Final Review reports `needs changes`, loop through the minimum necessary corrective path:
- Implement the fix.
- Rerun relevant checks.
- Update tests if needed.
- Run final review again.

## Quality bar

Optimize for controlled progress, not speed. The workflow should feel like a disciplined senior engineer: clarify first, plan second, build third, verify with evidence, then review against the original request.
