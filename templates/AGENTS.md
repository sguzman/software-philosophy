# Agent Guide

The repository documentation is the system of record.

## Read before changing code

1. docs/project/philosophy.md
2. docs/project/product-scope.md
3. docs/project/priorities.md
4. ARCHITECTURE.md
5. docs/project/current-status.md
6. docs/project/roles-and-workflow.md
7. the active roadmap
8. the single authorized goal under docs/work/ready/ or docs/work/active/
9. any director review/correction contract for that goal

## Roles

- Director / architect / integrator: owns philosophy, product scope, priorities, architecture, roadmap ordering, goal definitions, semantic review, correction contracts, and integration.
- Implementation worker: owns bounded implementation attempts, directly related repair passes, validation, durable reporting, and completion-observer startup/re-arm when available.
- Human maintainer: owns local operation and real-machine observations when requested. The human is not the normal communication courier, completion poller, goal-renumbering mechanism, dependency detective, or payload installer.

## Goal identity vs worker session

A repository macro-goal may span multiple worker/Codex Goal sessions.

If director review reopens the same semantic goal after a prior worker session terminated:
- keep the same repository goal ID;
- start a fresh worker session;
- read the reopened goal and director review;
- continue the existing branch/report lineage unless the review says otherwise;
- re-arm completion observation for the new attempt.

Do not create the next numbered goal merely because an execution session ended.

## Scope discipline

- Implement only the authorized macro-goal and current correction review.
- Respect every non-goal.
- Do not silently change architecture, product semantics, persistence contracts, or priority.
- Do not weaken tests to obtain green.
- Do not perform opportunistic broad rewrites.

## Worker autonomy

Continue through directly related diagnosis, implementation, repair, and retest loops already authorized by the goal/review.

Stop only when the current attempt's acceptance gates pass, an explicit non-goal would be violated, or a true architectural ambiguity requires director input.

## Completion observability

If this repository provides a completion observer:
1. arm a fresh observer epoch for every execution attempt;
2. prevent stale terminal state from a prior attempt under the same goal ID from retriggering;
3. continue the macro-goal normally;
4. terminalize as `done` or `blocked` only at the real end of the current attempt;
5. emit exactly one best-effort signal for that attempt;
6. preserve notification failure as non-fatal workflow UX.

Do not require the human to launch/reset the observer.

Do not treat notification delivery as evidence or director acceptance.

## Repo-native human operations

- Do not instruct the principal to download/unpack/run generated CI or agent payloads for ordinary development/manual QA.
- Keep dependency declarations and bootstrap/check machinery in the repository.
- Use the repository's current platform dependency policy; on the principal's Windows profile, ordinary CLI dependencies use Scoop/Scoopfile.
- If dependencies changed, the director tells the principal when bootstrap needs to run/rerun.
- Latent options such as Nix/mise do not authorize implementation.

## Handoff


Commit and push enough durable evidence that the director can review without chat history. Preserve prior attempt history on correction continuations.
