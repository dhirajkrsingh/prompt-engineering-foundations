# Prompt Engineering Foundations

Developer-first prompt engineering for reliable AI outputs: prompt anatomy, grounding, few-shot design, decomposition, and validation patterns that reduce hallucinations across the software development lifecycle.

## Overview

This repository is the foundation layer for working developers who want prompts that are precise, testable, and production-usable. The focus is not on clever wording. The focus is on prompt structure that reduces ambiguity, constrains unsupported claims, and gives models a repeatable path to produce useful results.

```
    ┌────────────────────────────────────────────────────────┐
    │                Reliable Prompt Anatomy                 │
    │                                                        │
    │  Role -> Context -> Task -> Examples -> Constraints   │
    │                -> Output Format -> Validation          │
    │                                                        │
    └───────────────────────┬────────────────────────────────┘
                            │
                            ▼
          ┌───────────────────────────────────────────┐
          │  Model behavior becomes more constrained  │
          │  - fewer invented facts                   │
          │  - clearer scoping                        │
          │  - more verifiable outputs                │
          │  - easier prompt iteration                │
          └───────────────────────────────────────────┘
```

## Why This Repo Exists

Most weak prompts fail in predictable ways:

1. The role is vague, so the model improvises the standard of quality.
2. The context is incomplete, so the model fills gaps with guesses.
3. The task is underspecified, so the output drifts.
4. The output format is loose, so downstream use becomes fragile.
5. There is no validation clause, so the model never checks itself.

This repository gives you patterns to fix those failure modes systematically.

## Core Prompt Framework

Use this as the default prompt skeleton for developer workflows.

| Component | Purpose | Hallucination Reduction Effect |
|-----------|---------|--------------------------------|
| **Role** | Defines the model's operating stance | Reduces behavioral drift |
| **Context** | Supplies bounded facts and codebase reality | Reduces unsupported assumptions |
| **Task** | States the exact job to do | Reduces scope creep |
| **Examples** | Shows what "good" looks like | Reduces formatting and reasoning variance |
| **Output Format** | Forces structure | Reduces ambiguous results |
| **Constraints** | States what not to do | Reduces fabricated APIs, files, claims |
| **Validation Criteria** | Forces a final check | Reduces silent failure |

## Modules

| File | Description |
|------|-------------|
| `examples/01_prompt_anatomy.md` | Breakdown of the base prompt shape with a developer workflow example |
| `examples/02_grounded_code_generation.md` | How to ask for code without inviting invented implementation details |
| `examples/03_few_shot_patterns.md` | Few-shot prompting patterns for reviews, triage, and structured engineering output |
| `examples/04_prompt_chaining_for_developers.md` | How to split complex development tasks into safer prompt stages |
| `templates/base-prompt-template.md` | Reusable master template with placeholders |
| `checklists/anti-hallucination-checklist.md` | Review checklist for shipping prompts safely |

## Developer Lifecycle Mapping

| SDLC Stage | Prompt Goal | Prompt Behavior |
|------------|-------------|-----------------|
| Discovery | Understand codebase reality | Ask for evidence, files, dependencies |
| Planning | Produce an execution plan | Separate facts from assumptions |
| Implementation | Generate or edit code | Restrict changes to known files and APIs |
| Debugging | Diagnose the root cause | Require hypotheses tied to evidence |
| Testing | Produce verification assets | Require explicit assertions and expected outcomes |
| Review | Find risks and regressions | Prefer concrete findings over summaries |
| Documentation | Explain real changes | Ground docs in existing code or diff |

## Prompting Principles Backed By Market Guidance

The common themes across current vendor guidance are consistent:

1. Be explicit about instructions and response format.
2. Add relevant context instead of assuming the model knows it.
3. Use few-shot examples when consistency matters.
4. Break hard tasks into steps or chained prompts.
5. Evaluate prompts empirically instead of trusting intuition.

For developers, that translates into a practical rule:

**If the model could plausibly invent a detail, your prompt should either provide that detail, forbid invention, or define the fallback behavior when the detail is missing.**

## Best Practices

1. Start every serious prompt with a bounded role and explicit task.
2. Prefer "use only the provided code/context" over broad open-ended prompting.
3. Ask the model to state missing information instead of inferring it.
4. Require assumptions to be labeled as assumptions.
5. Request evidence-backed reasoning for debugging and code review tasks.
6. For code generation, require compatibility with the current file structure and APIs.
7. Add a validation step that checks output against constraints before finalizing.
8. Treat prompt changes like code changes: version them and evaluate them.

## References

- OpenAI prompt engineering guidance: roles, reusable prompts, few-shot, context, evals
- Anthropic prompt engineering overview: define success criteria and test empirically
- Google prompt design strategies: constraints, formatting, chaining, self-critique, grounding
- Promptfoo anti-hallucination guidance: evals, rubrics, prompt comparison, regression testing

## Author

Dhiraj Singh

## Usage Notice

This repository is shared publicly for learning and reference.
It is made available for everyone through [VAIU Research Lab](https://vaiu.ai/Research_Lab).
For reuse, redistribution, adaptation, or collaboration, contact Dhiraj Singh / [VAIU Research Lab](https://vaiu.ai/Research_Lab).