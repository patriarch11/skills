---
name: repo-architecture
description: Create and update ADR files and AGENTS.md for code repositories. Use to discover project structure, infer tooling, propose architectural decisions for documentation, or write an AGENTS.md that references the repository ADR set.
disable-model-invocation: true
argument-hint: "[ADR directory path]"
---

# Repository Architecture Recorder

Create or update an ADR set and `AGENTS.md` for a source repository.
Follow a confirmation-first workflow: inspect the repository, infer missing context, confirm understanding with the user, propose ADR candidates, then write the approved ADRs and an `AGENTS.md` that points to them.

## Core Rules

- Require the user to specify the target ADR directory before drafting ADR files. If it is missing, ask for it first.
- Treat toolchain details, run commands, and architecture notes as optional inputs. If the user does not provide them, inspect the repository and infer them from files such as `README*`, `package.json`, `pyproject.toml`, `poetry.lock`, `requirements*.txt`, `go.mod`, `Cargo.toml`, `pom.xml`, `build.gradle*`, `Dockerfile*`, `docker-compose*`, `Makefile`, CI workflows, monorepo configs, and framework-specific config files.
- Never present inferred repository facts as final truth when confidence is low. Summarize the inference and ask the user to confirm or correct it.
- Do not draft speculative ADRs immediately. First propose a candidate ADR list with short rationales and wait for approval.
- If the user provides free-form decision notes, normalize them into classical ADR format rather than copying them verbatim.
- Write `AGENTS.md` in English.
- Write ADR content in Ukrainian.
- Make `AGENTS.md` reference the ADR files explicitly using repository-relative links.

## Default Workflow

Follow this sequence unless the user explicitly asks for only one narrow step.

### 1. Collect required and optional inputs

- Required: ADR directory.
- Optional: toolchain/run instructions, architecture description, existing ADR naming convention, list of ADRs to draft now.

### 2. Inspect repository when context is missing

- Review the repository tree and the smallest set of files needed to infer build, test, lint, dev, deploy, and architecture boundaries.
- Prefer concise evidence over exhaustive file dumps.

### 3. Confirm inferred understanding

Present a short summary:
- Probable stack.
- Probable run/test/lint/build commands.
- Probable architecture shape.
- Open questions or low-confidence assumptions.

Ask the user whether this understanding is correct before locking it into ADRs or `AGENTS.md`.

### 4. Propose ADR candidates

Suggest which decisions deserve ADRs. For each candidate include:
- Tentative title.
- Why it matters.
- Whether it seems already decided, partially decided, or still open.

Ask the user which ones to approve, reject, merge, rename, or postpone.

### 5. Draft approved ADRs

- Write only approved ADRs, or the ADRs explicitly requested by the user.
- Use the classical ADR structure (see ADR template section below).
- If numbering is needed and the repo does not already define it, default to zero-padded sequential filenames such as `0001-brief-kebab-case-title.md`.

### 6. Draft or update AGENTS.md

- Summarize repository purpose, architecture, toolchain, commands, boundaries, and contribution expectations.
- Add an ADR section that links to the approved ADR files.
- State that ADRs are the source of truth for accepted architectural decisions.

## How to Infer Tooling and Commands

When the user did not provide commands, inspect repository evidence and derive a best-effort command map.

Suggested priorities:
1. `Makefile`, `justfile`, task runners, or npm scripts usually provide the clearest command surface.
2. Then check language/package manifests and lockfiles.
3. Then check CI workflows to see what the project actually runs in automation.
4. Then check container and deployment files for environment assumptions.

Return the inferred commands in a compact structure:

```
Inferred commands to confirm:
- Install: `...`
- Dev: `...`
- Test: `...`
- Lint: `...`
- Build: `...`
```

If multiple options exist, list the preferred one first and explain why briefly.

## How to Infer Architecture

When the user did not provide an architecture summary:
- Inspect top-level directories and entrypoints.
- Identify main runtime components and boundaries.
- Identify whether the repo is monolith, modular monolith, monorepo, service-oriented, library, CLI, or mixed.
- Identify data/storage integrations, queues, external APIs, and deployment surfaces when visible.
- Separate facts from hypotheses.

Use a short confirmation block:

```
My current understanding of the repository:
- Type: ...
- Main components: ...
- Runtime flow: ...
- Key integrations: ...
- Uncertain points: ...

Please confirm or correct this before I write ADRs and AGENTS.md.
```

## What Merits an ADR

Suggest ADRs for decisions that are stable enough, consequential enough, or costly enough to rediscover:
- System or repo structure
- Module and boundary rules
- Framework selection
- Storage strategy
- API style and compatibility rules
- Messaging/eventing approach
- Background job model
- Authn/authz model
- Configuration and secret strategy
- Testing strategy
- Deployment/runtime topology
- Observability approach
- Multi-tenant or data-isolation approach
- Migration strategy from a legacy architecture

Avoid proposing ADRs for trivial implementation details, ephemeral experiments, or items that clearly belong in routine documentation instead.

## ADR Template (Ukrainian)

Use this structure when drafting ADRs:

```markdown
# [Коротка назва рішення]

- Статус: [Запропоновано | Погоджено | Замінено | Відхилено]
- Дата: [YYYY-MM-DD]
- Пов'язані ADR: [за потреби, відносні посилання]

## Контекст
[Яку проблему або обмеження ми маємо. Які сили, вимоги, ризики чи обставини впливають на вибір.]

## Рішення
[Що саме ми вирішили зробити. Сформулюй рішення однозначно, без двозначностей.]

## Альтернативи
- [Альтернатива 1] - [чому не обрали]
- [Альтернатива 2] - [чому не обрали]

## Наслідки

### Переваги
- [...]

### Недоліки / компроміси
- [...]

### Подальші дії
- [...]
```

ADR writing rules:
- Keep the prose crisp and concrete.
- Base the ADR on repository evidence and user confirmation.
- If something is still unresolved, mark the status accordingly instead of pretending it is accepted.
- Include alternatives when they materially clarify the decision.
- Prefer consequences that mention trade-offs, not just benefits.

## AGENTS.md Template (English)

Use this structure for `AGENTS.md`:

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
- [ADR title](relative/path/to/adr.md) - [one-line meaning]

## Decision precedence
1. Accepted ADRs
2. Explicit user instructions for the current task
3. Repository conventions already present in code and docs

## When adding a new ADR
- Save the ADR in the configured ADR directory.
- Link it from this file.
- Prefer extending an existing ADR only when the decision is truly the same decision.
```

AGENTS.md writing rules:
- Keep it operational and repository-specific.
- Prefer short sections over long essays.
- Separate confirmed facts from inferred-but-unconfirmed notes if confirmation is still pending.
- Include a section that links each approved ADR by filename and title.
- Tell future agents to consult ADRs before proposing architectural changes.
