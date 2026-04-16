---
name: dev-test
description: add or update tests for the behavior introduced or changed by an approved implementation. use when codex has already changed code and should now cover the new behavior, edge cases, and touched logic with focused tests. trigger this skill for creating unit, integration, or functional tests that match repository conventions, avoid brittle assertions, and document what scenarios are now covered.
---

# Dev Test

Add focused tests for the newly introduced or changed behavior. Cover the change, not the whole product.

## Workflow

1. Read the approved specification, approved plan, and implementation summary if available.
2. Identify the behavioral surface that changed.
3. Add or update the smallest set of meaningful tests needed to cover the change and its important edge cases.
4. Follow the project's existing testing style, fixtures, helpers, and naming conventions.
5. Run the new or updated tests.
6. Return a coverage report.

## Boundaries of autonomy

Ask the user before continuing if meaningful coverage would require:
- introducing a new test framework or major test helper,
- broad changes to test infrastructure,
- large snapshots or golden files with unclear review value,
- high-cost integration coverage that exceeds the apparent need.

Do not add noisy, brittle, or redundant tests just to increase count.

## Definition of done

Consider this phase done only when all of the following are true:
- New behavior and changed logic are covered by tests appropriate to the repository.
- Important edge cases from the specification are reflected where practical.
- The new or updated tests were run, or the limitation was stated.
- Remaining coverage gaps are explicit.

## Output artifact

Always return a single markdown artifact using this exact structure:

```markdown
# Test Coverage Report

## Tests added or updated
- [path or test name] - [scenario]

## Scenarios covered
- ...

## Commands run
- ...

## Remaining gaps
- [none] or ...
```

## Quality bar

Prefer behavior-focused tests with clear intent. Reuse existing fixtures. Keep assertions specific enough to catch regressions without making the test fragile.
