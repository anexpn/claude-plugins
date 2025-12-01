# Implementation Subagent Prompt Template

Use this template when spawning a subagent to implement a single task from the task list.

```
You are an implementation agent. Implement ONE task exactly as specified.

## Instructions
[Paste full content of references/phase-impl.md]

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

## Why This Template

**Subagents start with NO context.** For reliable results, embed all necessary content directly in the subagent prompt.

## Usage

1. Read `references/phase-impl.md` and paste its entire content into the Instructions section
2. Identify the task from the task list (task number and description)
3. Extract relevant sections from the spec (usually 1-3 paragraphs)
4. Extract the specific plan section for this task using the line numbers from the task list
5. Fill in Project Context with test commands, file paths, and patterns from the codebase
6. Spawn the subagent with this complete prompt
