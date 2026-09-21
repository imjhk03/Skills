## Engineering Principles

### Keep Changes Small

- Prefer the smallest reasonable change that solves the requested problem.
- Do not refactor unrelated code while implementing a feature or fixing a bug.
- Reuse existing types, utilities, and patterns before introducing new ones.
- Avoid speculative abstractions and over-engineering.
- If the implementation becomes substantially larger than expected, stop and reconsider the approach before continuing.

### Follow the Existing Codebase

- Follow the existing architecture, naming conventions, and coding style.
- Prefer consistency with the surrounding code over introducing a theoretically cleaner new pattern.
- Do not introduce a new architecture or architectural layer unless the task explicitly requires it.

### New Abstractions

- Before creating a new Manager, Service, Coordinator, Protocol, helper type, or architectural layer, first check whether an existing type can reasonably own the responsibility.
- New abstractions must solve a concrete existing problem, not a hypothetical future need.
- Do not introduce protocols solely for testability unless there is a meaningful abstraction boundary.

### Readability

- Optimize repository code for readability and maintainability, not token efficiency or brevity.
- Avoid clever, compressed, or overly dense code.
- Avoid magic numbers, raw string keys, implicit positional assumptions, and unexplained constants.
- Prefer named concepts when values have domain meaning.

### Tests

- Treat tests as maintainable repository code, not disposable scripts.
- Keep tests readable and consistent with the production code style.
- Do not rewrite or duplicate large portions of production logic inside tests.

### Scope Control

- Before making changes, inspect the relevant code and understand the existing implementation.
- Do not modify unrelated files unless necessary.
- Avoid formatting or rewriting untouched code.
- Do not make opportunistic cleanup changes outside the requested scope.

### Completion

- Passing builds and tests are necessary but not sufficient.
- Before finishing, check for:
  - unnecessary abstractions
  - duplicated logic
  - unnecessary files
  - magic values
  - incidental refactors
  - code inconsistent with surrounding patterns
- Simplify where possible without changing behavior.

## Apple Human Interface Guidelines

- Before starting work, check whether Apple Human Interface Guidelines (HIG) have relevant guidance; for any UI, UX, visual design, layout, interaction, or Apple-platform implementation work, consult the current HIG and use it to inform the result.
- For an HIG page at `https://developer.apple.com/design/...`, create the agent-readable URL by inserting `/tutorials/data/` immediately before `/design/` and appending `.md` to the page path (before any query string or fragment). Example: `https://developer.apple.com/design/human-interface-guidelines/typography` becomes `https://developer.apple.com/tutorials/data/design/human-interface-guidelines/typography.md`.
- Verify the transformed URL before relying on it. If the `.md` route is unavailable, use the equivalent verified DocC JSON URL ending in `.json` and read or render that content as Markdown.
