---
name: code-structure
description: Use when improving architecture, clarifying ownership, separating orchestration from mechanics, reducing duplication, or deciding where code should live.
---

# Code Structure

## Principle

Prefer architecture that makes ownership obvious.

Keep orchestration separate from reusable mechanics.

- Orchestration owns:
  - product meaning
  - workflow/state transitions
  - auth/policy decisions
  - user-facing behavior
  - coordination between lower-level pieces

- Shared helpers/services own:
  - reusable operations
  - provider/SDK/API interactions
  - parsing/formatting
  - low-level mechanics
  - isolated side-effect wrappers

## Architecture Goals

Good structure should:

- make state ownership clear
- keep side effects near runtime boundaries
- keep orchestration readable
- keep reusable mechanics small and explicit
- reduce coupling between unrelated domains
- make tests easier without excessive mocking
- preserve behavior while improving structure

## Use This Skill When

- Improving architecture or module boundaries.
- Deciding where code should live.
- Similar logic exists in 2+ places.
- A bug fix should apply to multiple workflows.
- A new feature shares mechanics with existing flows.
- A file mixes orchestration and low-level implementation details.
- Ownership, state flow, or dependency direction feels unclear.

## Dependency Direction

Prefer dependencies flowing from product-specific orchestration into lower-level helpers.

Lower-level modules should not import orchestration, UI, runtime globals, or policy decisions.

If two modules depend on each other conceptually, identify the shared concept and extract only that concept.

## Placement Checklist

Before moving or extracting code, ask:

- Who owns this state?
- Is this product behavior or reusable mechanics?
- Is this used by 2+ callers, or does it define a real boundary?
- Would extracting this reduce concepts, or add one?
- Can this be tested more easily after the change?
- Does the new module name describe a real responsibility?

## Avoid

- Creating service layers for one caller.
- Generic “god services”.
- Abstractions that add more concepts than they remove.
- Refactoring just for aesthetics.
- Moving code only to make architecture look cleaner.
- Letting utility files become junk drawers.

## Rule of Thumb

- “What this flow means” → orchestration.
- “How this operation works” → shared helper/service.
- “Who owns this state?” → keep it near the owner.
- “Where does the side effect happen?” → keep it near the boundary.

## Preferred Refactor Style

1. Keep behavior working first.
2. Identify the ownership or duplication problem.
3. Extract only the repeated mechanic or real shared concept.
4. Use explicit inputs and structured outputs.
5. Replace one caller, verify, then migrate others.
6. Delete old duplicated code.

## Good Signs

- Less total code.
- Clearer ownership.
- Simpler call sites.
- Dependencies point one way.
- Shared fixes apply everywhere.
- Easier testing.

## Bad Signs

- More layers than before.
- New abstractions with one caller.
- Services mutating unrelated state.
- “Utility” files becoming junk drawers.
- Hidden global behavior.
- Circular or domain-crossing dependencies.

## Mental Model

```text
Make ownership obvious.
Keep behavior stable.
Extract only repeated mechanics or real boundaries.
Prefer deletion and consolidation over abstraction.
```
