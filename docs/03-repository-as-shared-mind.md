# Repository as Shared Mind

The repository is the central coordination technology of the v1 doctrine.

This does not mean source files are literally intelligent. It means the repository is the durable medium in which the distributed development system stores what it knows, what it wants, what it is doing, what it has proven, and how recurring agent interactions are invoked.

## Why chat cannot be the system of record

Chat has several weaknesses:
- context can be lost or truncated;
- another agent may not see it;
- conclusions are mixed with exploration;
- stale assumptions are hard to detect;
- there is no stable state identity;
- it encourages humans to become couriers;
- reusable invocation wording can fork into incompatible chat variants.

Chat is excellent for thinking. It is poor institutional memory and poor canonical prompt storage.

## Canonical knowledge and protocol layers

A mature agentic repo should separate at least these layers:

    README.md
    AGENTS.md
    ARCHITECTURE.md

    docs/
      project/
        philosophy.md
        product-scope.md
        priorities.md
        current-status.md
        roles-and-workflow.md

      roadmaps/
        active-roadmap.md

      decisions/
        ...

      work/
        README.md
        queued/
        ready/
        active/
        blocked/
        done/
        reports/
        reviews/

    prompts/
      README.md
      execute-ready-goal.md
      continue-corrected-goal.md
      review-pushed-goal.md
      request-human-verification.md

    scripts/
      check
      deps-bootstrap
      qa
      goal-completion-observer

    options/
      ...

Not every project needs exactly these filenames. The separation of concerns matters more than spelling.

## Constitution vs ledger vs invocation protocol

The repository has distinct epistemic/protocol modes.

### Constitution

Normative files say what should remain true: philosophy, architecture, invariants, role authority, and product scope.

### Ledger

Descriptive files say what has actually been observed: current status, reports, test results, review notes, known blockers, and terminal work-state records.

A common failure is treating a plan as evidence. A checked roadmap box is historical metadata, not proof of current behavior.

### Invocation protocol

Prompt artifacts say how recurring interactions with humans/directors/workers are initiated.

They are repository artifacts, but they are intentionally thin. They point to constitution and ledger state rather than duplicating it.

The prompt artifact is durable. The act of pasting or triggering it in an agent UI is transient.

## Git as transport protocol

The director and worker do not need an ongoing live conversation.

    accepted main
      -> director commits doctrine / goal / prompt changes
      -> worker pulls
      -> prompt artifact invokes the repository contract
      -> worker executes on bounded branch
      -> worker pushes branch + report
      -> director inspects branch directly
      -> director accepts / rejects / writes review
      -> accepted result is integrated
      -> current status, roadmap, and recurring prompt artifacts are updated when needed

The repository carries the message and the reusable invocation contract.

## Repository as human workspace

The same principle extends to the principal's local interaction.

The checkout should contain enough durable machinery that routine human testing does not require an alternate package assembled elsewhere.

    pull accepted main
      -> materialize declared dependencies if required
      -> invoke repo-owned QA/build entrypoint
      -> observe product
      -> logs/evidence remain under repo-owned paths

An externally downloaded QA bundle is a competing execution channel. Even if technically convenient for CI, it weakens state identity for the human workflow and should not be used as the principal's development/QA interface.

## Durable state as observation surface

Once work state is represented durably, other local automation can observe it without entering the worker's private process or conversational context.

A completion observer is one example:

    active goal
      -> worker terminalizes to done/blocked
      -> observer notices durable transition
      -> observer emits one best-effort human notification

This preserves the repository as truth while allowing attention to be event-driven.

The observer does not create a new source of project state. It reads the ledger and routes attention.

## Prompt externalization

Recurring prompts are another form of externalized cognition.

Do not pay the human or director to reconstruct:
- the canonical worker invocation;
- the correction-continuation wording;
- the director-review invocation;
- the human-verification request format.

If the interaction is expected to recur, store its canonical prompt as a repository artifact.

The prompt should still remain thin. Its job is to route an agent into the repository, not to become a second repository written in prose.

## Context externalization

Worker intelligence becomes more reliable when project cognition is externalized into files.

Do not pay the worker to rediscover why an architecture exists, which subsystem owns state, what is forbidden, what the next priority is, what counts as done, how completion is surfaced to the human, or what the canonical recurring invocation says.

This is the **externalized cognition principle**:

> The more project reasoning, workflow state, and recurring protocol can be made durable and explicit, the less intelligence and human vigilance each execution step must purchase again.

## Repository health test

Ask:

> Could a capable new agent inspect only the repository at a known commit and understand what the project is, what is authoritative, what is currently true, what work is authorized next, what terminal states mean, how completion is surfaced, what canonical prompt invokes the next interaction, and what would require escalation?

If not, the repository is missing institutional memory or protocol.

Also ask:

> Can the principal perform the requested local test from this checkout, with repository-declared dependencies and a repository-owned command, without fetching an ad hoc runnable payload?

If not, the repository is missing an operational interface.
