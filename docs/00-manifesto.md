# Manifesto

Software development with AI should not be organized as a conversation that happens to emit code.

It should be organized as a governed system of durable state transitions.

The failure mode is easy to recognize: one capable agent reasons about architecture, another agent can edit the filesystem, and a human spends the day copying prompts, diffs, errors, and status messages between them. The code may advance quickly while the human becomes a low-bandwidth message bus.

A second failure mode appears after delegation improves: the worker can run for a long time, but the human still has to keep checking whether it is finished.

A third failure mode appears when the agents automate themselves but export ceremony back onto the human: download this CI archive, extract it somewhere, trust the generated executable, remember which copy is authoritative, and run a script from outside the repository.

That is not full delegation either. It is coordination debt displaced onto the principal.

A fourth failure mode is subtler: every individual request to the human appears small, but together they force the principal to keep project state, agent state, dependency state, branch state, and unfinished decisions live in working memory. The system technically delegates execution while retaining the human as its fragile synchronization layer.

That is also a design failure.

## The doctrine

**The repository is the shared institutional mind.**

Chat is useful for exploration. Agent context windows are useful for local reasoning. Neither is authoritative memory. Anything required for future work must be committed in a form another agent can recover without reconstructing a lost conversation.

**Human cognition is a budget, not free infrastructure.**

Human working memory is bounded, attention is largely serial, and context switching is expensive. The system must therefore treat avoidable human cognitive load as a cost to be engineered away.

The principal is the **semantic control plane**, not the operational data plane.

Human attention belongs on intent, taste, veto, embodied observation, and genuine authority decisions. Context transport, project-memory persistence, agent synchronization, retries, monitoring, dependency bookkeeping, prompt storage, and mechanical workflow state belong in the repository/agent layer whenever possible.

If an agent or deterministic repository mechanism can do something without human judgment, exporting that work to the principal is a workflow defect.

**Authority is asymmetric.**

The human principal owns desired ends and retains veto power.

The director owns interpretation of intent, architecture, prioritization, decomposition, goal definition, semantic review, and integration.

The implementation worker owns bounded execution: inspect, edit, compile, test, diagnose, and repair inside an authorized goal.

**Autonomy is bounded by architecture, not by prompt count.**

A worker should not need a new prompt after every compiler error or directly related defect. A good goal authorizes a coherent region of problem solving. The worker continues until the acceptance gates pass or a true escalation boundary is reached.

**Delegation should have a return channel.**

A long-running goal should not require the human to poll the worker. The worker should automatically arm a repository-owned, detached completion observer when the project provides one. The observer waits for a real terminal repository state such as `done` or `blocked`, emits one best-effort local notification, and exits.

The signal exists to route attention. It does not prove correctness, satisfy an acceptance gate, or authorize integration.

**Git is more than version control.**

Git is:
- the transaction log;
- the transport protocol between agents;
- the rollback mechanism;
- the identity of a project state;
- the boundary between accepted and candidate reality.

**Tests are evidence, not sovereignty.**

A green suite can prove specific mechanical claims. It cannot decide whether the product should exist in that form, whether architecture remains coherent, whether a UI feels right, or whether a behavior violates intent.

**The human should operate the system, not carry, watch, assemble, or remember it.**

The repository should be the human execution surface as well as the agent communication surface.

For ordinary development and manual QA:

    repository checkout
      -> declared dependencies
      -> repo-owned bootstrap
      -> repo-owned build/QA command
      -> repo-owned logs/evidence

Do not replace this with:

    chat/CI
      -> generated payload
      -> human download
      -> human extraction
      -> ambiguous external execution directory

The latter adds mental load, bandwidth dependence, provenance ambiguity, and another trust boundary while weakening the repository's role as the shared state.

The target human loop is short:
- express intent;
- pull accepted state;
- invoke the ready goal;
- disengage while ordinary authorized work continues;
- receive a terminal completion or blocked notification;
- perform real-machine observation when required;
- make only the decision or judgment that actually requires the principal;
- report taste or runtime facts;
- veto when necessary.

The human should not routinely ferry large prompts from director to worker, patches from worker to director, repeated status queries into the worker, or state/context that two agents could have recovered from the repository themselves.

When a genuine escalation reaches the principal, it should be **decision-ready**: the smallest sufficient context, relevant evidence, meaningful tradeoff, and durable repository pointer should already be prepared. The human should not be handed raw history and asked to reconstruct the decision boundary.

## The optimization target

The goal is not maximum agent activity.

The goal is maximum **useful autonomous progress per unit of human cognitive load** while preserving semantic control.

That requires:
- richer repository context;
- clearer authority;
- larger but architecturally closed goals;
- typed evidence;
- explicit escalation;
- direct agent review through Git;
- durable current-state knowledge;
- terminal completion observability;
- repo-native human execution;
- explicit dependency materialization;
- negative doctrine for known-bad workflow shapes;
- latent options that preserve future possibilities without creating work pressure;
- cognitive offload of memory, synchronization, monitoring, and mechanical coordination;
- decision-ready human escalation.

The philosophy can be summarized in one sentence:

> Humans define ends and exercise irreducible judgment; directors govern meaning; repositories preserve state, context, and execution contracts; workers perform bounded transformations; agents and automation absorb machine-shaped coordination; evidence constrains belief; completion signals route attention; dependencies are materialized from the repo; and Git makes every accepted change explicit and reversible.
