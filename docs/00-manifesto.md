# Manifesto

Software development with AI should not be organized as a conversation that happens to emit code.

It should be organized as a governed system of durable state transitions.

The failure mode is easy to recognize: one capable agent reasons about architecture, another agent can edit the filesystem, and a human spends the day copying prompts, diffs, errors, and status messages between them. The code may advance quickly while the human becomes a low-bandwidth message bus.

That is not automation. It is coordination debt.

## The doctrine

**The repository is the shared institutional mind.**

Chat is useful for exploration. Agent context windows are useful for local reasoning. Neither is authoritative memory. Anything required for future work must be committed in a form another agent can recover without reconstructing a lost conversation.

**Authority is asymmetric.**

The human principal owns desired ends and retains veto power.

The director owns interpretation of intent, architecture, prioritization, decomposition, goal definition, semantic review, and integration.

The implementation worker owns bounded execution: inspect, edit, compile, test, diagnose, and repair inside an authorized goal.

**Autonomy is bounded by architecture, not by prompt count.**

A worker should not need a new prompt after every compiler error or directly related defect. A good goal authorizes a coherent region of problem solving. The worker continues until the acceptance gates pass or a true escalation boundary is reached.

**Git is more than version control.**

Git is:
- the transaction log;
- the transport protocol between agents;
- the rollback mechanism;
- the identity of a project state;
- the boundary between accepted and candidate reality.

**Tests are evidence, not sovereignty.**

A green suite can prove specific mechanical claims. It cannot decide whether the product should exist in that form, whether architecture remains coherent, whether a UI feels right, or whether a behavior violates intent.

**The human should operate the system, not carry it.**

The target human loop is short:
- express intent;
- pull accepted state;
- invoke the ready goal;
- perform real-machine observation when required;
- report taste or runtime facts;
- veto when necessary.

The human should not routinely ferry large prompts from director to worker or patches from worker to director.

## The optimization target

The goal is not maximum agent activity.

The goal is maximum **useful autonomous progress per unit of human coordination** while preserving semantic control.

That requires:
- richer repository context;
- clearer authority;
- larger but architecturally closed goals;
- typed evidence;
- explicit escalation;
- direct agent review through Git;
- durable current-state knowledge.

The philosophy can be summarized in one sentence:

> Humans define ends, directors govern meaning, repositories preserve state, workers perform bounded transformations, evidence constrains belief, and Git makes every accepted change explicit and reversible.
