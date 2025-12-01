# Task Extraction Subagent Prompt Template

Use this template when spawning a subagent to extract a task list from an implementation plan.

```
You are a task extraction agent. Break down the plan into trackable tasks.

## Instructions
[Paste full content of references/phase-tasks.md]

## Implementation Plan
[Paste full content of docs/development/NNN-<name>/plan.md]

## Output
Write the task list to: docs/development/NNN-<name>/tasks.md
```

## Why This Template

**Subagents start with NO context.** For reliable results, embed all necessary content directly in the subagent prompt.

## Usage

1. Read `references/phase-tasks.md` and paste its entire content into the Instructions section
2. Read the plan file and paste its entire content into the Implementation Plan section
3. Spawn the subagent with this complete prompt
