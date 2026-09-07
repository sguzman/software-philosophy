# Transactional Development

The v1 doctrine models implementation as a sequence of bounded, reviewable state transitions.

## The transaction boundary

Every meaningful change should have:
- a known accepted base state;
- an explicit authorization;
- a durable macro-goal identity;
- one or more bounded execution attempts;
- candidate results;
- evidence;
- semantic review;
- an integration decision.

Git naturally supplies stable identities for these states.

## Input state

The input to a worker is not `the whole project in prose`.

It is a base commit or current accepted main, canonical doctrine, the active/reopened macro-goal, any current director review/correction contract, and local source relevant to the goal.

The worker can inspect the repository as needed. The director should not paste the codebase into the prompt.

## Candidate attempts

One macro-goal may produce several candidate states before acceptance.

Example:

    Goal 0006
      Attempt A1 -> candidate C1 -> director: revise
      Attempt A2 -> candidate C2 -> director: accept

C1 is historical evidence and implementation lineage. It is not erased merely because C2 supersedes it.

## Worker terminalization

Each execution attempt reaches a terminal execution state:

    active -> done
        or
    active -> blocked

`done` means the worker claims a reviewable candidate exists.

`blocked` means further execution requires unresolved authority or unavailable capability.

Neither state closes the project transaction.

If the repository has completion-observer machinery, terminalization triggers the best-effort return signal for **that attempt**.

## Review as transaction control

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

After integration, update stale current-status claims, roadmap gates, priorities, follow-up goals, and architectural notes.

This closes the transaction for that macro-goal.

## Revision and correctable rejection

A terminal worker attempt can be rejected without rejecting the macro-goal itself.

When the desired outcome remains the same, the director should write a durable correction review and **reopen the same goal** rather than incrementing the goal number merely because the worker session ended.

Typical transition:

    G: active(A1)
      -> done
      -> director review: revise
      -> G: ready
      -> fresh worker session
      -> active(A2)

The new session reads the current review contract and continues the same branch/report lineage unless the director explicitly requires a clean implementation branch.

## Session termination is not transaction closure

An agent UI may represent one session as permanently completed.

That is a property of the execution container, not of the repository transaction.

Therefore:

    session ended != goal closed
    new session != new goal
    worker DONE != director ACCEPT

This separation prevents tool UX from dictating project ontology.

## Signaling is orthogonal

Transaction correctness and completion signaling remain independent.

A useful worker candidate may be produced even if desktop notifications are unavailable.

A successful notification may occur for a candidate that the director later rejects.

A later correction attempt must re-arm signaling without consuming stale terminal state from an earlier attempt.

Formally:

    terminal_signal_i != acceptance
    notification_failure_i != product_failure

The return channel changes who is paying attention, not what is true.

## Reversibility

A transaction should be cheap to inspect and cheap to undo.

This favors bounded branches, explicit commits, preserved attempt history, no hidden mutable state, deterministic migrations where possible, visible generated artifacts, and reviewable diffs.

The point is not tiny commits for their own sake. The point is **recoverable causality**.
