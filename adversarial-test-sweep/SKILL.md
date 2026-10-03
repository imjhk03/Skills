---
name: adversarial-test-sweep
description: "Run a comprehensive adversarial unit-test audit when the user requests a sweep, especially after accumulated code changes. Probe edge cases, malformed data, races, boundaries, resource limits, corrupted state, and invalid assumptions; fix bugs and consolidate weak tests."
---

# Adversarial Test Sweep

Audit existing production behavior, repair concrete bugs, and leave a stronger, maintainable suite with no unexplained failures. This is a deliberate audit requested by the user; routine code changes do not trigger a comprehensive sweep.

## Establish the Baseline

- Read repository instructions, build/test configuration, relevant production contracts, and existing tests. Inspect accumulated changes when a useful base is available; include connected existing behavior where the requested audit warrants it. Do not assume an arbitrary commit range or limit the audit to recently touched lines.
- Run the existing suite and capture failures, skips, warnings, and available coverage. Follow local validation ordering, including a complete production-target build before tests where required. Preserve user changes and summarize likely work areas before a multi-file implementation.
- Separate product defects, invalid test expectations, fixture defects, flaky scheduling, and host failures. Diagnose a failure before deciding which code should change.

## Select Adversarial Cases

Trace inputs through real callers and prioritize invariants, shared logic, persistence, asynchronous state changes, and uncovered branches. Consider each category below where the code has a relevant contract; do not manufacture unsupported behavior to fill a checklist.

| Category | Useful probes |
|---|---|
| Edge cases | Empty, missing, repeated, conflicting, or degenerate values; unusual dates, locales, and identities |
| Malformed inputs | Invalid serialized data, partial records, unknown enum values, malformed components, and unsupported combinations |
| Race conditions | Reverse completion, cancellation, reentrancy, settings or authorization changes during suspension, observer lifetime |
| Boundary values | Exact inclusive/exclusive endpoints, zero, negative values, integer limits, overflow, DST and calendar transitions |
| Resource exhaustion | Bounded large inputs, exhausted counters or recurrence limits, supported dependency failures, cleanup after partial work |
| State corruption | Inconsistent persisted fields, stale results or caches, interrupted updates, recovery and isolation |
| Invalid assumptions | Ordering transitivity, identity uniqueness, deduplication precision, clock monotonicity, permissions, idempotence |

- Keep stress cases bounded and reproducible. Exercise resource limits with supported failure injection or manageable inputs; avoid exhausting the host's memory, disk, or process capacity. Seed generated inputs and retain the smallest useful failing case.
- Make races deterministic with controlled suspension and explicit acknowledgements. Use fixed clocks, calendars, locales, isolated persistence, and supported framework fixtures where needed. Avoid sleeps that merely hope a race occurs; await and clean up tasks, observers, and temporary state.

## Make Each Test Earn Its Place

- Ask: "Which production behavior does this protect, and what specific regression would it catch?" Keep cases with a distinct failure mode or necessary contract assertion. Extend or parameterize existing tests when that preserves readability and avoids duplication.
- Exercise the real production entry point or unit owning the behavior. Derive expected outcomes independently; never copy its algorithm into a test helper. Assert exact values, identities, order, exclusions, errors, and state transitions as the contract requires.
- Mock external or nondeterministic dependencies while keeping the behavior under test real. Reuse fixtures and existing boundaries. Do not introduce production protocols or architectural layers solely to facilitate this audit.
- Remove or consolidate empty, assertion-free, constant-only, duplicate, and mock-setter/response tests after checking that meaningful coverage survives. Retain helper-specific tests only for necessary complex guarantees not already established by production-facing tests. Do not delete a failing test to hide a defect.

## Repair and Repeat

- For each concrete bug, establish a focused permanent regression and demonstrate failure before the fix and success afterward when practical. Make the smallest production repair consistent with the existing architecture.
- Correct an invalid test expectation only when the production contract supports the change. Repair misleading fixtures instead of weakening assertions. Do not silence flaky failures through skips, blanket retries, or arbitrary delays.
- After each meaningful repair, compile and validate in the repository's required order, run affected tests, then repeat the complete relevant suite. Use supported runtime/configuration variants where they exercise materially different behavior. Revisit new failures until each is resolved or clearly identified as an external blocker.
- Use available coverage to inspect untested branches and compare the audited paths with the baseline. Add cases for demonstrated gaps in meaningful behavior; do not chase a universal percentage or test count. A passing suite alone does not establish strong coverage.
- Finish when scoped defects have permanent coverage, useful cases survive consolidation, the final suite passes, and remaining skips or limitations are explained. Report an environment blocker as unverified validation; do not claim a clean run when required checks could not execute.

## Report the Outcome

Summarize discovered bugs and fixes, retained regressions, removed/consolidated tests, actual validation commands and counts, and coverage of the audited paths. Explain legitimate skips and remaining gaps such as live services or rendered UI. Keep evidence proportional to the audit; create extra reports only when useful or requested.

Review the final diff for duplicated logic, unnecessary helpers, incidental refactors, and unrelated changes. Keep follow-up work separate. A sweep does not itself authorize commits, pushes, PRs, releases, or mutations of real user data; follow the user's existing authorization for those actions.
