---
description: Deeply investigate a bug or strange behavior and report root cause; do not implement
argument-hint: "<bug-or-behavior>"
---
Investigate this bug or strange behavior:

$ARGUMENTS

## Rules

- Report only. Do not implement, edit files, or apply patches.
- Search deeply enough to explain why it happens.
- Prefer evidence from code, tests, logs, docs, and reproducible commands.
- Cite concrete files, functions, commands, and observed behavior.
- Separate confirmed facts from hypotheses.
- If the issue is unclear, ask one focused clarification question.
- Do not guess missing requirements.

## Process

1. Reproduce or trace the behavior when practical.
2. Find the relevant entrypoints, data flow, and state changes.
3. Compare intended behavior with actual behavior.
4. Identify the root cause or strongest supported hypothesis.
5. Suggest the smallest safe fix.
6. Do not implement until the user confirms.

## Output

Use concise sections as useful:

- **Summary**: direct root-cause answer.
- **Observed Behavior**: what happens and how it was verified.
- **Expected Behavior**: what should happen.
- **Where It Occurs**: files/functions/flow involved.
- **Why It Occurs**: root cause and evidence.
- **Suggested Fix**: minimal change, no implementation yet.
- **Verification**: tests or manual checks to confirm the fix.
- **Risks/Open Questions**: uncertainty or tradeoffs.

End by asking: **Should I implement the suggested fix now?**
