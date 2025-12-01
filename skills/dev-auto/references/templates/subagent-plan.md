# Planning Subagent Prompt Template

Use this template when spawning a subagent to create an implementation plan from an approved specification.

```
You are a planning agent. Create a comprehensive implementation plan.

## Instructions
[Paste full content of references/phase-plan.md]

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

## Why This Template

**Subagents start with NO context.** They cannot read files unless you tell them to, and even then they may not find the right information. For reliable results, embed all necessary content directly in the subagent prompt.

## Usage

1. Read `references/phase-plan.md` and paste its entire content into the Instructions section
2. Read the approved spec file and paste its entire content into the Approved Specification section
3. Fill in the Project Context with relevant details from the codebase
4. Spawn the subagent with this complete prompt
