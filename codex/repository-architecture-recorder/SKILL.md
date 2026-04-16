---
name: repository-architecture-recorder
description: creates and updates repository adr files and agents.md for code repositories. use when the user wants a repo-aware agent to discover the project structure, infer tools and run commands, propose which architectural decisions should be documented, turn free-form decisions into classical adr documents, or write an agents.md that references the repository adr set.
---

# Repository Architecture Recorder

## Overview

Use this skill to create or update an ADR set and `AGENTS.md` for a source repository.
The skill is optimized for a confirmation-first workflow: inspect the repository, infer missing context, confirm understanding with the user, propose ADR candidates, then write the approved ADRs and an `AGENTS.md` that points to them.

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

1. **Collect required and optional inputs**
   - Required: ADR directory.
   - Optional: toolchain/run instructions, architecture description, existing ADR naming convention, list of ADRs to draft now.

2. **Inspect repository when context is missing**
   - Review the repository tree and the smallest set of files needed to infer build, test, lint, dev, deploy, and architecture boundaries.
   - Prefer concise evidence over exhaustive file dumps.

3. **Confirm inferred understanding**
   - Present a short summary:
     - probable stack
     - probable run/test/lint/build commands
     - probable architecture shape
     - open questions or low-confidence assumptions
   - Ask the user whether this understanding is correct before locking it into ADRs or `AGENTS.md`.

4. **Propose ADR candidates**
   - Suggest which decisions deserve ADRs.
   - For each candidate include:
     - tentative title
     - why it matters
     - whether it seems already decided, partially decided, or still open
   - Ask the user which ones to approve, reject, merge, rename, or postpone.

5. **Draft approved ADRs**
   - Write only approved ADRs, or the ADRs explicitly requested by the user.
   - Use the classical ADR structure from `references/adr-template-uk.md`.
   - If numbering is needed and the repo does not already define it, default to zero-padded sequential filenames such as `0001-brief-kebab-case-title.md`.

6. **Draft or update `AGENTS.md`**
   - Summarize repository purpose, architecture, toolchain, commands, boundaries, and contribution expectations.
   - Add an ADR section that links to the approved ADR files.
   - State that ADRs are the source of truth for accepted architectural decisions.

## How to Infer Tooling and Commands

When the user did not provide commands, inspect repository evidence and derive a best-effort command map.

Suggested priorities:
- `Makefile`, `justfile`, task runners, or npm scripts usually provide the clearest command surface.
- Then check language/package manifests and lockfiles.
- Then check CI workflows to see what the project actually runs in automation.
- Then check container and deployment files for environment assumptions.

Return the inferred commands in a compact structure such as:

```markdown
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
- inspect top-level directories and entrypoints
- identify main runtime components and boundaries
- identify whether the repo is monolith, modular monolith, monorepo, service-oriented, library, CLI, or mixed
- identify data/storage integrations, queues, external APIs, and deployment surfaces when visible
- separate facts from hypotheses

Use a short confirmation block such as:

```markdown
My current understanding of the repository:
- Type: ...
- Main components: ...
- Runtime flow: ...
- Key integrations: ...
- Uncertain points: ...

Please confirm or correct this before I write ADRs and `AGENTS.md`.
```

## What Merits an ADR

Suggest ADRs for decisions that are stable enough, consequential enough, or costly enough to rediscover. Typical examples:
- system or repo structure
- module and boundary rules
- framework selection
- storage strategy
- API style and compatibility rules
- messaging/eventing approach
- background job model
- authn/authz model
- configuration and secret strategy
- testing strategy
- deployment/runtime topology
- observability approach
- multi-tenant or data-isolation approach
- migration strategy from a legacy architecture

Avoid proposing ADRs for trivial implementation details, ephemeral experiments, or items that clearly belong in routine documentation instead.

## ADR Writing Rules

Use the template in `references/adr-template-uk.md`.

Additional rules:
- Keep the prose crisp and concrete.
- Base the ADR on repository evidence and user confirmation.
- If something is still unresolved, mark the status accordingly instead of pretending it is accepted.
- Include alternatives when they materially clarify the decision.
- Prefer consequences that mention trade-offs, not just benefits.
- Do not invent metrics, incident history, or stakeholder approvals.

## `AGENTS.md` Writing Rules

Use the structure in `references/agents-template-en.md`.

Additional rules:
- Keep it operational and repository-specific.
- Prefer short sections over long essays.
- Separate confirmed facts from inferred-but-unconfirmed notes if confirmation is still pending.
- Include a section that links each approved ADR by filename and title.
- Tell future agents to consult ADRs before proposing architectural changes.
- If relevant, include a note describing how to add a new ADR and how `AGENTS.md` should be updated when ADRs change.

## Output Expectations

When proposing ADR candidates, use this compact format:

```markdown
## Proposed ADRs
1. **ADR-XXXX: Title**  
   Why: ...  
   State: decided | partially decided | open
```

When drafting an ADR, produce:
- target filename
- full markdown content

When drafting `AGENTS.md`, produce full markdown content that is ready to save.

## References

- For the classical ADR format in Ukrainian, see `references/adr-template-uk.md`.
- For the `AGENTS.md` structure in English, see `references/agents-template-en.md`.
