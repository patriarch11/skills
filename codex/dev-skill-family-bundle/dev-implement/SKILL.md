---
name: dev-implement
description: implement code changes from an approved implementation plan. use when codex already has an approved spec and plan and should modify the repository accordingly without redoing discovery. trigger this skill for writing code, editing files, refactoring within agreed boundaries, and keeping the implementation aligned with the approved plan. the skill should avoid scope creep, escalate boundary-breaking decisions, and return a concise change summary instead of a new plan.
---

# Dev Implement

Implement the approved plan in the repository. Stay inside the approved scope. Do not silently expand the change set.

## Preconditions

Require both of the following before implementation:
- an approved specification,
- an approved implementation plan.

If either is missing or ambiguous, stop and ask for the missing approval or route back to the relevant phase.

## Workflow

1. Restate the approved target briefly to anchor the work.
2. Modify the smallest set of files that satisfies the plan.
3. Reuse existing patterns, abstractions, and conventions.
4. Keep notes about deviations, blockers, or follow-up items.
5. Return a compact implementation summary.

## Boundaries of autonomy

Pause and ask the user before continuing if implementation requires:
- adding a new dependency,
- changing an API contract or persistence schema,
- introducing a new architecture pattern or large module split,
- touching unrelated subsystems not named in the plan,
- making product decisions that change the approved behavior,
- performing destructive data or file operations outside the planned scope.

If the repository reality differs from the plan, explain the mismatch and propose the smallest correction before proceeding.

## Definition of done

Consider this phase done only when all of the following are true:
- The code changes follow the approved plan or document a justified deviation.
- Scope creep is avoided.
- The changed files are coherent and readable.
- Known blockers or follow-ups are stated explicitly.
- The output includes a clear summary of what changed.

## Output artifact

Always return a single markdown artifact using this exact structure:

```markdown
# Implementation Summary

## Goal
[Short reminder of the approved change.]

## Files changed
- [path] - [reason]

## Key implementation notes
- ...

## Deviations from plan
- [none] or ...

## Blockers or follow-ups
- [none] or ...
```

## Quality bar

Prefer minimal, maintainable diffs. Preserve existing project style. Avoid speculative cleanups unless they are required to complete the approved work.
