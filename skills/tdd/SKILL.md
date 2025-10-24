---
name: tdd
description: Test-Driven Development workflow for implementing new features and bug fixes. Use this skill when implementing any new feature or fixing any bug to ensure proper test coverage and incremental development through the red-green-refactor cycle.
---

# Test-Driven Development (TDD)

## Overview

This skill enforces Test-Driven Development methodology for all feature implementations and bug fixes. TDD ensures code correctness through a disciplined workflow of writing tests first, implementing minimal code to pass those tests, and then refactoring.

## When to Use This Skill

Use this skill whenever:
- Implementing a new feature
- Fixing a bug
- Adding new functionality to existing code
- Modifying behavior that can be tested

## TDD Workflow

Follow this five-phase workflow for EVERY new feature or bugfix:

### Phase 1: Write a Failing Test

Write a test that correctly validates the desired functionality. The test should:
- Clearly express the expected behavior
- Cover the specific feature or bug being addressed
- Be focused and minimal (test one thing)
- Use descriptive names that explain what behavior is being tested

Example test scenarios:
- For a feature: Test that the new function returns expected output for given input
- For a bug: Test that reproduces the bug (should fail before the fix)

### Phase 2: Run the Test to Confirm Failure

Execute the test suite to verify the new test fails as expected. This confirms:
- The test is actually testing something
- The test framework is working correctly
- The feature/fix hasn't already been implemented

If the test passes unexpectedly, revisit the test to ensure it's testing the right thing.

### Phase 3: Write Minimal Implementation

Write ONLY enough code to make the failing test pass. Resist the urge to:
- Add extra features or functionality
- Over-engineer the solution
- Implement related but untested behavior

The implementation should be the simplest possible code that makes the test green.

### Phase 4: Run the Test to Confirm Success

Execute the test suite again to verify:
- The new test now passes
- All existing tests still pass
- No regressions were introduced

If tests fail, fix the implementation (not the test) until all tests pass.

### Phase 5: Refactor While Keeping Tests Green

With working tests in place, refactor the code to improve:
- Code clarity and readability
- Elimination of duplication
- Better structure and organization
- Performance (if needed)

After each refactoring change:
- Run the test suite immediately
- Ensure all tests remain green
- If tests fail, revert the change and try a different approach

## Key Principles

- **Test First, Always**: Never write production code without a failing test
- **Minimal Implementation**: Write only enough code to pass the current test
- **Keep Tests Green**: All tests must pass before moving to the next feature
- **Incremental Development**: Build functionality incrementally through small test-code cycles
- **Refactor Fearlessly**: With comprehensive tests, refactoring is safe and encouraged
