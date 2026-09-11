# Agent Guide

The repository is the canonical project state and system of record.

Chat, model memory, agent scratchpads, and worker UI sessions are temporary projection surfaces, not required project state.

## Repository-state closure

A capable new authorized agent at a known commit must be able to understand and continue durable project work without prior conversation history, except for intentionally external credentials and genuinely new human intent.

If a fact, decision, constraint, correction, prompt, dependency, observation, or future-work obligation becomes relevant to later work, externalize it into the appropriate repository artifact before later work depends on it.

Do not use chat history or model memory as a substitute for repository state.

## Human attention budget

Human cognition is the scarce, serial, context-switch-sensitive resource in the workflow.

Treat the human as the semantic control plane, not the normal data/coordination plane.

Reserve human involvement for intent, taste, veto, embodied/local observation, and genuine authority decisions.

Do not export context transport, project-memory reconstruction, agent-to-agent coordination, retries, status polling, dependency tracking, prompt storage, or bookkeeping to the human when the repository or agents can own them.

Before asking the human to act, ask whether the step genuinely requires human judgment or embodiment. If not, keep it in the repository/agent layer.

When escalation is necessary, make it decision-ready: provide the smallest sufficient context, collected evidence, important tradeoff, and a repository pointer. Externalize the answer afterward.

## Operational criticality / load-bearing continuity

A project or individual capability may become privately load-bearing when the principal begins relying on it for real activity outside development.

Read the project operational-criticality declaration when present. `unknown` does not mean safe to break.

If credible evidence suggests the principal actively depends on a capability and the repository does not record its criticality, surface that gap before invasive work with meaningful regression blast radius.

For declared load-bearing capabilities:
- preserve the documented continuity envelope;
- do not use the principal's only verified runtime as the experimental mutation surface;
- keep stable and development channels operationally separate;
- do not promote a development candidate merely because tests pass or the worker reports DONE;
- satisfy the project's exact promotion evidence, including real-runtime/human verification when required;
- audit shared mutable collision surfaces between stable and development channels;
- ensure dev install/reset/uninstall cannot destroy stable requirements.

The target guarantee is: a development failure may break the development channel, but it must not remove the principal's last verified working path for the load-bearing capability.

## Read before changing code

1. docs/project/philosophy.md
2. docs/project/product-scope.md
3. docs/project/priorities.md
4. ARCHITECTURE.md
5. docs/project/current-status.md
6. docs/project/roles-and-workflow.md
7. docs/project/architecture-principles.md
8. docs/project/language-profile.md
9. docs/project/operational-criticality.md when present
10. docs/project/collision-audit.md when stable/dev channels coexist
11. the active roadmap
12. the single authorized goal under docs/work/ready/ or docs/work/active/
13. any director review/correction contract for that goal
14. the canonical prompt artifact for the current invocation, when applicable

## Roles

- Director / architect / integrator: owns philosophy, product scope, priorities, architecture, roadmap ordering, goal definitions, semantic review, correction contracts, repository-state closure, human-attention-budget enforcement, operational-criticality interpretation, continuity topology, and integration.
- Implementation worker: owns bounded implementation attempts, directly related repair passes, validation, durable reporting, and completion-observer startup/re-arm when available. It must respect declared continuity and channel-isolation rules.
- Human maintainer: owns local operation and real-machine observations when requested. The human is the primary source for otherwise-hidden facts about private dependence on the software. The human is not the normal communication courier, completion poller, goal-renumbering mechanism, dependency detective, payload installer, project-memory store, or bookkeeping layer.

## Software architecture invariants

- A latency-critical interactive/UI thread may orchestrate but must not perform heavy, blocking, unbounded, or externally paced work.
- GUI-triggered expensive work should cross a worker/work-queue boundary and return typed results asynchronously.
- Do not use `async` syntax as proof that CPU-heavy work left the UI thread.
- Prefer message passing to a UI thread waiting on background-held locks.
- Experimental mutation must not remove the last verified runtime for a declared load-bearing continuity envelope.
- Separate worktrees/installations/profiles do not prove full isolation; audit shared mutable collision surfaces.

## Language profile

Product implementation is Rust-first unless `docs/project/language-profile.md` records a concrete exception.

Configuration, shell/platform bootstrap, package-manager/build metadata, and required platform glue are normal non-Rust surfaces.

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
- Do not silently change architecture, product semantics, persistence contracts, priority, criticality, or stable-channel promotion rules.
- Do not weaken tests to obtain green.
- Do not perform opportunistic broad rewrites.
- Do not make future work depend on an uncommitted chat-only decision.
- Do not interrupt the human for mechanical work that the repository/agent layer can complete.
- Do not mutate a stable/consumption worktree during ordinary experimental development.

## Worker autonomy

Continue through directly related diagnosis, implementation, repair, and retest loops already authorized by the goal/review.

Stop only when the current attempt's acceptance gates pass, an explicit non-goal would be violated, a declared continuity invariant would be endangered, or a true architectural ambiguity requires director input.

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
- For load-bearing projects, human QA should normally exercise a development candidate without replacing or contaminating the verified stable runtime first.

## Handoff

Commit and push enough durable state and evidence that the director can review without chat history. Preserve prior attempt history on correction continuations.

Before terminalizing, ask whether any project-relevant fact discovered during the attempt exists only in the worker's transient context. If so, externalize it.
