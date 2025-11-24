# Runbook

This document describes how to build, test, and validate the work in this development session, as well as when to pause for human feedback.

## Build Instructions

[How to build/compile the code]

```bash
# Example:
npm install
npm run build
```

## Test Instructions

[How to run tests]

```bash
# Example:
npm test
npm run test:integration
```

## Run Instructions

[How to run the application locally for manual testing]

```bash
# Example:
npm run dev
# Then visit http://localhost:3000
```

## Validation Steps

[Any additional validation steps beyond automated tests]

- [ ] Manual testing checklist item 1
- [ ] Manual testing checklist item 2
- [ ] Performance check
- [ ] Security review

## Feedback Points

These are structured points where the agent must pause and ask for human input during implementation.

### After [specific milestone or step]
**Purpose:** [Why feedback is needed at this point]
**Questions to ask:** [What specifically to verify or get approval on]

### Before [specific action]
**Purpose:** [Why approval is needed before proceeding]
**Questions to ask:** [What to confirm with human]

### When [specific condition occurs]
**Purpose:** [Why this situation requires human input]
**Questions to ask:** [What guidance is needed]

---

## Example Feedback Points

### After implementing core authentication logic
**Purpose:** Verify the authentication approach matches expectations before building dependent features
**Questions to ask:**
- Does the login flow work as expected?
- Should we add any additional authentication factors?

### Before making database schema changes
**Purpose:** Schema changes are hard to reverse, need approval
**Questions to ask:**
- Review proposed schema changes
- Confirm migration strategy

### When encountering an unclear requirement
**Purpose:** Avoid making assumptions about product behavior
**Questions to ask:**
- Clarify the expected behavior for [specific scenario]
- Get decision on [unclear aspect]
