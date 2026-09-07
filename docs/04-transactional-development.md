# Transactional Development

The v1 doctrine models implementation as a sequence of bounded, reviewable state transitions.

## The transaction boundary

Every meaningful change should have:
- a known base state;
- an explicit authorization;
- a bounded transformation;
- a candidate result;
- evidence;
- a semantic review;
- an integration decision.

Git naturally supplies stable identities for these states.

## Input state

The input to a worker is not `the whole project in prose`.

It is a base commit or current main, canonical doctrine, the active macro-goal, and local source relevant to the goal.

The worker can inspect the repository as needed. The director should not paste the codebase into the prompt.

## Candidate state

The worker produces a branch, commits, changed files, tests, a report, and possibly a blocked-state record.

The candidate is isolated from accepted main until review.

## Worker terminalization

Before director review, the worker reaches a terminal execution state:

    active -> done
        or
    active -> blocked

`done` means the worker claims a reviewable candidate exists.

`blocked` means further execution requires unresolved authority or unavailable capability.

Neither terminal state closes the project transaction.

If the repository has completion-observer machinery, this transition is the event that may trigger the best-effort human return signal.

## Review as commit validation

The director asks:

1. Did the candidate satisfy the stated outcome?
2. Were non-goals respected?
3. Were architectural boundaries preserved?
4. Are new abstractions coherent?
5. Does the evidence actually support the claims?
6. Did the worker hide uncertainty?
7. Is the diff proportionate to the goal?
8. Has project-state documentation become stale?
9. Is the candidate semantically desirable?

Passing tests answer only part of this list. A completion notification answers none of it.

## Acceptance

Acceptance means the candidate becomes part of authoritative project reality.

After integration, update any stale current-status claims, roadmap gates, priorities, follow-up goals, and architectural notes.

This closes the transaction.

## Rejection and revision

Rejection should also be durable.

When possible, write a review contract that says what is wrong, whether the architecture remains valid, what correction is authorized, what must not be changed, and what evidence is required next.

Then the worker can perform a correction pass without the human relaying the review through chat.

## Signaling is orthogonal

Transaction correctness and completion signaling must remain independent.

A useful worker candidate may be produced even if desktop notifications are unavailable.

A successful notification may occur for a candidate that the director later rejects.

Formally:

    terminal_signal != acceptance
    notification_failure != product_failure

The return channel changes who is paying attention, not what is true.

## Reversibility

A transaction should be cheap to inspect and cheap to undo.

This favors bounded branches, explicit commits, no hidden mutable state, deterministic migrations where possible, visible generated artifacts, and reviewable diffs.

The point is not tiny commits for their own sake. The point is **recoverable causality**.
