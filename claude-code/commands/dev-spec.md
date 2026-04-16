---
description: Turn a freeform development request into an approved implementation specification. Use for feature requests, bug fixes, refactors, integrations, and API changes when the request is ambiguous or missing acceptance criteria.
---

# Dev Spec

Convert the user's freeform request and any provided context into an implementation-ready specification. Do not write code. Do not produce an implementation plan. Stop and wait for explicit user approval before any later phase.

## Workflow

1. Parse the request and any provided task context.
2. Distill the work into a concrete specification.
3. Surface assumptions, ambiguities, constraints, dependencies, and missing information.
4. Capture non-functional requirements only if the user supplied them. If none were supplied, state `nfrs: none provided` instead of inventing them.
5. Ask for explicit approval of the specification.
6. Stop after presenting the artifact.

## Boundaries of autonomy

Ask the user instead of deciding silently when any of these are true:
- Multiple plausible product interpretations exist.
- The requested behavior conflicts with provided context, repo conventions, or earlier instructions.
- Scope is unclear enough that different implementations would materially differ.
- Missing information would change the acceptance criteria, API contract, data model, or user experience.

Do not:
- Start planning.
- Suggest a full implementation sequence.
- Choose a library or stack unless the user explicitly asked for options in the specification phase.
- Mark the spec as approved without an explicit user confirmation.

## Definition of done

Consider this phase done only when all of the following are true:
- The requested outcome is restated clearly.
- Scope and non-goals are explicit.
- Acceptance criteria are testable.
- Assumptions and open questions are listed.
- NFRs are captured as provided by the user, or explicitly marked as not provided.
- The output ends with a direct request for approval or corrections.

## Output artifact

Always return a single markdown artifact using this exact structure:

```markdown
# Specification

## Summary
[One short paragraph describing the requested change.]

## Scope
- ...

## Non-goals
- ...

## Inputs and constraints
- ...

## Assumptions
- ...

## Acceptance criteria
- ...

## NFRs
- [Use user-provided NFRs only, or write `none provided`]

## Open questions
- ...

## Approval request
[Ask the user to approve or correct the specification.]
```

## Quality bar

Prefer a compact, implementation-relevant spec over product prose. Convert vague statements into observable behavior. Make acceptance criteria concrete enough that later review can verify them line by line.
