# Escalation, Review, and Integration

Bounded autonomy works only when the worker knows when to stop.

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
Candidate is suitable for integration.

### Reject
Candidate violates doctrine or goal strongly enough that correction should start from a different approach.

### Revise
Architecture is basically sound; write a bounded correction contract.

### Block
New director or human decision is required before implementation should continue.

## Integration authority

The worker should normally not merge its own candidate into accepted main.

This preserves a clean separation:

    worker: “Here is the candidate and evidence.”
    director: “This becomes project reality.”

For trivial repositories, the roles may be collapsed physically into one agent. The conceptual distinction should remain.

## Review artifacts

A durable review can include:
- Result;
- acceptance decision;
- architectural findings;
- contract misses;
- evidence findings;
- required corrections;
- correction non-goals;
- integration notes;
- next-goal recommendation.

This allows correction work to proceed repo-to-repo instead of chat-to-chat.
