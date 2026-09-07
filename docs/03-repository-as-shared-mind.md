# Repository as Shared Mind

The repository is the central coordination technology of the v1 doctrine.

This does not mean source files are literally intelligent. It means the repository is the durable medium in which the distributed development system stores what it knows, what it wants, what it is doing, and what it has proven.

## Why chat cannot be the system of record

Chat has several weaknesses:
- context can be lost or truncated;
- another agent may not see it;
- conclusions are mixed with exploration;
- stale assumptions are hard to detect;
- there is no stable state identity;
- it encourages humans to become couriers.

Chat is excellent for thinking. It is poor institutional memory.

## Canonical knowledge layers

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

    scripts/
      goal-completion-observer

Not every project needs exactly these filenames. The separation of concerns matters more than spelling.

## Constitution vs ledger

The repository has two epistemic modes.

### Constitution

Normative files say what should remain true: philosophy, architecture, invariants, role authority, and product scope.

### Ledger

Descriptive files say what has actually been observed: current status, reports, test results, review notes, known blockers, and terminal work-state records.

A common failure is treating a plan as evidence. A checked roadmap box is historical metadata, not proof of current behavior.

## Git as transport protocol

The director and worker do not need an ongoing live conversation.

    accepted main
      -> director commits doctrine / goal
      -> worker pulls
      -> worker executes on bounded branch
      -> worker pushes branch + report
      -> director inspects branch directly
      -> director accepts / rejects / writes review
      -> accepted result is integrated
      -> current status and roadmap are updated

The repository carries the message.

## Durable state as observation surface

Once work state is represented durably, other local automation can observe it without entering the worker's private process or conversational context.

A completion observer is one example:

    active goal
      -> worker terminalizes to done/blocked
      -> observer notices durable transition
      -> observer emits one best-effort human notification

This preserves the repository as truth while allowing attention to be event-driven.

The observer does not create a new source of project state. It reads the ledger and routes attention.

## Context externalization

Worker intelligence becomes more reliable when project cognition is externalized into files.

Do not pay the worker to rediscover why an architecture exists, which subsystem owns state, what is forbidden, what the next priority is, what counts as done, or how completion is surfaced to the human.

This is the **externalized cognition principle**:

> The more project reasoning and workflow state can be made durable and explicit, the less intelligence and human vigilance each execution step must purchase again.

## Repository health test

Ask:

> Could a capable new agent inspect only the repository at a known commit and understand what the project is, what is authoritative, what is currently true, what work is authorized next, what terminal states mean, how completion is surfaced, and what would require escalation?

If not, the repository is missing institutional memory.
