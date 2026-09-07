# 0000 — Goal title

## Outcome

Describe the desired end state.

## Why now

Explain why this goal is the next semantic unit of work.

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

State what must be true before the current worker attempt may claim DONE and what the director will review.

## Validation

List exact commands and required evidence classes.

## Correction continuation policy

Goal ID: preserve unless the director explicitly supersedes this semantic goal.
Branch lineage: reuse by default / specify otherwise.
Report lineage: append/preserve prior attempts.
Fresh worker session after prior session terminalization: yes.
Required review path: docs/work/reviews/<id>.md

## Completion observability

Observer path / command:
Goal identity:
Attempt/epoch handling:
Terminal states: done / blocked
Checkout-restoration reliability rule:
Stale prior-attempt state rule:
Notification failure policy: non-fatal unless this goal explicitly exists to repair the observer itself.

The worker launches/re-arms the observer automatically. Do not require a second human command.

## Repository handoff

Branch name:
Report path:
Work-state transitions:

## Human verification

State only observations that truly require the human or local machine.

## Stop / escalation conditions

List exact discoveries that require director judgment.
