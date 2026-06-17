---
name: ask-questions-if-underspecified
description: Clarify requirements before implementing. Do not use automatically, only when invoked explicitly.
---

# Ask Questions If Underspecified

## Goal

Ask the minimum set of clarifying questions needed to avoid wrong work. Do not start implementing until the must-have questions are answered, or the user explicitly approves proceeding with stated assumptions.

## Workflow

### 1) Decide Whether The Request Is Underspecified

Treat a request as underspecified if, after exploring how to perform the work, some or all of the following are unclear:

- Objective: what should change vs stay the same
- Done: acceptance criteria, examples, edge cases
- Scope: which files, components, users, or behaviors are in or out
- Constraints: compatibility, performance, style, dependencies, time
- Environment: language/runtime versions, OS, build/test runner
- Safety and reversibility: data migration, rollout, rollback, risk

If multiple plausible interpretations exist, assume the request is underspecified.

### 2) Ask Must-Have Questions First

Ask 1-5 questions in the first pass. Prefer questions that eliminate whole branches of work.

Make questions easy to answer:

- Optimize for scannability with short, numbered questions.
- Offer multiple-choice options when possible.
- Suggest reasonable defaults when appropriate and mark them clearly as the default or recommended choice.
- Bold the recommended choice in option lists.
- If presenting options in a code block, put a bold "Recommended" line immediately before the code block and tag defaults inside the code block.
- Include a fast-path response such as `defaults` to accept all recommended/default choices.
- Include a low-friction "not sure" option when helpful.
- Separate "Need to know" from "Nice to know" if that reduces friction.
- Structure options so the user can respond with compact decisions such as `1b 2a 3c`.
- Restate the chosen options in plain language before proceeding.

### 3) Pause Before Acting

Until must-have answers arrive:

- Do not run commands, edit files, or produce a detailed plan that depends on unknowns.
- Do perform a clearly labeled, low-risk discovery step only if it does not commit to a direction, such as inspecting repo structure or reading relevant config files.

If the user explicitly asks to proceed without answers:

- State assumptions as a short numbered list.
- Ask for confirmation.
- Proceed only after the user confirms or corrects the assumptions.

### 4) Confirm Interpretation, Then Proceed

Once answers arrive, restate the requirements in 1-3 sentences, including key constraints and what success looks like, then start work.

## Question Templates

- "Before I start, I need: (1) ..., (2) ..., (3) .... If you don't care about (2), I will assume ...."
- "Which of these should it be? A) ... B) ... C) ... (pick one)"
- "What would you consider 'done'? For example: ..."
- "Any constraints I must follow (versions, performance, style, deps)? If none, I will target the existing project defaults."
- Use numbered questions with lettered options and a clear reply format.

```text
1) Scope?
a) Minimal change (default)
b) Refactor while touching the area
c) Not sure - use default

2) Compatibility target?
a) Current project defaults (default)
b) Also support older versions: <specify>
c) Not sure - use default

Reply with: defaults (or 1a 2a)
```

## Anti-Patterns

- Do not ask questions that can be answered with a quick, low-risk discovery read, such as configs, existing patterns, or docs.
- Do not ask open-ended questions if a tight multiple-choice or yes/no question would eliminate ambiguity faster.

