---
name: dev-workflow
description: Complete development workflow from specification to implementation to review. Use this skill for any substantial development work (features, bugfixes, hotfixes) that requires planning, isolated implementation, and review. Orchestrates the entire process using specialized subagents.
---

# Development Workflow

## Overview

Orchestrate a complete, structured development workflow from initial design through final delivery. This skill manages the entire process: specification generation, detailed planning, task breakdown, isolated implementation, and thorough review.

## When to Use This Skill

Use this skill when:
- Starting any substantial development work (feature, bugfix, hotfix)
- Need a structured approach with clear planning and review
- Want isolated implementation sessions to minimize context pollution
- Working on changes that benefit from systematic tracking

**Don't use for:** Trivial changes, exploratory work, or when a quick iteration is more appropriate.

## Workflow Phases

The workflow consists of five phases, orchestrated by spawning specialized subagents:

### Phase 1: Specification (Interactive)

Generate a comprehensive design specification through iterative questioning.

**What happens:**
1. Spawn a subagent to gather requirements
2. Subagent asks ONE question at a time (preferring multiple choice)
3. Refines understanding through Q&A
4. Presents specification in 200-300 word sections
5. Gets approval for each section
6. Writes final spec to `docs/development/NNN-<name>/spec.md`

**User involvement:** Answer questions, approve spec sections

### Phase 2: Planning (Automated)

Create detailed implementation plan assuming implementer has minimal context.

**What happens:**
1. Spawn a subagent with the approved spec
2. Subagent creates comprehensive plan with:
   - Files to modify
   - Code patterns to follow
   - Testing requirements
   - Step-by-step guidance
3. Writes plan to `docs/development/NNN-<name>/plan.md`

**User involvement:** Review and approve the plan

### Phase 3: Task Extraction (Automated)

Break down the plan into trackable tasks.

**What happens:**
1. Spawn a subagent with the plan
2. Subagent extracts discrete tasks
3. Links each task to specific plan sections (line numbers)
4. Writes task list to `docs/development/NNN-<name>/tasks.md`

**User involvement:** Review task list

### Phase 4: Implementation (Isolated Sessions)

Implement tasks one at a time in fresh, isolated sessions.

**Implementation Options:**

**Option A: Claude Subagent (Recommended)**
1. For each task, spawn a fresh implementation subagent
2. Subagent reads: task → spec → relevant plan section
3. Subagent implements according to plan (NO deviation)
4. Follows TDD, DRY, YAGNI principles
5. Completes one task, then stops

**Option B: External Coding Agent**
1. Provide the external agent with:
   - Task list file path: `docs/development/NNN-<name>/tasks.md`
   - Spec file path: `docs/development/NNN-<name>/spec.md`
   - Plan file path: `docs/development/NNN-<name>/plan.md`
   - Implementation instructions: `references/impl_phase.md` (from this skill)
2. Direct the agent to implement the next uncompleted task
3. Agent reads task → spec → relevant plan section → implements
4. Agent reports completion (but does NOT mark complete or commit yet)

**Option C: Human Implementation**
1. Human reads the next task from tasks.md
2. Human reads corresponding spec and plan sections
3. Human implements according to plan
4. Human reports completion for review

**User involvement:** Choose implementation method, trigger each task, provide clarifications if needed

### Phase 5: Review (Isolated Sessions)

Review completed work before marking complete.

**What happens:**
1. After implementation, spawn a review subagent
2. Subagent reads: spec → plan section → implementation
3. Checks against requirements, code quality, tests
4. Provides specific feedback OR sign-off

**User involvement:**
- Route feedback between reviewer and implementer
- Authorize task completion and commit after sign-off
- Decide when to do final review

## Using This Skill

### Quick Start

Invoke this skill and say:
> "I want to implement [feature/fix description]"

The skill will guide you through each phase, spawning the appropriate subagents.

### Manual Phase Control

You can also invoke specific phases:

- **"Start spec phase"** - Begin specification generation
- **"Generate plan"** - Create plan from existing spec
- **"Implement next task"** - Spawn implementer for next uncompleted task
- **"Review last implementation"** - Spawn reviewer for completed work
- **"Final review"** - Check all completed work together

