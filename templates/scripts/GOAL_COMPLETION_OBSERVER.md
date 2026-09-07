# Goal Completion Observer Contract

This is a technology-independent contract for a repository-owned terminal goal observer.

A Windows repository may implement it as `scripts/codex-goal-notify.ps1`.

## Required semantics

- Accept one explicit goal identity and repository root.
- Be launched automatically by the implementation worker.
- Run detached from the current agent turn/shell lifecycle.
- Observe durable goal state or a deterministic goal-specific sentinel.
- Distinguish `done` from `blocked`.
- Emit exactly one terminal notification.
- Exit after signaling.
- Do not notify for `ready`, `active`, ordinary retries, or intermediate agent turns.
- Survive the repository's normal checkout-restoration handoff without routinely missing the event.
- Notification delivery failure is non-fatal to product correctness.
- Provide a deterministic no-notification or injectable-sink test mode.
- Do not become a persistent machine-wide daemon unless the repository explicitly chooses that architecture.

## Recommended notification payload

- project identity;
- goal ID;
- terminal status: Completed or Blocked.

An audible cue may be used when the platform permits it without intrusive behavior.

## Minimum tests

- done detection;
- blocked detection;
- no signal for active/ready;
- exactly-once terminal behavior;
- missing/malformed goal handling;
- checkout-restoration-safe observation;
- notification sink failure remains non-fatal.

## Epistemic rule

The observer is an attention router.

It is not evidence, review, acceptance, or integration.
