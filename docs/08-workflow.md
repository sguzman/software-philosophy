# End-to-End Workflow

This is the canonical v1.2 operating loop.

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

The director inspects current repository state, resolves implications, updates doctrine/architecture if needed, determines priority, defines the next architecturally closed macro-goal, and commits that shared context.

## Phase 3 — initial worker session

The human pulls accepted main and starts one worker/Codex Goal session with a thin instruction pointing at AGENTS and the ready goal.

No giant prompt ferry is required. No separate watcher command should be required when the repository provides completion-observer machinery.

## Phase 4 — worker activation and attempt

The worker:
1. synchronizes from accepted main;
2. creates the goal branch or enters the branch named by the goal;
3. moves the goal `ready -> active`;
4. arms a fresh completion-observer epoch for this execution attempt;
5. executes all authorized passes;
6. validates;
7. writes/updates the durable report;
8. moves the goal to `done` or `blocked` only at the real terminal state;
9. commits and pushes;
10. signals terminal state and restores the shared checkout as required.

The completion observer emits one best-effort terminal notification for this attempt and exits.

## Phase 5 — director review

The human only needs to tell the director that the worker attempt terminalized. The director inspects Git directly.

The director chooses:

### Accept
Integrate the candidate, update project state, and close the macro-goal transaction.

### Revise / correctable reject
Keep the same repository macro-goal identity.

The director:
1. writes a durable review/correction contract on accepted main;
2. preserves the goal ID;
3. normally preserves the implementation branch and report lineage;
4. moves/reopens the same goal back to `ready/`;
5. records whether the next attempt should keep or replace the implementation approach.

### Block
Record the unresolved decision. Once resolved, reopen the same goal if its semantic objective remains unchanged.

### Abandon / supersede
Close the old goal without acceptance. Create a new goal ID only when the semantic work unit itself changes.

## Phase 6 — correction continuation in a fresh worker session

If the prior worker/Codex Goal session already terminated, **start a new worker session**.

Do not create a new repository macro-goal merely because the UI session ended.

The human:
1. pulls the director's correction on main;
2. starts/resets a fresh worker session;
3. gives the thin correction-continuation prompt.

The worker:
1. reads AGENTS, the reopened ready goal, and the director review from current main before mutating;
2. fetches/switches to the existing goal branch unless the review explicitly requires a replacement branch;
3. brings the current director-owned correction/governance state into the working branch using the repository's safe Git policy;
4. moves the same goal `ready -> active` for the new attempt;
5. re-arms completion observation so stale prior-attempt terminal state cannot retrigger;
6. executes the correction contract;
7. appends/preserves report history;
8. terminalizes and pushes again.

Then return to Phase 5.

## Phase 7 — integration

Accepted work is integrated.

Then update current status, roadmap gate, relevant architecture notes, and next goal.

The repository now represents a new accepted state.

## Phase 8 — prepare repo-native human verification

Before asking the human to test, the director verifies that the repository owns the local execution path.

The request should identify:
- the accepted commit/main state to pull;
- whether dependencies changed;
- whether `deps.ps1`, `scoop import`, or an equivalent repo bootstrap must be run/rerun;
- the single repo-owned QA/build command;
- the observation needed from the human.

Do **not** ask the principal to download, unpack, or run a generated CI/agent payload for ordinary development or manual QA.

If the environment is not ready, repair the repository bootstrap path rather than exporting setup ceremony to the human.

## Phase 9 — human verification when necessary

Only evidence unavailable remotely should routinely return to the human, and it should be collected through the repo-native execution surface.

Examples include real GPU launch, audio quality, device integration, subjective UI judgment, or `this is not what I wanted`.

The director incorporates the observation into durable repo state.

## The cyclic goal state machine

    queued -> ready -> active(A1) -> done
                                  |
                                  -> blocked

    done -> director review -> accept -> integrated/closed
                           |
                           -> revise/correctable reject -> ready -> active(A2) -> ...

    blocked -> decision resolved -> ready -> active(A2) -> ...

`done` is terminal for an **attempt**, not necessarily for the macro-goal.

## The steady-state human loop

    tell director what you want
    pull main
    start worker session
    disengage
    receive attempt done/blocked notification
    tell director
    if accepted: move to next goal
    if correction required:
        pull same goal correction
        start fresh worker session
        continue same goal ID
    if real-machine check requested:
        director tells you whether deps need refresh
        run repo-owned QA command
        report observation

The goal is not zero human involvement.

The goal is to remove low-value relay, vigilance, and accidental work renumbering while preserving high-value human authorship.
