# Base Prompt Template For Developers

Use this as the default starting point for prompts that need to be reliable.

## Template

```text
# Role
You are a [specific role] working inside [specific domain or repo context].
Your priority is correctness, grounded reasoning, and explicit handling of uncertainty.

# Context
Use only the following context unless the task explicitly allows broader knowledge:
- [codebase facts]
- [relevant files or snippets]
- [product/domain constraints]
- [runtime or environment constraints]

# Task
Complete the following task:
[exact task]

# Examples
Input example:
[example input]

Good output example:
[example output]

# Output Format
Return:
1. [required section or data shape]
2. [required section or data shape]

# Constraints
- Do not invent files, functions, APIs, tests, or package usage that are not present in the context.
- If required information is missing, say exactly what is missing.
- Separate confirmed facts from assumptions.
- Keep changes scoped to the stated task.

# Validation Criteria
Before finalizing, verify:
1. Every major claim is grounded in the provided context.
2. The output matches the requested format.
3. Any uncertainty is stated explicitly.
4. No unsupported implementation details were introduced.
```

## Why This Template Works

Each section removes a class of model failure:

| Section | Failure It Prevents |
|---------|---------------------|
| Role | Tone drift, low-quality default behavior |
| Context | Hallucinated facts, stale assumptions |
| Task | Scope expansion, partial answers |
| Examples | Format inconsistency, vague interpretation |
| Output Format | Downstream parsing failures |
| Constraints | Fabricated code or overreach |
| Validation Criteria | Silent non-compliance |

## Example: Bug Fix Prompt

```text
# Role
You are a senior Python debugging assistant working in an existing production repository.

# Context
Use only the following information:
- Error stack trace from failing test
- Current implementation of payment reconciliation service
- Existing test files in tests/payments/

# Task
Identify the root cause of the failure and propose the smallest safe fix.

# Examples
Good output example:
1. Root cause
2. Evidence
3. Minimal fix
4. Regression risks

# Output Format
Return exactly four sections:
1. Root cause
2. Evidence
3. Minimal fix
4. Regression risks

# Constraints
- Do not invent missing source files.
- Do not recommend refactors outside the failing path unless required.
- If the trace is insufficient, say what additional file or test is needed.

# Validation Criteria
Before finalizing, check that the root cause is supported by the provided code and that the fix is smaller than a rewrite.
```