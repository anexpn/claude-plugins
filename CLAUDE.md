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

The plugin provides two complementary development workflows:

1. **dev-auto** → Autonomous development workflow
   - Generates detailed specs, plans, and tasks for autonomous agent execution
   - All artifacts serve as session memory: `docs/development/NNN-name/{spec.md, plan.md, tasks.md}`
   - Use when: Requirements are well-defined upfront, autonomous implementation desired
   - Contains 5 phases: Specification (interactive) → Planning → Task Extraction → Implementation (autonomous) → Review (interactive)

2. **dev-guided** → Human-in-the-loop iterative development
   - Creates problem statement, decisions log, runbook, and progress tracking
   - Use when: Requirements emerge during implementation, decisions need human approval at each step
   - Artifacts: `docs/development/NNN-name/{problem_statement.md, decisions.md, runbook.md, progress.md, plan-N.md}`

**Key concept:** Choose the workflow that matches your needs. dev-auto for autonomous execution with upfront planning, dev-guided for iterative work with ongoing human decisions.

The `dev-auto/references/` directory contains phase-specific instructions and subagent prompt templates (subagents have no context—everything must be embedded in the prompt).

## Writing/Modifying Skills

- Skills are pure markdown—no code
- Frontmatter `name` must match the directory name
- `description` in frontmatter determines when Claude Code suggests the skill
- References files are for embedding in subagent prompts, not for direct use

## Development Workflow Artifacts

**For dev-auto workflow:**
```
docs/development/NNN-<name>/
├── spec.md       # Design specification
├── plan.md       # Implementation plan
└── tasks.md      # Task tracking list
```

**For dev-guided workflow:**
```
docs/development/NNN-<name>/
├── problem_statement.md  # Problem scope and boundaries
├── decisions.md          # Explicit technical decisions with rationale
├── runbook.md            # Build/test/validation instructions and feedback points
├── progress.md           # Session-by-session progress log
└── plan-N.md             # Session-specific implementation plans
```
