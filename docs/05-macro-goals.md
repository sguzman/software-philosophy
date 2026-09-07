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

    forward channel: durable goal contract
    return channel: terminal completion signal

The return channel is best-effort UX. Repository work state remains authoritative.

## The architecturally closed goal

A macro-goal should be:

> **As large as possible while remaining architecturally closed.**

A goal is architecturally closed when likely decisions during execution are already covered by existing architecture, explicit constraints, non-goals, delegated low-level latitude, and acceptance criteria.

Within such a goal, the worker can diagnose, implement, compile, repair directly related failures, retest, and continue to the next authorized subtrack without asking for a fresh prompt.

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
What must be true before the worker may declare completion?

### Validation
What commands or evidence classes are required?

### Repository handoff
Branch, report, work-state transition, and push behavior.

### Completion observability
If the repository provides a goal observer, how it is armed, what terminal states it observes, and what failures are non-fatal.

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

The correct size is not measured in files, commits, or tokens.

It is measured in **decision closure**.

## Macro-goals may have stages

A macro-goal can contain multiple stages when they share one coherent outcome and the director has already decided the architecture connecting them.

## One ready goal

A useful default is at most one authorized goal in `ready/`.

This keeps priority unambiguous, worker invocation simple, branch ownership obvious, completion observation specific to one goal, and state transitions visible.

Parallel goals are possible, but they require deliberate isolation rather than accidental concurrency.

## Thin invocation

When the repo is healthy, the human prompt to the worker can be:

> Read AGENTS.md and execute the single authorized macro-goal in docs/work/ready/. Automatically arm the repository completion observer when the protocol provides one, then continue through all authorized passes until acceptance passes or escalation requires stopping.

That is the desired end state: the repository carries the contract, and the worker carries its own completion return path.
