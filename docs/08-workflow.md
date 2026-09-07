# End-to-End Workflow

This is the canonical v1.0 operating loop.

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

No giant prompt ferry is required.

## Phase 4 — worker transaction

The worker:
1. synchronizes from accepted main;
2. creates the goal branch;
3. marks the goal active;
4. inspects relevant code;
5. implements;
6. diagnoses and repairs directly related failures;
7. runs validation;
8. writes a report;
9. marks done or blocked;
10. commits and pushes;
11. restores the shared checkout to main if the local workflow requires it.

## Phase 5 — director review

The director directly inspects:
- candidate branch;
- diff;
- report;
- tests and evidence;
- canonical doctrine.

The director accepts, rejects, writes a correction review, or escalates to the human.

## Phase 6 — integration

Accepted work is integrated.

Then update:
- current status;
- roadmap gate;
- relevant architecture notes;
- next goal.

The repository now represents a new accepted state.

## Phase 7 — human verification when necessary

Only evidence unavailable remotely should routinely return to the human.

Examples:
- real GPU launch;
- audio quality;
- device integration;
- subjective UI judgment;
- “this is not what I wanted.”

The director incorporates the observation into durable repo state.

## The steady-state human loop

    tell director what you want
    pull main
    invoke ready goal
    optionally perform requested real-machine check
    tell director the observation
    repeat

The goal is not zero human involvement.

The goal is to remove low-value human relay while preserving high-value human authorship.
