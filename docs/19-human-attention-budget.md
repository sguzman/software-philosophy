# Human Attention Budget

Modality: **HARD DESIGN PRINCIPLE / OPTIMIZATION TARGET**

## Core rule

> **Human cognition is the scarce, serial, context-switch-sensitive resource in the development system. Spend it only where human authority or embodied judgment is actually required.**

The human principal should not be used as project memory, agent-to-agent transport, status poller, dependency tracker, prompt store, retry loop, merge coordinator, or bookkeeping layer.

The repository and agents should absorb those functions.

## Human control plane, not data plane

A useful systems analogy is:

    HUMAN PRINCIPAL
      control plane
      intent / taste / veto / embodied observation / exceptional authorization

    REPOSITORY + AGENTS
      data and coordination plane
      state / context / transport / execution / retries / evidence / monitoring / bookkeeping

The human is the source of semantic authority, not the normal carrier of operational state.

The repository is the conduit between agents and across time.

## Why the human layer is special

Human cognition has properties the workflow must treat as architectural constraints:

- working memory is bounded;
- attention is largely serial;
- context switching is expensive;
- long inactive gaps cause context decay;
- remembering exact operational state is unreliable;
- repetitive mechanical coordination consumes the same attention needed for judgment;
- interruption and uncertainty create disproportionate mental load.

Agents and repository artifacts can reread, search, diff, rehydrate, and transport durable context far more cheaply than a human can keep it live in working memory.

Therefore the workflow should optimize around the human as the most expensive coordination surface.

## Irreducibly human work

Human attention is justified when the task requires one or more of:

- expression of desired ends;
- taste or preference;
- value judgment;
- final veto;
- embodied/local observation unavailable to agents;
- authorization across a genuine authority boundary;
- choosing among materially different outcomes when repository doctrine does not already decide.

These are high-value uses of human cognition.

## Reducible human work

The system should aggressively eliminate human effort spent on:

- remembering project state;
- reconstructing prior chat context;
- copying prompts between agents;
- copying diffs, logs, or error messages between agents that can inspect the repo directly;
- polling for completion;
- tracking worker-session lifecycle;
- remembering dependency/bootstrap order;
- determining whether dependencies changed when the repository can declare that;
- downloading/extracting temporary QA payloads;
- manually reconciling competing state descriptions;
- remembering which branch/report/review is current;
- repeatedly restating architecture, constraints, or acceptance criteria;
- babysitting ordinary retries already inside delegated scope;
- carrying information from one capable agent to another.

If an agent or repository mechanism can deterministically own the work, exporting it to the principal is a design defect.

## Cognitive-load taxes

The existing taxes are special cases of one umbrella cost: **human cognitive load**.

### Prompt tax

The human repeatedly pushes delegated work forward because authority/context was not externalized well enough.

### Vigilance tax

The human repeatedly pulls status back because completion is not observable/event-driven.

### Ceremony tax

The human performs mechanical setup, transport, extraction, provenance, or cleanup work that should be automated or repository-owned.

### Context-reconstruction tax

The human must reload, remember, or explain project state because repository-state closure is incomplete or agent handoff is weak.

### Synchronization tax

The human must determine which agent, branch, report, prompt, dependency state, or session is authoritative because coordination state is ambiguous.

A mature workflow drives all of these toward zero.

## Cognitive offload

**Cognitive offload** is the deliberate transfer of memory, coordination, monitoring, and mechanical decision support from human working memory into durable repository state and agent-owned automation.

Examples:

- architecture decision -> repository architecture document;
- current status -> evidence-backed current-state file;
- recurring invocation -> prompt artifact;
- work authorization -> macro-goal;
- correction -> durable review contract;
- completion awareness -> observer/notification;
- dependencies -> machine-readable declarations + bootstrap;
- agent-to-agent handoff -> Git branch/report/review lineage.

Cognitive offload is not loss of human control.

It preserves control by reserving human attention for choices that actually require the principal.

## Decision-ready escalation

When the system genuinely needs the principal, it should minimize the context the principal must reconstruct.

A good escalation should provide:

- the decision that is actually required;
- the smallest sufficient context;
- relevant evidence already collected;
- the important tradeoff or ambiguity;
- the consequences of the available choices;
- a repository pointer to the full durable state.

Do not dump raw project history on the human and ask them to rediscover the decision boundary.

## Attention-preserving default

Before assigning any task to the human, ask:

> **Does this require human intent, taste, embodied observation, or authority?**

If no, the default answer is:

> **Keep it in the repository/agent layer.**

If yes, ask for only the irreducible human contribution, then externalize the result back into repository state.

## Relationship to repository-state closure

Repository-state closure protects the project from dependence on vanished human/agent memory.

The human-attention principle protects the principal from having to keep that state alive mentally in the first place.

Together:

    repository-state closure
      -> project state lives durably outside the human

    human attention budget
      -> human cognition is reserved for irreducible judgment

This is the intended multi-agent architecture.

## Hard review test

For any workflow step involving the principal, ask:

1. Why must a human do this?
2. Is the required context already in the repository?
3. Could an agent or deterministic repository tool perform the mechanical portion?
4. Can the request be reduced to a smaller decision or observation?
5. After the human responds, will the result be externalized so they are not asked to remember it later?

If the answer reveals avoidable human coordination work, redesign the workflow.

## Optimization target

The governing objective is:

> **Maximize useful autonomous progress per unit of human cognitive load while preserving human semantic control.**

The objective is not to remove the human.

It is to stop wasting the human on machine-shaped work.
