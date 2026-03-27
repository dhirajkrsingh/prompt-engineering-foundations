# Example 2: Grounded Code Generation Without Invented Details

## Problem

Code generation prompts often fail because they ask for implementation before establishing what already exists.

## Failure Pattern

```text
Write a service class for invoice reconciliation.
```

This invites the model to invent:

- folder structure
- class naming conventions
- logging style
- error types
- persistence layer
- test style

## Better Strategy

Split the interaction into two stages.

### Stage 1: Discovery Prompt

```text
You are helping with code generation in an existing TypeScript repo.

Before suggesting code, inspect the existing structure and answer:
1. Which files likely own invoice reconciliation?
2. What naming conventions are used for services and errors?
3. What database or repository abstraction is already present?
4. What test framework is in use?

Constraints:
- Use only evidence from the current repo.
- If a detail is not visible, say "not confirmed".
```

### Stage 2: Implementation Prompt

```text
Using only the confirmed findings above, implement a new invoice reconciliation service that matches the existing project conventions.

Return:
1. Files to change
2. Minimal implementation plan
3. Code
4. Tests

Constraints:
- Do not add packages.
- Do not create abstractions that are not already used in the repo.
- If a dependency is not confirmed, stop and flag the missing information.
```

## Why Two Stages Work

The first prompt forces evidence gathering. The second prompt consumes a constrained fact set. This reduces the model's freedom to improvise unsupported details.

## Hallucination-Reduction Moves

1. Ask for confirmed findings first.
2. Use those findings as the only allowed basis for generation.
3. Forbid invention explicitly.
4. Require the model to stop when a needed dependency is unconfirmed.

## Good Constraint Language

Prefer:

```text
If the repository does not expose enough information to determine the correct implementation, do not guess. State the missing dependency or file explicitly.
```

Avoid:

```text
Try your best.
```

"Try your best" often means "fill missing facts with plausible fiction."