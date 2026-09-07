# 0000 — Goal title

## Outcome

Describe the desired end state.

## Why now

Explain why this goal is the next unit of work.

## Starting evidence

List current failures, commits, tests, logs, or status claims.

## Architecture authority

Point to canonical docs and pre-decided architecture.

## Authorized passes / subtracks

List diagnosis, implementation, repair, test, and cleanup work that can proceed without another prompt.

## Constraints

List invariants, compatibility rules, ownership boundaries, and implementation constraints.

## Non-goals

Explicitly prohibit adjacent work.

## Acceptance gates

State what must be true before worker-terminal DONE is allowed.

## Validation

List exact commands and required evidence classes.

## Completion observability

Observer path / command:
Goal identity:
Terminal states: done / blocked
Checkout-restoration reliability rule:
Notification failure policy: non-fatal unless this goal explicitly exists to repair the observer itself.

The worker launches the observer automatically when available. Do not require a second human command.

## Repository handoff

Branch name:
Report path:
Work-state transitions:

## Human verification

State only observations that truly require the human or local machine.

## Stop / escalation conditions

List exact discoveries that require director judgment.
