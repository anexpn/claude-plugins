# Implementation Session Phase

When materials already exist in the docs folder, start an implementation session to continue the development work.

## Session Flow

1. Load context from existing materials
2. Enter plan mode and create session plan
3. Implement according to plan
4. Update progress and other materials

## 1. Load Context

Read all existing materials in order:

1. **problem_statement.md** - Understand the problem scope
2. **decisions.md** - Understand what choices have been made
3. **runbook.md** - Understand how to validate work and when to get feedback
4. **progress.md** - Understand what has been done and what's outstanding

Additionally, check for existing plan files (plan-1.md, plan-2.md, etc.) to understand previous approaches.

## 2. Create Session Plan

Enter plan mode and create a plan for this implementation session:

**Plan should include:**
- What will be accomplished in this session
- Specific steps to take
- Dependencies between steps
- Expected validation points from runbook.md
- Outstanding questions or uncertainties

**Determine session number:**
- Count existing plan-N.md files
- Next session number = max(N) + 1
- If no plan files exist, this is session 1

**After plan is approved by human:**
- Save plan as `plan-N.md` where N is the session number
- Proceed with implementation

## 3. Implement According to Plan

Follow the plan created in step 2.

**During implementation:**

- **Respect feedback points:** When reaching a feedback point defined in runbook.md, MUST pause and ask for human input
- **Document new decisions:** If new unclear aspects arise, update decisions.md and ask for human input
- **Update runbook if needed:** If build/test/validation steps change, update runbook.md
- **Follow existing decisions:** Use the choices recorded in decisions.md

**Testing and validation:**
- Follow the build/test instructions in runbook.md
- Perform validation steps defined in runbook.md
- Ensure all tests pass before completing session

## 4. Update Progress

At the end of the session, update progress.md with a new entry:

**Entry format:**
```markdown
## Session N (YYYY-MM-DD)

### Accomplished
- [What was implemented/completed]
- [Tests that now pass]
- [Issues that were resolved]

### Outstanding
- [What still needs to be done]
- [Known issues or blockers]

### Questions
- [New unclear aspects that need decisions]
- [Uncertainties or concerns]
```

**Also update if needed:**
- **decisions.md** - If new decisions were made
- **runbook.md** - If validation steps changed

## Session Completion

After updating all materials:
1. Verify all changes are recorded in progress.md
2. Verify any new decisions are in decisions.md
3. Verify runbook.md is current
4. Inform human that the session is complete
5. Summarize what was accomplished and what's next