## Subagent Orchestration

This skill leverages the Task tool to spawn specialized subagents with isolated context:

**Specification Agent** (`general-purpose`)
- Loads: Current project state, user input
- Detailed instructions in: `references/spec_phase.md`
- Interactive mode: Asks questions, gets approval

**Planning Agent** (`general-purpose`)
- Loads: Approved spec, project context
- Detailed instructions in: `references/plan_phase.md`
- Outputs: Comprehensive implementation plan

**Task Extraction Agent** (`general-purpose`)
- Loads: Approved plan
- Detailed instructions in: `references/tasks_phase.md`
- Outputs: Structured task list with line references

**Implementation Agent** (`general-purpose`)
- Loads: Single task, spec, relevant plan section
- Detailed instructions in: `references/impl_phase.md`
- Constraint: NO deviation from plan
- Fresh session per task (no context pollution)

**Review Agent** (`general-purpose`)
- Loads: Spec, plan section, implementation
- Detailed instructions in: `references/review_phase.md`
- Outputs: Specific feedback or sign-off

## File Structure

All workflow artifacts are stored in:
```
docs/development/NNN-<name>/
├── spec.md       # Design specification
├── plan.md       # Implementation plan
└── tasks.md      # Task tracking list
```

The NNN-<name> directory structure is created in Phase 1.

## Key Principles

1. **Separation of concerns** - Design, implementation, and review are distinct phases
2. **Isolated context** - Implementation and review happen in fresh sessions
3. **Plan adherence** - Implementers follow the plan strictly
4. **Incremental commits** - Each task gets its own commit after review
5. **Quality gates** - Nothing is marked complete without review sign-off

## Workflow State Management

Track workflow progress through:
- Task list checkboxes (`- [ ]` → `- [x]`)
- Commit history (one commit per completed task)
- File timestamps in docs/development/NNN-<name>/

## Advanced Usage

### Resuming After Interruption

If interrupted mid-workflow:
1. Read the task list to see completed tasks
2. Use "Implement next task" to continue
3. The subagent will pick up from the first uncompleted task

### Modifying the Plan

If the plan needs adjustment:
1. Edit `docs/development/NNN-<name>/plan.md`
2. Update affected tasks in `tasks.md`
3. Continue implementation with updated plan

### Parallel Implementation

For independent tasks, spawn multiple implementation agents in parallel:
> "Implement tasks 1, 3, and 5 in parallel"

Review each independently before marking complete.

### Using External Coding Agents

To use external agents (Cursor, Windsurf, Aider, etc.) for implementation:

1. **Complete spec, plan, and task phases** in Claude (phases 1-3)
2. **Export the context** to the external agent:
   - Task list: `docs/development/NNN-<name>/tasks.md`
   - Spec: `docs/development/NNN-<name>/spec.md`
   - Plan: `docs/development/NNN-<name>/plan.md`
   - Implementation guide: Extract `references/impl_phase.md` from this skill
3. **Instruct the external agent:**
   ```
   Read the task list at [path]. Implement the next uncompleted task.
   Follow the implementation guide in impl_phase.md strictly.
   Read the spec and the plan section referenced in the task.
   DO NOT mark the task complete or commit - report completion only.
   ```
4. **After implementation**, return to Claude for review (phase 5)
5. **Route feedback** between Claude reviewer and external implementer
6. **After sign-off**, external agent (or human) marks complete and commits

This approach allows you to:
- Use Claude for planning and review (its strength)
- Use external agents for implementation (potentially faster or with different capabilities)
- Maintain the structured workflow and quality gates

## References

Detailed instructions for each phase are in `references/`:
- `spec_phase.md` - Specification generation guidance
- `plan_phase.md` - Planning requirements and format
- `tasks_phase.md` - Task extraction rules
- `impl_phase.md` - Implementation constraints and workflow
- `review_phase.md` - Review checklist and standards

These references are loaded into subagent context as needed.
