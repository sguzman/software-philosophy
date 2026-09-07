# End-to-End Workflow

This is the canonical v1.1 operating loop.

## Phase 0 — establish governance

Before substantial agentic work, create enough durable context that a new agent can navigate the project.

Minimum:
- README map;
- AGENTS entry point;
- product philosophy and scope;
- architecture or invariants;
- current status;
- active roadmap;
- work queue protocol;
- deterministic validation commands.

For long-running local goals, also establish a repository-owned completion observer or explicitly document that none exists yet.

## Phase 1 — human intent

The principal supplies a desire, complaint, idea, taste judgment, observed failure, or change in priorities.

The input may be vague. It does not need to be an implementation plan.

## Phase 2 — director synthesis

The director:
- inspects current repository state;
- resolves what the intent implies;
- updates doctrine if needed;
- updates architecture if needed;
- determines priority;
- defines the next architecturally closed macro-goal;
- commits that shared context.

The director spends reasoning on uncertainty before delegating mutation.

## Phase 3 — thin worker invocation

The human pulls accepted main and invokes the worker with a short instruction pointing at AGENTS and the ready goal.

No giant prompt ferry is required. No separate watcher command should be required when the repository already provides completion-observer machinery.

## Phase 4 — worker activation

The worker:
1. synchronizes from accepted main;
2. creates the goal branch;
3. marks the goal active;
4. automatically launches the repository completion observer for that explicit goal when available;
5. verifies observer startup sufficiently to continue without human intervention.

Observer startup failure is workflow degradation, not automatically a product-goal failure.

## Phase 5 — worker transaction

The worker:
1. inspects relevant code;
2. implements;
3. diagnoses and repairs directly related failures;
4. runs validation;
5. writes a report;
6. marks the goal `done` or `blocked` only at the real terminal state;
7. commits and pushes;
8. restores the shared checkout to main if the local workflow requires it.

The completion observer emits one best-effort terminal notification and exits. The observer must be designed so routine checkout restoration cannot silently erase the terminal event before it is observable.

## Phase 6 — human return / director review

The terminal signal returns attention to the human.

The human need only tell the director that the goal finished or blocked; the director should inspect the repository directly rather than requiring pasted reports.

The director inspects candidate branch, diff, report, tests/evidence, canonical doctrine, and terminal state.

The director accepts, rejects, writes a correction review, or escalates to the human.

## Phase 7 — integration

Accepted work is integrated.

Then update current status, roadmap gate, relevant architecture notes, and next goal.

The repository now represents a new accepted state.

## Phase 8 — human verification when necessary

Only evidence unavailable remotely should routinely return to the human.

Examples include real GPU launch, audio quality, device integration, subjective UI judgment, or `this is not what I wanted`.

The director incorporates the observation into durable repo state.

## The steady-state human loop

    tell director what you want
    pull main
    invoke ready goal
    disengage
    receive done/blocked notification
    tell director the goal terminalized
    optionally perform requested real-machine check
    report taste/runtime observation
    repeat

The goal is not zero human involvement.

The goal is to remove low-value human relay **and low-value human vigilance** while preserving high-value human authorship.
