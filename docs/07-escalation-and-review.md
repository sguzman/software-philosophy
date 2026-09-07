# Escalation, Review, and Integration

Bounded autonomy works only when the worker knows when to stop, and durable review works only when the system knows whether a correction is a new goal or another attempt at the same goal.

## Escalation is an authority boundary

A worker should escalate when continued progress requires a decision outside the macro-goal.

Common triggers:
- two plausible solutions imply different architecture;
- an invariant must be changed;
- product semantics would change;
- persistence compatibility would change;
- a dependency choice creates a new long-term subsystem;
- acceptance criteria appear impossible without broad scope expansion;
- the selected external API cannot satisfy the required contract.

Do not escalate ordinary implementation difficulty.

Not escalation:
- compiler error;
- formatting failure;
- a directly related failing test;
- a missing import;
- a local refactor needed to implement the authorized abstraction;
- a second blocker clearly inside the same goal.

## Blockers are durable

When escalation is required:
- preserve the branch;
- write the evidence;
- move the goal to blocked/ if the repo protocol uses work states;
- state the exact decision required;
- do not silently choose.

A good blocker compresses uncertainty for the director.

## Director review

The director reviews both implementation and epistemics.

### Implementation review
Architecture, ownership, data flow, API shape, scope, maintainability.

### Contract review
Outcome, non-goals, acceptance gates, required validation.

### Evidence review
Did the claimed tests run? Are claims stronger than evidence? Were failures hidden? Were tests weakened?

### Product review
Is this actually the desired behavior? Does it preserve taste and priority?

## Review outcomes

### Accept
Candidate is suitable for integration. Integrate and close the macro-goal transaction.

### Revise
The macro-goal remains valid, but the current attempt is insufficient.

Write a bounded correction contract, preserve the same goal ID, move/reopen the goal to `ready/`, and authorize another attempt.

If the previous worker session has already terminated, the human starts a **fresh worker session**. That session continues the same repository goal lineage.

### Reject
The current candidate or approach is not acceptable.

Two cases must be distinguished:

1. **Correctable rejection, same objective.** The goal's desired outcome remains valid. Preserve the goal ID, write a correction/replacement approach contract, and start another attempt; use a fresh worker session if required.
2. **Goal abandonment or supersession.** The semantic objective itself is no longer desired or has changed enough to be a different work unit. Close/supersede the old goal and create a new goal ID if more work is authorized.

Do not use a new goal number merely to represent a new agent session.

### Block
New director or human decision is required before implementation should continue.

Once the blocking decision is resolved, the same goal may be reopened to `ready/` for another attempt.

## Correction review contract

A correction review should state:
- decision;
- whether the repository macro-goal identity is preserved;
- why the candidate was insufficient;
- accepted work that should be kept;
- required corrections;
- correction non-goals;
- same/new branch decision;
- report history rule;
- work-state transition back to `ready/` when applicable;
- whether a fresh worker session is required because the prior session terminated;
- completion-observer re-arm requirements;
- validation and evidence required for the next review.

## Integration authority

The worker should normally not merge its own candidate into accepted main.

This preserves a clean separation:

    worker: `Here is the candidate and evidence.`
    director: `This becomes project reality.`

For trivial repositories, the roles may be collapsed physically into one agent. The conceptual distinction should remain.

## Review artifacts

A durable review can include Result, goal identity, attempt disposition, architectural findings, contract misses, evidence findings, required corrections, correction non-goals, branch/report continuation instructions, session-lifecycle instructions, integration notes, and next-goal recommendation.

This allows correction work to proceed repo-to-repo instead of chat-to-chat.
