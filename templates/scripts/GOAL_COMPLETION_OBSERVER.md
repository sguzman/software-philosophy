# Goal Completion Observer Contract

This is a technology-independent contract for a repository-owned terminal execution-attempt observer.

A Windows repository may implement it as `scripts/codex-goal-notify.ps1`.

## Required semantics

- Accept one explicit repository goal identity and repository root.
- Establish a fresh observer epoch for the current execution attempt.
- Be launched/re-armed automatically by the implementation worker.
- Run detached from the current agent turn/shell lifecycle.
- Observe durable attempt terminal state or a deterministic goal/attempt-specific sentinel.
- Distinguish `done` from `blocked`.
- Emit exactly one terminal notification **per attempt**.
- Exit after signaling.
- Do not notify for `ready`, `active`, ordinary retries, or intermediate agent turns.
- Survive the repository's normal checkout-restoration handoff without routinely missing the event.
- Permit the same goal ID to be reopened for another attempt without stale terminal/ack state causing an immediate false notification.
- Notification delivery failure is non-fatal to product correctness.
- Provide a deterministic no-notification or injectable-sink test mode.
- Do not become a persistent machine-wide daemon unless the repository explicitly chooses that architecture.

## Re-arm strategies

Use one of:
- goal + attempt/epoch ID;
- rotating per-attempt state files;
- unique session token managed by automation;
- safe stale-state reset under a single-active-attempt invariant;
- another deterministic equivalent.

The human must not manually manage the attempt token or stale-state cleanup.

## Recommended notification payload

- project identity;
- goal ID;
- terminal status: Completed or Blocked;
- correction/attempt identity when useful.

## Minimum tests

- done detection;
- blocked detection;
- no signal for active/ready;
- exactly-once terminal behavior within one attempt;
- second attempt under the same goal does not consume/replay the first attempt's terminal state;
- missing/malformed goal handling;
- checkout-restoration-safe observation;
- notification sink failure remains non-fatal.

## Epistemic rule

The observer is an attention router.

It is not evidence, review, acceptance, goal closure, or integration.
