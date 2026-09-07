# Evidence and Verification

Agentic systems fail when they collapse `the agent says it worked` into `it is true`.

The v1 doctrine treats evidence as typed, scoped, and revisable.

## Evidence classes

### E0 — static repository evidence

Examples: file exists, function has a particular signature, dependency is configured, branch contains a change.

Useful for structural claims.

### E1 — deterministic checks

Examples: formatting, linting, type checking, compilation, unit tests, deterministic integration tests.

Useful for mechanical correctness.

### E2 — hosted platform evidence

Examples: Windows CI compile, Linux CI tests, platform API enumeration in a hosted runner.

Useful only for capabilities actually present in that environment.

### E3 — runtime environment evidence

Examples: program launches on a real desktop, GPU renderer initializes, audio device works, filesystem integration behaves correctly.

This may require a specific machine.

### E4 — human experiential evidence

Examples: UI feels responsive, layout is comfortable, highlight movement looks correct, audio transition sounds wrong, or the implementation technically works but solves the wrong problem.

This evidence cannot always be replaced by automation.

## Notifications are not evidence

A completion notification is **not** an evidence class.

It may be caused by a durable repository transition, but the signal itself proves only that the observer attempted to route attention.

Invalid claims:
- `I saw a toast -> tests passed`;
- `Codex notified me -> goal acceptance gates were satisfied`;
- `Completed notification -> director accepted the branch`.

The correct interpretation is:

> `A terminal signal arrived -> inspect the durable goal state, report, candidate, and evidence.`

## No evidence laundering

Do not silently promote one evidence class into another.

Invalid promotion:
- Linux compile -> Windows behavior;
- hosted Windows build -> real GPU launch;
- generated mock screenshot -> actual UI state;
- passing unit tests -> acceptable product semantics;
- roadmap completion mark -> verified current implementation;
- completion notification -> accepted implementation.

## Current-state language

Use explicit status labels such as VERIFIED, VERIFIED IN HOSTED CI, VERIFIED ON REAL WINDOWS MACHINE, IMPLEMENTED BUT RUNTIME UNVERIFIED, PARTIAL, BLOCKED, HISTORICAL, OBSOLETE, and UNKNOWN.

The exact vocabulary may vary. The principle is that uncertainty is represented, not erased.

## Reports and evidence

Worker reports should include exact commands, exact result summary, environment, known limitations, failures, and unverified claims.

When completion-observer behavior is material, reports may also record whether observer startup succeeded or failed. That record is workflow diagnostics, not product evidence.

Never write `works on Windows` when the evidence is only `cargo check succeeded on windows-latest`.

## Director responsibility

The director interprets evidence and decides what state claims are justified.

This is semantic work because the meaning of a passing test depends on what it covers, where it ran, what it excludes, and whether the test itself was weakened.

## Truthful degradation

When an environment cannot prove something, classify the limitation.

Do not distort architecture merely to manufacture a green check.

This is the **truthful evidence principle**:

> Preserve the distinction between product failure and evidence-environment limitation.
