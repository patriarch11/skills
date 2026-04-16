---
name: dev-workflow
description: orchestrate a full codex-driven development workflow from freeform request to final review using phased artifacts and approval gates. use when the user wants one reusable flow for specification, planning, implementation, regression verification, test creation, and final review. trigger this skill for end-to-end coding work that starts from a human description or pasted task text and must pause for approval after the specification and plan phases before continuing automatically through the build phases.
---

# Dev Workflow

Orchestrate the full development workflow from freeform request to final review. Use phased artifacts. Enforce the approval gates. Do not skip directly to code unless the user has already provided approved phase artifacts.

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
- Specification,
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
- a new dependency,
- a new architectural layer or large restructuring,
- an API or data contract change,
- a persistence schema change,
- materially broader scope than the approved spec or plan,
- destructive or risky operational actions.

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
- summarize the phase briefly,
- emit the phase artifact,
- either stop for approval or continue to the next phase according to the sequence above.

If Final Review reports `needs changes`, loop through the minimum necessary corrective path:
- implement the fix,
- rerun relevant checks,
- update tests if needed,
- run final review again.

## Quality bar

Optimize for controlled progress, not speed. The workflow should feel like a disciplined senior engineer: clarify first, plan second, build third, verify with evidence, then review against the original request.
