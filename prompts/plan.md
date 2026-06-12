---
description: Create a concise implementation plan before coding; do not implement until confirmed
argument-hint: "<task-or-change>"
---

Plan this implementation request:

$ARGUMENTS

## Rules

- Do not implement until the user explicitly confirms.
- First understand the goal, scope, constraints, and success criteria.
- If required details are missing, ask direct clarification questions before drafting the plan.
- Use the `ask_user_question` tool for every clarification question.
- Present exactly 2 options for each `ask_user_question` question. Keep questions single-select, do not use previews, and do not add an "Other" or "Type something" option; the tool provides the custom answer row automatically.
- If more than 4 clarifications are needed, ask the most important 4 first, then ask follow-ups after the user answers.
- Ask all questions needed; do not hide unresolved issues in an "Open Questions" section.
- Do not assume requirements, choose behavior, or invent APIs unless the assumption is trivial and low-risk.
- Prioritize clarification about behavior, scope, acceptance criteria, constraints, data/API changes, UI/UX, errors, tests, and compatibility risks.

## Output

Keep the plan concise. Include only useful sections:

- **Goal**: what will change.
- **Known Context**: confirmed or discovered facts.
- **Approach**: implementation steps.
- **Files/Areas**: likely affected paths/components.
- **Behavior Changes**: user-visible or system changes.
- **Tests/Verification**: automated/manual checks.
- **Risks**: known tradeoffs or uncertainties that do not require clarification first.
- **Readiness**: whether it is ready to implement and why.

Do not include an "Open Questions" section. If non-trivial questions remain, ask them instead of providing a plan.

End complete plans by asking: **Should I implement this plan now?**
