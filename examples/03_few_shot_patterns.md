# Example 3: Few-Shot Patterns For Lower-Hallucination Outputs

## Why Few-Shot Helps

Few-shot prompting reduces ambiguity by showing the model the exact pattern to copy. This is most useful when you need:

1. stable output format
2. narrow reasoning style
3. consistent handling of uncertainty
4. reliable distinction between facts and assumptions

## Developer Use Cases Where Few-Shot Is Worth It

| Use Case | Why Few-Shot Helps |
|----------|--------------------|
| Code review findings | Makes severity ordering and evidence format consistent |
| Root-cause analysis | Encourages evidence-first diagnoses |
| Structured change plans | Keeps plans ordered and scoped |
| Documentation summaries | Keeps docs tied to actual implementation |
| Bug triage | Prevents broad speculative causes |

## Weak Prompt

```text
Review this change and tell me what is wrong.
```

## Better Few-Shot Prompt

```text
# Role
You are a senior reviewer focused on bugs, regressions, and missing tests.

# Instructions
Return findings first.
Each finding must include severity, evidence, and likely impact.
If there are no findings, say so explicitly.

# Example 1
Input: Change adds caching to user permissions.
Output:
Severity: High
Evidence: Cache invalidation is not triggered when permissions are updated.
Impact: Users may retain stale authorization state.

# Example 2
Input: Change renames a config field without updating docs.
Output:
Severity: Medium
Evidence: Documentation still references `authTimeoutSeconds`, but code now expects `sessionTimeoutSeconds`.
Impact: Deployments may use the wrong config key.

# Task
Review the provided diff.
```

## What Makes Few-Shot Work Here

1. The examples teach the shape of a finding.
2. The examples bias the model toward concrete evidence.
3. The examples narrow the style away from vague summaries.

## Few-Shot Rules For Developers

1. Use small, high-signal examples.
2. Keep example formatting consistent.
3. Include at least one example that shows correct uncertainty behavior.
4. Do not overload the prompt with many near-duplicate examples.
5. Prefer examples from the same type of engineering task.

## Important Warning

Few-shot examples do not replace context. If the repo facts are missing, few-shot examples mostly make the model confidently consistent, not necessarily correct.