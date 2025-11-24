# Initial Setup Phase

When starting a new development session (no materials exist in the docs folder), guide the human through creating the foundational documents through structured Q&A.

## Phase Flow

1. Create problem_statement.md
2. Create decisions.md
3. Create runbook.md
4. Create empty progress.md

## 1. Problem Statement Creation

**Purpose:** Define what problem is being solved, providing scope without prescribing solution.

**Questions to ask:**
- "What problem are you trying to solve?"
- "What is the scope of this work? What's explicitly out of scope?"
- "What does success look like for this work?"
- "Are there any constraints or requirements I should know about?"

**Format:** Use the template in `template-problem_statement.md`

**Key principle:** Focus on the WHAT and WHY, not the HOW.

## 2. Decisions Creation

**Purpose:** Explicitly capture human choices on unclear aspects. NO assumptions or defaults.

**Critical rule:** MUST ask about every unclear aspect. MUST NOT assume "sensible defaults" or "de facto standards."

**Areas to probe:**
- Language/framework choices
- Library/dependency choices
- Architectural patterns
- Data storage approaches
- Testing strategies
- Error handling approaches
- Security considerations

**Questions format:**
- "Which [language/library/pattern] should be used for X?"
- "How should Y be handled?"
- "What approach should be taken for Z?"

**For each unclear aspect:**
1. Explain why a decision is needed
2. Present options if helpful (but don't bias toward one)
3. Ask for the human's choice
4. Record the decision and rationale in decisions.md

**Format:** Use the template in `template-decisions.md`

**Key principle:** Capture explicit human choices, not assumptions.

## 3. Runbook Creation

**Purpose:** Document how to validate work and when to get feedback during implementation.

**Questions to ask:**
- "How should this code be built/compiled?"
- "How should this code be run/tested?"
- "Are there any other validation steps I should perform?"
- "At what points during implementation should I pause and ask for your feedback?"

**Format:** Use the template in `template-runbook.md`

**Key sections:**
- Build instructions
- Test instructions
- Feedback points (structured list of when to pause for human input)
- Other validation steps

**Key principle:** Establish clear validation and feedback loops.

## 4. Progress Initialization

Create an empty progress.md file using the template in `template-progress.md`. This will be populated after the first implementation session.

## Completing Initial Setup

After creating all four files, inform the human that the setup is complete and ask if they want to start the first implementation session now or later.
