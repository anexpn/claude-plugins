---
argument-hint: files | components | config | diagram | git | test
description: Analyze codebase structure and dependencies for experienced developers
---

# Explore: ${ARGUMENTS:-files}

Analyze and synthesize information about the codebase for experienced developers.

---

## Available Aspects

Use `/explore <aspect>` where aspect is one of:

- **files**: Show the 10 most important files for understanding this codebase and explain why each is critical
- **components**: Map out the dependencies between the main components - which modules depend on which others
- **config**: Identify the key configuration files and explain what each controls
- **diagram**: Create a detailed diagram of how the main components interact
- **git**: Analyze the git history to show the most frequently changed files and what they suggest about the system's evolution
- **test**: Show the testing strategy - where are tests located and how to run them

---

## Your Task

The user wants to explore: **${ARGUMENTS:-files}**

Provide a comprehensive analysis for this aspect. Use the Explore agent (Task tool with subagent_type=Explore) for thorough investigation.
