---
name: dev-review
description: Review and validate implementation work against the spec and plan. This skill should be used after an implementer completes a task (using dev-impl) or when checking final deliverables. Use this to ensure work meets requirements before sign-off.
---

# Development Review

## Overview

Review completed implementation work to ensure it meets the specification and plan requirements. This skill provides thorough checking with fresh eyes, catching issues before work is marked complete.

## When to Use This Skill

Use this skill when:
- An implementer has completed a task and needs review before sign-off
- Checking a single task implementation (task-level review)
- Checking all completed work at the end (final review)
- Validating that implementation matches the spec and plan

## Review Types

### Type 1: Task-Level Review

Review a single completed task before it gets marked complete and committed.

**When:** After the implementer completes one task using dev-impl

**Process:**
1. Read the task list to identify which task was just completed
2. Read the spec file for overall context
3. Read the relevant plan section for this specific task
4. Examine the implementation work (code changes, tests, etc.)
5. Verify the implementation against requirements
6. Provide feedback

### Type 2: Final Review

Review all completed work at the end of the development session.

**When:** After all tasks in the task list are marked complete

**Process:**
1. Read the complete spec
2. Read the complete plan
3. Read the task list to see all completed work
4. Examine the entire implementation
5. Verify everything works together as intended
6. Generate a final report or identify remaining issues

## Review Workflow

### Step 1: Load Context

For **task-level review**, read:
1. Task list (`docs/development/NNN-<name>/tasks.md`)
2. Spec file (path at top of task list)
3. Plan section for the specific task (line numbers in task list)
4. The actual implementation (files modified)

For **final review**, read:
1. Complete spec (`docs/development/NNN-<name>/spec.md`)
2. Complete plan (`docs/development/NNN-<name>/plan.md`)
3. Task list to understand what was done (`docs/development/NNN-<name>/tasks.md`)
4. All implementation work

### Step 2: Check Against Requirements

Verify that the implementation:
1. **Meets the spec** - Does it implement what was designed?
2. **Follows the plan** - Does it follow the specified approach?
3. **Has proper tests** - Are there adequate tests? Do they pass?
4. **Follows conventions** - Does it match project code style and patterns?
5. **Is complete** - Are there any missing pieces?
6. **Works correctly** - Run tests, check functionality

### Step 3: Check Code Quality

Look for:
1. **DRY violations** - Is there unnecessary duplication?
2. **YAGNI violations** - Are there features that weren't in the plan?
3. **Poor test design** - Are tests actually testing logic or just mocking?
4. **Edge cases** - Are edge cases handled?
5. **Error handling** - Is error handling appropriate?
6. **Documentation** - Are complex parts documented?

### Step 4: Provide Feedback

**If issues are found:**
1. Document specific problems clearly
2. Reference exact locations (file:line)
3. Explain what needs to change and why
4. Prioritize issues (blocking vs. nice-to-have)
5. Return feedback to the user

**If no issues are found:**
1. Confirm the work meets all requirements
2. Explicitly state sign-off
3. For task-level review: Tell user to inform implementer to mark complete and commit
4. For final review: Generate a completion report

### Step 5: Follow-Up

**For task-level review with issues:**
- User will copy feedback to the implementer session
- Implementer will fix and resubmit
- Repeat review process

**For task-level review with sign-off:**
- Implementer marks task complete in task list
- Implementer creates commit
- Move to next task

**For final review with issues:**
- User spawns new implementer session to address issues
- Repeat until all issues resolved

**For final review with sign-off:**
- Generate final report documenting what was delivered
- Confirm all tasks complete and requirements met

## Review Principles

1. **Fresh perspective** - Review with no assumptions about what should be there
2. **Spec is truth** - The spec defines what needs to be done
3. **Plan is guidance** - The plan defines how it should be done
4. **Be thorough** - Don't just skim; actually check the work
5. **Be specific** - Vague feedback wastes everyone's time
6. **Be fair** - Don't ask for changes beyond the spec/plan without good reason

## What NOT to Do

1. **Don't accept insufficient work** - If it doesn't meet requirements, don't sign off
2. **Don't scope creep** - Don't ask for features not in the spec unless there's a genuine issue
3. **Don't skip testing** - Always verify tests exist and pass
4. **Don't assume** - Actually read the code; don't just trust it works
5. **Don't be vague** - "This looks wrong" is not helpful; "Line 42: this should handle null values" is helpful

## Final Report Format

For final reviews that pass, generate a report like:

```markdown
# Final Review Report: [Feature/Fix Name]

**Date:** [Date]
**Spec:** docs/development/NNN-<name>/spec.md
**Plan:** docs/development/NNN-<name>/plan.md
**Tasks:** docs/development/NNN-<name>/tasks.md

## Summary

[Brief overview of what was implemented]

## Review Results

✅ All requirements from spec met
✅ Implementation follows plan
✅ Tests present and passing
✅ Code quality acceptable
✅ All tasks completed

## Deliverables

- [List of files created/modified]
- [Number of tests added]
- [Any documentation updated]

## Sign-Off

Implementation complete and ready for integration.
```

## Context Awareness

This skill is part of a larger workflow:
- **dev-spec** creates the spec, plan, and task list
- **dev-impl** implements individual tasks
- **dev-review** (this skill) reviews completed work

The reviewer role is deliberately independent and critical. Provide honest assessment without worrying about hurting feelings - the goal is quality work.
