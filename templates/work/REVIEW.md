# 0000 — Director Review

## Decision

ACCEPT / REVISE / REJECT-CORRECTABLE / REJECT-SUPERSEDE / BLOCK

## Repository goal identity

Preserve same goal ID: yes / no
Reason:

## Attempt disposition

Current attempt:
Worker session terminal: yes / no / unknown
Next action:

## Goal compliance

## Architectural review

### Interactive-thread audit

If GUI/interactive code changed:
- any blocking I/O on the UI thread?
- any CPU-heavy or user-data-scaled work on the UI thread?
- any blocking receive/join/sleep/process wait?
- any contended lock that can stall interaction?
- is expensive work moved behind an asynchronous worker boundary?
- can stale results overwrite newer UI intent?

### Language-profile audit

- product/runtime code remains Rust-first, or deviation is explicitly justified?

## Evidence review

## Scope / non-goal review

## Accepted work to preserve

## Required corrections

Only include if another attempt is authorized.

## Correction non-goals

## Continuation contract

Reopen goal to ready: yes / no
Next worker session: fresh if prior session terminated
Branch: reuse existing / replacement branch
Report: append/preserve history
Sync current director review/governance from main before editing: yes
Completion observer: re-arm fresh attempt/epoch; stale prior terminal state must not retrigger

## Validation required for next review

## Integration

Record integrated commit or reason for non-integration.

## Current-state updates

## Next goal

Only allocate a new goal ID when the semantic work unit actually advances or this goal is superseded.
