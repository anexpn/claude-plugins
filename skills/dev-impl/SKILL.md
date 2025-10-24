---
name: dev-impl
description: Execute implementation of a single task from a development plan in an isolated session. This skill should be used when implementing one task from a task list created by dev-spec. Use this for focused, context-efficient implementation that strictly follows the plan.
---

# Development Implementation

## Overview

Execute the implementation of a single task from a development plan. This skill operates in an isolated session with minimal context, focusing exclusively on completing one task according to the detailed plan.

## When to Use This Skill

Use this skill when:
- Implementing a task from a task list (created by dev-spec)
- Starting a fresh implementation session without carrying over unnecessary context
- Following a detailed plan that has already been created
- Working on one specific unit of work that will be reviewed separately

## Core Principle

**DO NOT DEVIATE FROM THE PLAN.** The planning phase has already determined the approach. This phase is strictly about execution according to the plan.

## Workflow

### Step 1: Identify the Task

1. Ask the user to provide the path to the task list file
2. Read the task list file
3. Identify the next uncompleted task (first `- [ ]` item)
4. Note the plan line numbers referenced for this task

### Step 2: Load Context

Read ONLY the necessary context:
1. **Task list** (`docs/development/NNN-<name>/tasks.md`) - to identify the task
2. **Spec file** (path specified at top of task list) - to understand the overall goal
3. **Plan section** (path and line numbers specified in task list) - to get detailed instructions for this specific task

**Important:** Do NOT read unrelated code or explore beyond what the plan specifies. Keep the context focused and minimal.

### Step 3: Implement According to Plan

Follow the plan section for this task exactly:
1. Touch the files specified in the plan
2. Follow the code structure and patterns described
3. Implement tests as specified (TDD approach)
4. Follow the testing approach described
5. Make changes incrementally
6. Test as you go

**Key principles during implementation:**
- DRY (Don't Repeat Yourself)
- YAGNI (You Aren't Gonna Need It)
- TDD (Test-Driven Development)
- Follow the plan's guidance on file organization, patterns, and test design
- Make small, focused changes
- DO NOT add features not in the plan
- DO NOT refactor beyond what the plan specifies

### Step 4: Self-Review

Before declaring the task complete:
1. Verify all requirements from the plan section are met
2. Run the tests
3. Check that the implementation matches the plan's intent
4. Ensure code follows project conventions

### Step 5: Await Review

After implementation is complete:
1. Inform the user the task is complete
2. DO NOT mark the task as complete in the task list yet
3. Wait for the user to run the dev-review skill
4. The user will either:
   - Provide reviewer feedback (return to Step 3 to address it)
   - Confirm sign-off (proceed to Step 6)

### Step 6: Mark Complete and Commit

Only after receiving explicit sign-off from the reviewer:
1. Mark the task as complete in the task list (change `- [ ]` to `- [x]`)
2. Create a git commit with a clear message describing what was implemented
3. Include reference to the task number or description

**Commit message format:**
```
Implement [task description]

- Brief summary of what was done
- Reference to task list item

Related to: docs/development/NNN-<name>/tasks.md
```

## Important Constraints

1. **One task only** - Do not proceed to the next task automatically
2. **No deviation** - Follow the plan exactly; don't improvise or "improve" unless the plan says to
3. **Isolated session** - This should be a fresh session without unrelated context
4. **No premature completion** - Only mark complete after reviewer sign-off
5. **Always commit** - Every completed task gets its own commit

## Handling Issues

If you encounter problems during implementation:
- **Plan is unclear:** Ask the user to clarify (may need to update the plan)
- **Plan approach doesn't work:** Stop and inform the user (may need to update the plan)
- **Tests are failing:** This is your responsibility - fix them before completing
- **Unexpected conflicts:** Stop and ask the user for guidance

**DO NOT** solve problems by deviating from the plan without explicit permission.

## Context Awareness

This skill is part of a larger workflow:
- **dev-spec** creates the spec, plan, and task list
- **dev-impl** (this skill) implements individual tasks
- **dev-review** reviews completed work

The implementer role is deliberately constrained and focused. Strategic thinking and design decisions have already been made in the planning phase.
