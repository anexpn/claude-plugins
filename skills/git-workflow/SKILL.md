---
name: git-workflow
description: Version control workflow and best practices for git operations. Use this skill when starting work on a project, managing git repositories, committing changes, creating branches, or handling uncommitted work to ensure proper version control hygiene.
---

# Git Workflow

## Overview

This skill defines best practices for version control using git, including repository initialization, branch management, commit practices, and handling uncommitted changes. It ensures disciplined version control that maintains clean history and proper change tracking.

## When to Use This Skill

Use this skill when:
- Starting work on a new project
- Beginning a new feature or task
- Handling uncommitted changes
- Creating commits
- Managing branches
- Working with version control in any capacity

## Pre-Work Assessment

Before starting any development work, perform this assessment:

### 1. Check if Project is in Git Repository

If the project isn't in a git repository:
- **STOP** and ask permission to initialize one
- Do not proceed with work until the repository decision is made
- Explain why version control is important for the task

### 2. Assess Uncommitted Changes

Before starting new work, check for uncommitted changes or untracked files:
- Run `git status` to see the current state
- **STOP** and ask how to handle existing changes
- Suggest committing existing work first before starting new tasks
- Never mix unrelated changes together

### 3. Verify or Create Working Branch

When starting work without a clear branch for the current task:
- Create a WIP (Work In Progress) branch
- Use descriptive branch names that indicate the work being done
- Example: `wip/add-user-authentication`, `fix/memory-leak-in-parser`

## Commit Practices

### Track All Non-Trivial Changes

All meaningful changes should be tracked in git:
- Commit logical units of work
- Don't wait until everything is "perfect" to commit
- Commits create checkpoints for experimentation

### Commit Frequently Throughout Development

Commit regularly during the development process:
- Commit even if high-level tasks aren't complete
- Create commits for incremental progress
- Commit after each meaningful step
- Include journal entries in commits

### Never Skip, Evade, or Disable Pre-Commit Hooks

Pre-commit hooks exist for important reasons:
- NEVER use `--no-verify` or similar flags
- If a hook fails, fix the issue it identifies
- Don't bypass code quality checks
- If a hook is problematic, discuss it rather than disabling it

### Selective Staging with git add

Be intentional about what gets staged:
- **NEVER use `git add -A`** unless immediately after `git status`
- Review changes before staging them
- Don't add random test files, temporary files, or unrelated changes
- Stage related changes together
- Use `git add <specific-files>` or `git add -p` for selective staging

## Branch Management

### Branch Naming Conventions

Use descriptive, lowercase branch names with hyphens:
- `wip/feature-description` - Work in progress
- `feature/specific-feature` - New feature
- `fix/bug-description` - Bug fix
- `refactor/component-name` - Code refactoring

### When to Create Branches

Create a new branch when:
- Starting a new feature
- Beginning a bug fix
- Starting work without a clear current branch
- Experimenting with changes
- Working on tasks that may need isolation

## Commit Messages

### Commit Message Structure

Write clear, informative commit messages:
- Use present tense ("Add feature" not "Added feature")
- Be specific about what changed and why
- Focus on the "why" more than the "what"
- Keep the first line concise (50 characters or less)
- Add detailed explanation in the body if needed

### Example Good Commit Messages

```
Add user authentication with JWT tokens

Implement JWT-based authentication to support stateless sessions.
This enables horizontal scaling without session storage concerns.
```

```
Fix memory leak in WebSocket connection handler

Connection handlers weren't being properly cleaned up on disconnect,
causing memory to grow unbounded over time.
```

## Anti-Patterns to Avoid

- **Working without version control**: Always use git for projects
- **Mixing unrelated changes**: Keep commits focused and logical
- **Bypassing hooks**: Never skip pre-commit checks
- **Indiscriminate staging**: Don't use `git add -A` blindly
- **Infrequent commits**: Commit regularly, not just at milestones
- **Vague commit messages**: Be specific about changes and rationale
- **Working on main**: Create branches for new work
