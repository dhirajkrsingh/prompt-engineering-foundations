# Anti-Hallucination Prompt Review Checklist

Use this before you rely on a prompt in serious development work.

## Scope

- Does the prompt define a specific role?
- Does it define the exact task?
- Does it limit the task to a known scope?

## Grounding

- Does the prompt provide concrete context or tell the model where to get it?
- Does it forbid unsupported assumptions?
- Does it say what to do when information is missing?

## Output Control

- Is the output format explicit?
- Are examples included if consistency matters?
- Does the prompt distinguish required content from optional content?

## Developer Safety

- Does it forbid invented files, packages, APIs, or test frameworks?
- Does it require assumptions to be labeled?
- Does it require evidence-backed reasoning for debugging or review tasks?

## Validation

- Does the prompt force a final check against constraints?
- Does it ask the model to confirm compliance before finishing?
- Is there a fallback behavior when the answer cannot be grounded?

## Release Gate

Do not ship the prompt as "ready" if any of these are true:

1. The prompt relies on implied repo structure.
2. The prompt asks for code but provides no project conventions.
3. The prompt asks for a fix without defining the failure.
4. The prompt does not define what uncertainty should look like.
5. The prompt cannot be evaluated with concrete test cases.