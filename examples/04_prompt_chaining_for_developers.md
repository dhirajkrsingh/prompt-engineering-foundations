# Example 4: Prompt Chaining Across A Development Task

## Principle

One large prompt often combines incompatible goals:

- discover the codebase
- decide on a plan
- edit code
- generate tests
- write documentation

That increases hallucination risk because the model is rewarded for completeness before certainty.

## Safer Prompt Chain

### Prompt 1: Discovery

```text
Identify the files and symbols relevant to [task].
Return only confirmed findings and unknowns.
```

### Prompt 2: Planning

```text
Using only the confirmed findings, create a minimal implementation plan with risks and validation.
Do not generate code yet.
```

### Prompt 3: Implementation

```text
Implement the smallest safe change consistent with the plan and current repo conventions.
```

### Prompt 4: Tests

```text
Add focused regression tests for the changed behavior using the existing test framework.
```

### Prompt 5: Review

```text
Review the proposed change for regressions, unsupported assumptions, and missing tests.
```

## Why This Reduces Hallucinations

1. Discovery constrains the available facts.
2. Planning turns those facts into explicit decisions.
3. Implementation is then forced to stay inside that decision boundary.
4. Review provides a final challenge pass.

## When To Chain

Chain prompts when:

- the repo is unfamiliar
- the task spans more than one file area
- the bug is not yet well understood
- the implementation requires tests and docs
- you need auditable reasoning steps

Do not chain just for style. Chain when each stage reduces uncertainty for the next stage.