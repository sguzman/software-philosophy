# Transactional Development

v1.0 models implementation as a sequence of bounded, reviewable state transitions.

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

The input to a worker is not “the whole project in prose.”

It is:
- a base commit or current main;
- canonical doctrine;
- the active macro-goal;
- local source relevant to the goal.

The worker can inspect the repository as needed. The director should not paste the codebase into the prompt.

## Candidate state

The worker produces:
- a branch;
- commits;
- changed files;
- tests;
- a report;
- possibly a blocked-state record.

The candidate is isolated from accepted main until review.

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

Passing tests answer only part of this list.

## Acceptance

Acceptance means the candidate becomes part of authoritative project reality.

After integration, update any stale:
- current-status claims;
- roadmap gates;
- priorities;
- follow-up goals;
- architectural notes.

This closes the transaction.

## Rejection and revision

Rejection should also be durable.

When possible, write a review contract that says:
- what is wrong;
- whether the architecture remains valid;
- what correction is authorized;
- what must not be changed;
- what evidence is required next.

Then the worker can perform a correction pass without the human relaying the review through chat.

## Reversibility

A transaction should be cheap to inspect and cheap to undo.

This favors:
- bounded branches;
- explicit commits;
- no hidden mutable state;
- deterministic migrations where possible;
- visible generated artifacts;
- reviewable diffs.

The point is not tiny commits for their own sake. The point is **recoverable causality**.
