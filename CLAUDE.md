# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Claude Code plugin providing development workflow commands and skills. It is a configuration-only project—no build system, no dependencies, just markdown files.

**Plugin name:** `jun-dev-workflows`
**Marketplace group:** `jun-workflows`

## Repository Structure

```
.claude-plugin/     # Plugin manifest files
commands/           # Slash commands (markdown)
skills/             # Skills (markdown in SKILL.md files)
```

## How Claude Code Plugins Work

**Commands** (in `commands/`): Slash commands that expand into prompts. Each `.md` file has frontmatter with `description` and optional `argument-hint`.

**Skills** (in `skills/`): Each skill is a directory with a `SKILL.md` file. Frontmatter must include `name` and `description`. Some skills have a `references/` subdirectory for supporting phase documentation.

**Manifest** (`.claude-plugin/plugin.json`): Points to `commands/` and `skills/` directories.

## Skill Architecture

The dev-workflow skills follow a coordinated pattern:

1. **dev-spec** → Interactive spec + plan + task creation (runs in main conversation)
2. **dev-impl** → Isolated task implementation (designed for subagent sessions)
3. **dev-review** → Code review against spec/plan (runs in main conversation)

**Key concept:** `dev-workflow` orchestrates the full process. `dev-spec`, `dev-impl`, and `dev-review` can be used independently.

The `dev-workflow/references/` directory contains phase-specific instructions meant to be embedded in subagent prompts (subagents have no context—everything must be passed in the prompt).

## Writing/Modifying Skills

- Skills are pure markdown—no code
- Frontmatter `name` must match the directory name
- `description` in frontmatter determines when Claude Code suggests the skill
- References files are for embedding in subagent prompts, not for direct use

## Development Workflow Artifacts

When using dev-spec/dev-workflow, artifacts are stored in:
```
docs/development/NNN-<name>/
├── spec.md       # Design specification
├── plan.md       # Implementation plan
└── tasks.md      # Task tracking list
```
