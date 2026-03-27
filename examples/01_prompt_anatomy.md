# Example 1: Prompt Anatomy For A Real Developer Task

## Goal

Take a vague prompt and turn it into a low-hallucination prompt.

## Weak Prompt

```text
Fix the auth bug and add tests.
```

## Why It Fails

1. No role is defined.
2. No context is provided.
3. The model has to guess what the auth bug is.
4. The test framework is unspecified.
5. The acceptable scope is unclear.

This is exactly the kind of prompt that causes the model to invent routes, middleware, files, or package usage.

## Improved Prompt

```text
# Role
You are a senior backend engineer working in an existing Node.js authentication service.

# Context
Use only the following facts:
- The bug occurs in `src/auth/session.ts`
- The failure happens when expired refresh tokens are accepted as valid
- Existing tests live in `tests/auth/session.test.ts`
- The project uses Vitest

# Task
Find the root cause of the expired refresh token bug, implement the smallest safe fix, and add focused tests for the failure case.

# Output Format
Return:
1. Root cause
2. Proposed fix
3. Tests to add
4. Risks or assumptions

# Constraints
- Do not invent new auth flows or new packages.
- Keep the fix limited to the affected session validation path unless the evidence proves otherwise.
- If a required file is missing, state that explicitly instead of guessing.

# Validation Criteria
Before finalizing, verify that:
1. The fix directly addresses expired refresh token acceptance.
2. The proposed tests cover both the failing case and a valid-token case.
3. Any assumption is labeled explicitly.
```

## Why The Improved Prompt Is Better

| Prompt Section | What It Changed |
|----------------|-----------------|
| Role | Forces production-minded debugging behavior |
| Context | Anchors the model in real files and facts |
| Task | Defines diagnosis, fix, and tests in one bounded unit |
| Output Format | Produces immediately reviewable output |
| Constraints | Prevents speculative redesign |
| Validation Criteria | Forces a final compliance check |

## Practical Rule

If you expect a precise answer, every vague noun in your prompt should be treated as a defect until it is either defined or intentionally left open.

Examples of vague nouns:

- "the bug"
- "the right architecture"
- "best test"
- "the correct API"
- "industry standard"

Replace them with repo-specific facts.