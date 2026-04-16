---
name: dev-plan
description: turn an approved specification into an implementation plan for codex. use when the specification is already approved and codex should inspect the codebase, fit the change into the current architecture, identify affected files and modules, choose the technical approach, note risks, and stop for explicit approval before writing code. trigger this skill for planning new features, bug fixes, refactors, schema changes, and integrations where architecture fit and validation strategy matter.
---

# Dev Plan

Create an implementation plan from an approved specification. Inspect the codebase before proposing changes. Do not write code. Stop and wait for explicit user approval before implementation.

## Inputs

Require an approved specification from the user or from earlier conversation context. If the specification is missing or clearly unapproved, ask for it or route back to the specification phase.

## Workflow

1. Read the approved specification.
2. Inspect the repository to understand the existing structure, patterns, entry points, and constraints.
3. Identify the smallest change that fits the current architecture.
4. Propose the approach, affected areas, validation strategy, and risks.
5. Highlight any decision that exceeds the agent's autonomy boundary.
6. Ask for explicit approval of the plan.
7. Stop after presenting the artifact.

## Boundaries of autonomy

Ask the user before finalizing the plan if any of these are required or likely:
- Add a new dependency or framework.
- Introduce a new architectural layer, service, package, or cross-cutting abstraction.
- Change an external API contract, event contract, public interface, or persistence schema.
- Restructure a large area of the codebase.
- Choose between materially different approaches with different trade-offs.

Prefer fitting into existing project conventions over inventing new structure.

## Definition of done

Consider this phase done only when all of the following are true:
- The plan maps back to the approved specification.
- Affected files, modules, or subsystems are identified as specifically as possible.
- The implementation approach is concrete and minimal.
- Validation steps are defined.
- Risks, trade-offs, and approval-needed decisions are explicit.
- The output ends with a direct approval request.

## Output artifact

Always return a single markdown artifact using this exact structure:

```markdown
# Implementation Plan

## Spec reference
[Short summary of the approved specification being implemented.]

## Proposed approach
- ...

## Affected areas
- [file/module/subsystem] - [why it changes]

## Architecture fit
- ...

## Stack and dependencies
- [existing stack to use]
- [new dependency only if truly needed]

## Risks and trade-offs
- ...

## Validation plan
- [existing tests/checks to run]
- [new tests likely needed]

## Approval-needed decisions
- ...

## Approval request
[Ask the user to approve the plan or request changes.]
```

## Quality bar

Ground the plan in the current repository, not in an idealized rewrite. Prefer smaller and safer changes. If the stack was not specified, recommend the most natural fit for the existing codebase rather than a fashionable tool.
