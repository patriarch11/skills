# Development Skills for Claude Code

A collection of 8 slash commands for structured development workflows with approval gates.

## Installation

### Claude Code

Copy the command files to your project's `.claude/commands/` directory:

```bash
# Project-level (available in this repo only)
mkdir -p .claude/commands
cp claude-code/commands/*.md .claude/commands/

# Or user-level (available in all repos)
mkdir -p ~/.claude/commands
cp claude-code/commands/*.md ~/.claude/commands/
```

After installation, commands are available as slash commands:
- `/dev-spec` - Convert freeform request to approved specification
- `/dev-plan` - Turn approved spec into implementation plan
- `/dev-implement` - Implement approved plan
- `/dev-verify` - Run existing checks, fix regressions
- `/dev-test` - Add tests for changed behavior
- `/dev-review` - Final self-review against spec and plan
- `/dev-workflow` - Full orchestrated workflow (spec -> plan -> implement -> verify -> test -> review)
- `/repo-architecture` - Create ADRs and AGENTS.md for a repository

### Other Agent Tools

The `.md` files in `commands/` are self-contained prompts with frontmatter metadata. They can be adapted for any agent system that accepts markdown-based instructions:

- **Cursor**: Copy to `.cursor/rules/` or use as custom instructions
- **Windsurf**: Add to `.windsurfrules` or custom commands
- **Aider**: Use as `--message-file` or add to `.aider.conf.yml` conventions
- **Copilot**: Reference in `.github/copilot-instructions.md`
- **Any LLM agent**: Paste the file content as a system/user prompt

## Recommended Usage

1. Use `/dev-workflow` as the default entry point for end-to-end work.
2. Use individual phase commands when you want to force a specific stage.
3. The workflow enforces approval gates after Specification and Plan phases.

## Dev Skill Family

The 7 dev skills form a phased workflow:

```
Request -> Spec -> Plan -> Implement -> Verify -> Test -> Review -> Done
             ^               ^
          approval         approval
           gate              gate
```

Each phase produces a structured markdown artifact that the next phase consumes.
