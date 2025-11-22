---
name: dev-spec
description: Guide a complete design and planning session for development work (features, bugfixes, hotfixes). This skill should be used when starting new development work that requires a spec, detailed implementation plan, and task breakdown. Use this for substantial changes that need careful planning and tracking.
---

# Development Spec & Planning

## Overview

Guide the creation of a complete development specification, implementation plan, and task list for new features, bugfixes, or hotfixes. This skill covers three phases: specification generation, detailed planning, and task breakdown.

## Execution Model

**This skill runs in the main conversation, not as a subagent.**

The specification phase requires back-and-forth interaction with the user (asking questions, getting approval for each section). Subagents cannot interact with users, so this phase must run directly in the main conversation.

For the planning and task extraction phases, you have two options:
1. **Continue in main conversation** - Simpler, maintains context
2. **Spawn subagents** - Use when you want isolated context for planning

If spawning subagents for planning/tasks, you must embed all necessary context in the prompt (see dev-workflow skill for templates).

## When to Use This Skill

Use this skill when:
- Starting a new feature, bugfix, or hotfix that requires planning
- The work is substantial enough to benefit from a written spec and plan
- Multiple implementation steps need to be tracked
- An implementation will happen in separate sessions requiring clear guidance

## Workflow

### Phase 1: Specification Generation

Start by gathering context and refining the user's idea into a fully-formed specification.

**Approach:**
1. Examine the current project state to understand the starting point
2. Ask clarifying questions ONE AT A TIME to refine the idea
   - Prefer multiple-choice questions for efficiency
   - Open-ended questions are acceptable when necessary
   - NEVER ask more than one question per message
3. Continue until the requirements are fully understood
4. Present the design specification in sections of 200-300 words
5. Ask for confirmation after EACH section before proceeding

**Initial prompt to use:**
> I've got an idea I want to talk through with you. I'd like you to help me turn it into a fully formed design and spec (and eventually an implementation plan). Check out the current state of the project in our working directory to understand where we're starting off, then ask me questions, one at a time, to help refine the idea. Ideally, the questions would be multiple choice, but open-ended questions are OK, too. Don't forget: only one question per message. Once you believe you understand what we're doing, stop and describe the design to me, in sections of maybe 200-300 words at a time, asking after each section whether it looks right so far.

**Output:** Write the complete specification to `docs/development/NNN-<name>/spec.md` where:
- `NNN` is a sequential number (ask user for the number or determine the next available)
- `<name>` is a short descriptive name (feature name, fix name, etc.)

### Phase 2: Implementation Planning

After the spec is approved, create a comprehensive implementation plan.

**Approach:**
1. Assume the implementer has zero context about the codebase
2. Assume the implementer has questionable taste and needs explicit guidance
3. Document everything needed:
   - Which files to touch for each task
   - Code structure and patterns to follow
   - Testing requirements and approach
   - Documentation to check or update
   - How to test each change
4. Break the work into bite-sized tasks
5. Emphasize: DRY, YAGNI, TDD, frequent commits
6. Account for the implementer being skilled but unfamiliar with the toolset and domain
7. Provide detailed guidance on test design (don't assume they know this well)

**Prompt to use:**
> Great. I need your help to write out a comprehensive implementation plan. Assume that the engineer has zero context for our codebase and questionable taste. Document everything they need to know. Which files to touch for each task, code, testing, docs they might need to check. How to test it. Give them the whole plan as bite-sized tasks. DRY. YAGNI. TDD. Frequent commits. Assume they are a skilled developer, but know almost nothing about our toolset or problem domain. Assume they don't know good test design very well. Please write out this plan, in full detail, into docs/. Extract a task list for the engineer to track his process. Let the engineer update the task list when he finishes a step.

**Output:** Write the complete plan to `docs/development/NNN-<name>/plan.md`

### Phase 3: Task List Extraction

Extract a structured task list from the implementation plan.

**Task list format:**
```markdown
# Task List: <Feature/Fix Name>

**Spec:** docs/development/NNN-<name>/spec.md
**Plan:** docs/development/NNN-<name>/plan.md

## Tasks

- [ ] Task 1 description (Plan lines: XX-YY)
- [ ] Task 2 description (Plan lines: ZZ-AA)
- [ ] Task 3 description (Plan lines: BB-CC)
...

## Instructions for Implementer

1. Implement ONE task at a time
2. Read the corresponding plan section (line numbers provided)
3. Follow the plan - DO NOT DEVIATE
4. After completing a task and getting sign-off, mark it complete with [x]
5. Commit after each completed task
```

**Output:** Write the task list to `docs/development/NNN-<name>/tasks.md`

## File Structure

All files for a development session are stored in:
```
docs/development/NNN-<name>/
├── spec.md       # Design specification
├── plan.md       # Detailed implementation plan
└── tasks.md      # Task tracking list
```

## Next Steps

After completing all three phases, guide the user to use:
- **dev-impl** skill: For implementing individual tasks in isolated sessions
- **dev-review** skill: For reviewing completed work

Remind the user:
1. Implementation should happen in separate sessions (one task at a time)
2. The implementer should read: task list → spec → relevant plan section
3. After implementation, spawn a checker session using dev-review
4. Only mark tasks complete after review sign-off
