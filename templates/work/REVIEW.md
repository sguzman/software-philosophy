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

### Load-bearing continuity audit

If a load-bearing capability is touched:
- is the continuity envelope explicitly identified?
- did the attempt avoid mutating the principal's only verified stable runtime?
- is a separate development channel actually being exercised?
- can the principal resume stable operation without repairing dev first?
- did dev install/reset/uninstall avoid damaging stable requirements?
- did the attempt discover new private-use dependence that must be externalized?

### Collision-surface audit

If stable/dev channels coexist:
- source/worktree isolation verified?
- runtime/application/extension identity isolated or intentionally shared?
- persistent state/database/storage collisions audited?
- DOM/global namespace collisions audited where relevant?
- audio/device/global-resource ownership audited?
- IPC/ports/sockets audited?
- Native Messaging / OS registrations / service names audited?
- destructive cleanup/uninstall blast radius audited?
- UNKNOWN surfaces called out honestly?

Separate worktrees/profiles alone are not sufficient evidence of isolation.

### Promotion audit

If stable promotion is proposed:
- exact candidate identity recorded?
- automated gates passed?
- strongest relevant runtime evidence collected?
- continuity envelope verified on the exact candidate?
- human experiential acceptance obtained where required?
- stable advances only to the candidate actually verified?

Worker DONE is not stable promotion by itself.

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
Stable/consumption channel remains untouched during correction: yes / no / not applicable

## Validation required for next review

## Integration

Record integrated commit or reason for non-integration.

If this review promotes stable, record the exact verified candidate and promotion evidence separately from ordinary development acceptance.

## Current-state updates

Update operational criticality, continuity envelope, promotion rules, and collision audit when the review discovers new durable facts.

## Next goal

Only allocate a new goal ID when the semantic work unit actually advances or this goal is superseded.
