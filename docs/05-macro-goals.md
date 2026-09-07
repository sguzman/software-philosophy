# Macro-Goals, Prompt Tax, and Vigilance Tax

Macro-goals are a central operational improvement of the v1 doctrine.

They exist because a one-prompt-per-fix workflow can make the human a scheduler and courier even when the agents are individually capable.

## Prompt tax

**Prompt tax** is the coordination cost paid when work is unnecessarily split across many conversational turns.

Symptoms include predictable compiler failures causing new prompts, the same architecture being copied repeatedly, or execution stalling at ordinary local repair work.

Prompt tax consumes attention, breaks flow, and reduces practical autonomy.

## Vigilance tax

**Vigilance tax** is the coordination cost paid when the human must keep checking whether delegated work has stopped.

Symptoms:
- opening the terminal every few minutes;
- asking the worker `are you done?`;
- keeping the task mentally resident because completion has no return channel;
- forgetting that a goal finished and discovering it much later;
- running an extra manual watcher command after every invocation.

Macro-goals remove unnecessary **forward** coordination. Completion observers remove unnecessary **return-path** coordination.

A mature delegation therefore has both:

    forward channel: durable goal/review contract
    return channel: terminal completion signal for the current attempt

The return channel is best-effort UX. Repository work state remains authoritative.

## The architecturally closed goal

A macro-goal should be:

> **As large as possible while remaining architecturally closed.**

A goal is architecturally closed when likely decisions during execution are already covered by existing architecture, explicit constraints, non-goals, delegated low-level latitude, and acceptance criteria.

Within such a goal, the worker can diagnose, implement, compile, repair directly related failures, retest, and continue to the next authorized subtrack without asking for a fresh prompt.

## Goal identity is semantic, not conversational

A macro-goal is not `one prompt`, `one chat`, `one Codex Goal session`, or `one terminal notification`.

It is the durable semantic objective plus its contract and lineage.

Therefore one macro-goal may span:
- multiple implementation stages;
- multiple worker sessions;
- multiple candidate branches/commits inside one branch lineage;
- multiple director review/correction passes;
- multiple terminal notifications, one per execution attempt.

The goal number advances because the semantic work unit advances, not because an execution container ended.

## What a macro-goal contains

A strong goal specifies:

### Outcome
What state should exist when work is complete?

### Why now
Why is this the next piece of work?

### Starting evidence
What failures or observations motivate the goal?

### Authorized passes
Which related implementation and repair loops are in scope?

### Constraints
Which architecture and compatibility rules apply?

### Non-goals
Which tempting adjacent work is explicitly excluded?

### Acceptance gates
What must be true before the worker may declare attempt-terminal DONE, and what the director ultimately reviews?

### Validation
What commands or evidence classes are required?

### Repository handoff
Goal ID, branch/report lineage, work-state transition, and push behavior.

### Correction continuation policy
What should be reused if director review requests another pass?

Default: same goal ID, same semantic objective, same branch/report lineage; fresh worker session if the previous session terminated.

### Completion observability
How the observer is armed for each execution attempt, what terminal states it observes, and how stale prior-attempt state is prevented from retriggering.

### Human verification
What, if anything, requires a real local machine or subjective observation?

### Stop / escalation conditions
What discovery would require director judgment?

## Goal sizing

Too small:
- every compile error creates another human round trip;
- the worker is prevented from solving obvious local consequences.

Too large:
- the worker must infer priorities;
- architecture becomes implicit;
- unrelated work accumulates;
- failures become hard to review.

The correct size is not measured in files, commits, tokens, prompts, or worker sessions.

It is measured in **decision closure**.

## Macro-goals may have stages and attempts

A macro-goal can contain multiple stages when they share one coherent outcome and the director has already decided the architecture connecting them.

A macro-goal can also contain multiple attempts when director review finds a correctable gap after an earlier worker session has terminalized.

Stages are planned subdivisions inside execution.

Attempts are review-separated executions in the same goal lineage.

## One ready goal

A useful default is at most one authorized goal in `ready/`.

A correction continuation reopens the same goal back to `ready/`; it does not create a second simultaneously authorized goal.

This keeps priority unambiguous, worker invocation simple, branch ownership obvious, and state transitions visible.

## Thin invocation

Initial execution:

> Read AGENTS.md and execute the single authorized macro-goal in docs/work/ready/. Arm the completion observer when provided and continue through all authorized passes until the current attempt terminalizes.

Correction continuation after a terminated session:

> This is a director correction continuation of the same repository goal, not a new macro-goal. Read AGENTS.md, the reopened ready goal, and its director review. Continue the existing branch/report lineage in a fresh worker session and re-arm completion observation for this attempt.

The repository carries the contract and the correction delta.
