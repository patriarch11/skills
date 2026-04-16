# AGENTS.md Template (English)

Use this structure as the default for repository `AGENTS.md` files.
Adapt sections to the repository; remove sections that do not add value.

```markdown
# AGENTS.md

## Purpose
[What this repository is for and what agents should optimize for.]

## Repository shape
- Type: [service | monolith | monorepo | library | cli | mixed]
- Main components: [...]
- Important directories: [...]

## Stack and tooling
- Languages/frameworks: [...]
- Package/build tools: [...]
- Infrastructure/runtime: [...]

## Preferred commands
- Install: `...`
- Dev: `...`
- Test: `...`
- Lint: `...`
- Build: `...`

## Working rules for agents
- Prefer minimal, scoped changes.
- Follow existing naming and module boundaries.
- Update tests and docs when behavior changes.
- Do not introduce new architecture without checking ADRs first.

## Architecture notes
[Short repository-specific summary of boundaries and runtime flow.]

## ADR index
- [ADR title](relative/path/to/adr.md) — [one-line meaning]
- [ADR title](relative/path/to/adr.md) — [one-line meaning]

## Decision precedence
1. Accepted ADRs
2. Explicit user instructions for the current task
3. Repository conventions already present in code and docs

## When adding a new ADR
- Save the ADR in the configured ADR directory.
- Link it from this file.
- Prefer extending an existing ADR only when the decision is truly the same decision.
```

## Guidance

- Keep this operational, not philosophical.
- If some details are inferred and not yet confirmed, label them clearly.
- Prefer repository-relative links for ADR references.
- Keep commands copy-pasteable.
