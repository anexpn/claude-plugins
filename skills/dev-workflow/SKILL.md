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

## Architecture: Interactive vs Automated Phases

This workflow has two types of phases:

**Interactive phases (run in main conversation):**
- Specification - Requires back-and-forth Q&A with user
- Review - Requires routing feedback and getting sign-off

**Automated phases (run as subagents):**
- Planning - Transforms spec into detailed plan
- Task extraction - Breaks plan into trackable tasks
- Implementation - Executes one task per subagent

**Why this split:** Subagents cannot interact with the user. They run autonomously and return a single result. Interactive phases must run in the main conversation.

## Workflow Phases

### Phase 1: Specification (Interactive - Main Conversation)

Generate a comprehensive design specification through iterative questioning.

**How to run:** Follow the instructions in `references/spec_phase.md` directly in the main conversation.

**Process:**
1. Examine the project to understand current state
2. Ask ONE question at a time (preferring multiple choice)
3. Refine understanding through Q&A until certain
4. Present specification in 200-300 word sections
5. Get approval for each section before proceeding
6. Write final spec to `docs/development/NNN-<name>/spec.md`

**User involvement:** Answer questions, approve spec sections

### Phase 2: Planning (Automated - Subagent)

Create detailed implementation plan assuming implementer has minimal context.

**How to run:** Spawn a subagent with rich context embedded in the prompt.

**Subagent prompt must include:**
1. Full content of the approved spec (not just the path)
2. Project structure summary (key directories, technologies)
3. Relevant existing code patterns to follow
4. The complete instructions from `references/plan_phase.md`
5. Output path: `docs/development/NNN-<name>/plan.md`

**User involvement:** Review and approve the plan

### Phase 3: Task Extraction (Automated - Subagent)

Break down the plan into trackable tasks.

**How to run:** Spawn a subagent with rich context embedded in the prompt.

**Subagent prompt must include:**
1. Full content of the plan (not just the path)
2. The complete instructions from `references/tasks_phase.md`
3. Output path: `docs/development/NNN-<name>/tasks.md`

**User involvement:** Review task list

### Phase 4: Implementation (Automated - Subagent per Task)

Implement tasks one at a time in fresh, isolated sessions.

**Implementation Options:**

**Option A: Claude Subagent (Recommended)**

For each task, spawn a fresh subagent with rich context.

**Subagent prompt must include:**
1. The specific task description and number
2. Relevant sections from the spec (not the whole spec unless needed)
3. The specific plan section for this task (extract by line numbers)
4. The complete instructions from `references/impl_phase.md`
5. Key project context: file locations, patterns, test commands

The subagent implements according to plan (NO deviation), follows TDD/DRY/YAGNI, completes one task, then stops.

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

### Phase 5: Review (Interactive - Main Conversation)

Review completed work before marking complete.

**How to run:** Follow the instructions in `references/review_phase.md` directly in the main conversation.

**Process:**
1. Read the spec, plan section, and implementation
2. Check against requirements, code quality, tests
3. Provide specific feedback OR sign-off
4. Route feedback to implementer if issues found
5. After sign-off, authorize task completion and commit

**User involvement:**
- Trigger review after implementation completes
- Authorize task completion and commit after sign-off
- Decide when to do final review

## Using This Skill

### Quick Start

Invoke this skill and say:
> "I want to implement [feature/fix description]"

The skill will guide you through each phase, running interactive phases in the main conversation and spawning subagents for automated phases.

### Manual Phase Control

You can also invoke specific phases:

- **"Start spec phase"** - Begin specification (runs in main conversation)
- **"Generate plan"** - Create plan from existing spec (spawns subagent)
- **"Extract tasks"** - Break plan into tasks (spawns subagent)
- **"Implement next task"** - Implement next uncompleted task (spawns subagent)
- **"Review last implementation"** - Review completed work (runs in main conversation)
- **"Final review"** - Check all completed work together (runs in main conversation)

## Subagent Context Requirements

**Critical:** Subagents start with NO context. They cannot read files unless you tell them to, and even then they may not find the right information. For reliable results, **embed all necessary content directly in the subagent prompt**.

### Planning Subagent Prompt Template

```
You are a planning agent. Create a comprehensive implementation plan.

## Instructions
[Paste full content of references/plan_phase.md]

## Approved Specification
[Paste full content of docs/development/NNN-<name>/spec.md]

## Project Context
- Technologies: [list]
- Key directories: [list with descriptions]
- Relevant patterns: [describe existing patterns to follow]
- Test command: [command]

## Output
Write the plan to: docs/development/NNN-<name>/plan.md
```

### Task Extraction Subagent Prompt Template

```
You are a task extraction agent. Break down the plan into trackable tasks.

## Instructions
[Paste full content of references/tasks_phase.md]

## Implementation Plan
[Paste full content of docs/development/NNN-<name>/plan.md]

## Output
Write the task list to: docs/development/NNN-<name>/tasks.md
```

### Implementation Subagent Prompt Template

```
You are an implementation agent. Implement ONE task exactly as specified.

## Instructions
[Paste full content of references/impl_phase.md]

## Your Task
Task [N]: [description]

## Relevant Specification
[Paste relevant sections from spec.md]

## Plan Section for This Task
[Paste lines XX-YY from plan.md]

## Project Context
- Test command: [command]
- Files to modify: [list from plan]
- Patterns to follow: [describe]

## Constraints
- DO NOT DEVIATE FROM THE PLAN
- Implement this ONE task only
- Report completion but do NOT mark complete or commit
```

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
2. **Interactive vs automated** - User-facing phases run in main conversation; automated phases use subagents
3. **Rich subagent context** - Embed all necessary content in subagent prompts, not just file paths
4. **Plan adherence** - Implementers follow the plan strictly
5. **Incremental commits** - Each task gets its own commit after review
6. **Quality gates** - Nothing is marked complete without review sign-off

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
- `spec_phase.md` - Specification generation guidance (used directly in main conversation)
- `plan_phase.md` - Planning requirements and format (embedded in subagent prompt)
- `tasks_phase.md` - Task extraction rules (embedded in subagent prompt)
- `impl_phase.md` - Implementation constraints and workflow (embedded in subagent prompt)
- `review_phase.md` - Review checklist and standards (used directly in main conversation)

**For interactive phases:** Read the reference file and follow its instructions directly.
**For automated phases:** Read the reference file and embed its content in the subagent prompt.
