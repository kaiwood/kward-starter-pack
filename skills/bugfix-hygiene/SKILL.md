---
name: bugfix-hygiene
description: Use during iterative bug fixing, especially after failed guesses, multiple attempted fixes, or when the user confirms the bug now works. Keep the working diff clean after each attempt, remove safe failed-hypothesis leftovers, and summarize final cleanup.
---

# Bugfix Hygiene

## Goal

Keep iterative bugfixes focused and understandable.

When debugging involves guesses or multiple attempts, clean up safely as you go so the final diff contains only the real fix, required supporting changes, and useful regression coverage.

## Use This Skill When

- A bugfix involves multiple hypotheses or attempted fixes.
- The user says a previous fix did not work.
- Tests or manual checks fail after an attempted fix.
- The user confirms the bug now works after iterative debugging.
- The diff contains temporary logs, speculative guards, abandoned changes, or unrelated edits.

## Core Rules

- Only remove changes that are clearly safe to remove.
- Only clean up changes introduced during the current bugfix.
- Never revert pre-existing user changes.
- Do not remove a change just because it looks indirect.
- Preserve multi-step fixes, even if one part only enables another.
- If a change might be required but the reason is unclear, keep it and call it out.
- Prefer reverting experimental leftovers over adding new abstractions.
- Do not broaden the fix during cleanup.

## During Bugfixing

At the start of an iterative bugfix, inspect or remember the existing dirty state when practical:

- note files already modified before your changes
- avoid overwriting or reverting user work
- keep changes scoped to the bug

After each attempted fix or failed verification:

1. Identify what hypothesis the attempt tested.
2. Keep changes still needed for the next attempt.
3. Remove obvious artifacts from abandoned attempts:
   - debug logging
   - temporary tracing
   - throwaway comments
   - unused imports, variables, functions, or helpers
   - speculative guards that did not address the reproduced bug
   - unrelated formatting or refactors
4. Re-run the smallest relevant verification when practical.

## Final Cleanup

When the user confirms the fix works, or before presenting the final result:

1. Inspect the full diff.
2. Identify the confirmed root cause.
3. Classify changed areas as:
   - root-cause fix
   - required supporting change
   - regression test
   - verification/tooling change
   - debug artifact
   - failed-hypothesis leftover
   - unrelated incidental change
4. Remove only clearly unnecessary artifacts or leftovers.
5. Keep changes required for final behavior or regression coverage.
6. Run focused verification when practical.

## Usually Safe To Remove

When confirmed unnecessary:

- console/debug logging
- temporary tracing
- abandoned comments
- unused variables/functions/imports
- speculative guards unrelated to the confirmed root cause
- formatting churn unrelated to touched logic
- test edits that weaken assertions or merely mask the bug

## Not Safe To Remove Without Proof

Be careful with:

- compatibility guards
- error handling
- timing/order changes
- state initialization changes
- test fixture changes
- changes that only matter in edge cases
- multi-file fixes where one part enables another
- changes in files modified before the current bugfix

## Final Report

Keep the final report short. Include:

- root cause
- final required changes
- removed leftovers, if any
- verification run
- retained uncertain changes, if any, and why

Example:

```text
Cleaned up the iterative bugfix diff:
- Root cause: stale state was read before session restore completed.
- Kept: restore ordering fix and regression test.
- Removed: temporary logging and an unused guard from an earlier hypothesis.
- Verification: npm test passed.
```

If nothing was safe to remove:

```text
I checked the diff for failed-guess leftovers. Nothing was clearly safe to remove without risking the fix.
```
