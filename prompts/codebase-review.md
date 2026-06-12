---
description: Review a codebase or scope for maintainability, dead code, duplication, and practical cleanup
argument-hint: "[scope-or-focus]"
---

Review this codebase or scope:

$ARGUMENTS

## Rules

- Report only. Do not edit, refactor, or apply patches.
- Treat the repo as production code.
- Cite concrete files, modules, commands, and observed patterns.
- Prefer deletion and simplification over new abstractions.
- Avoid speculative rewrites or “frameworkizing”.
- Do not invent service layers unless they clearly reduce duplication or clarify ownership.
- Prefer small, local improvements with measurable value.
- If scope is unclear, ask one focused clarification question.

## Focus

Prioritize:

1. Correctness or broken behavior.
2. Dead, unreachable, duplicated, or unused code.
3. Unnecessary complexity or accidental abstractions.
4. Architecture boundaries and ownership clarity.
5. Readability, consistency, important test gaps, and tooling friction.
6. Performance-sensitive hot paths or repeated work.
7. Naming drift and outdated terminology after renames/migrations.

Look for:

- duplicated logic, types, parsers, validation, config access, or render/message handling
- unclear ownership or files mixing orchestration with low-level mechanics
- stale compatibility layers, dead code, and legacy leftovers
- practical helper extraction or consolidation opportunities
- tests/tooling gaps that make safe cleanup harder

## Process

1. Read project guidance, README, manifests, docs, and build/test config as relevant.
2. Map entrypoints, top-level domains, runtime boundaries, generated output to ignore, and tests/tooling.
3. Inspect implementation deeply enough to identify real issues, not style preferences.
4. Run safe verification when practical: typecheck, compile, tests, lint, or configured dead-code/dependency checks.
5. Separate command/tool failures from actual code findings.

## Output

Produce a concise but concrete report. Use sections as useful:

### Scope

- repo/scope reviewed
- commands run
- areas inspected
- skipped/generated areas

### Architecture Summary

- structure
- responsibilities
- runtime boundaries
- coupling
- ownership observations

### Findings

For each finding include:

- Severity: low / medium / high
- Type: correctness / duplication / dead code / ownership / simplification / naming / performance / tests-tooling
- Files/modules involved
- Problem
- Why it matters
- Suggested simplification or cleanup
- Risk level
- Estimated scope/diff size
- Suggested timing: now / later / ignore

### Dead/Leftover Code Candidates

- why removable/stale
- what to verify before removal

### Simplification Opportunities

- concrete ways to reduce code or concepts
- possible helper extraction/consolidation
- opportunities to merge duplicated logic safely

### Performance/Hot Path Notes

- repeated work
- unnecessary rerenders
- avoidable allocations/scans
- cache opportunities
- scaling risks

### Verification Notes

- passed/failed/skipped commands
- relevant diagnostics observations

### Recommended Cleanup Plan

Prefer staged cleanup:

1. safe deletions
2. duplicate helper consolidation
3. ownership cleanup
4. tests/tooling cleanup
5. optional larger refactors

### Risks / Questions

- areas needing human judgment
- risky migrations
- places where behavior/contracts are unclear

If a section has no meaningful findings, say so briefly instead of inventing issues.
