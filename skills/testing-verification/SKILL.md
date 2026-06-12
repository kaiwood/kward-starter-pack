---
name: testing-verification
description: Use when adding logic, fixing bugs, changing tests, or finishing implementation work. Guides focused test coverage, safe verification, and avoids weakening tests to hide failures.
---

# Testing Verification

## Goal

Verify behavior with the smallest useful checks, and keep tests trustworthy.

Use tests to prove the change works without overfitting to implementation details or weakening coverage.

## Use This Skill When

- Adding or changing behavior.
- Fixing a bug.
- Editing tests or fixtures.
- Refactoring logic.
- Finishing implementation work.
- Deciding which verification command to run.

## Core Rules

- Test behavior, not private implementation details.
- Add or update tests for new logic when practical.
- Prefer focused tests near the changed code.
- Do not weaken assertions just to make tests pass.
- Do not delete failing tests unless they are obsolete and the behavior change is intentional.
- Fix production code before changing tests.
- Keep tests deterministic and independent of external services when practical.
- Separate real code failures from tooling, environment, or flaky-test failures.

## Test Changes

When changing tests:

- Preserve the original behavioral intent unless the requested behavior changed.
- Prefer clearer setup over broader mocks.
- Avoid snapshots for behavior that needs precise assertions.
- Avoid asserting incidental ordering, formatting, or internals unless that is the contract.
- Add regression coverage for confirmed bugs when practical.
- Keep fixtures minimal and readable.

## Verification Strategy

Run the smallest relevant check first, then broaden if needed.

Typical order:

1. Targeted unit test or focused test file.
2. Typecheck/compile for touched language.
3. Related integration or package tests.
4. Full test suite only when the change is broad or risky.

If a command is expensive, unavailable, flaky, or blocked by environment, say so and explain what was run instead.

## Before Finishing

Before finalizing an implementation or bugfix:

1. Identify the behavior changed.
2. Confirm whether test coverage exists or was added.
3. Run relevant verification when practical.
4. Check that tests were not weakened to pass.
5. Summarize verification clearly.

## Failure Handling

When tests fail:

- Read the failure before changing code.
- Identify whether the failure is caused by the current change, existing behavior, test fragility, or environment.
- Prefer fixing the root cause over updating expected output.
- If updating expected output, explain why the new output is correct.
- Do not mask failures with broad skips, retries, or looser assertions unless explicitly justified.

## Final Report

Keep the verification summary short:

```text
Verification:
- Added regression test for the missing restore case.
- Ran `npm test -- chatSession`: passed.
- Skipped full suite because change was isolated to session state.
```

If no tests were run:

```text
Verification not run: no focused test exists and full suite requires unavailable service X.
```
