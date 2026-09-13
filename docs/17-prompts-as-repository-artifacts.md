# Prompts as Repository Artifacts

Prompts are part of the repository protocol.

The durable prompt definition belongs in Git.

> **A reusable operational prompt is a first-class repository artifact.**

Chat, a Codex Goal box, a CLI invocation, or another agent interface may *deliver* a prompt. Those interfaces are invocation surfaces. They are not the canonical home of the prompt.

## Artifact vs invocation

The doctrine distinguishes:

    prompt artifact
      = durable, versioned repository file

    prompt invocation
      = transient act of sending/using that artifact

This resolves an ambiguity in the earlier phrase `a prompt is an invocation surface, not project memory`.

The intended meaning is:

- the prompt should remain a thin invocation contract rather than duplicating architecture, roadmap, or work-state knowledge;
- **the reusable prompt itself should still be stored in the repository**;
- the invocation may be copied into a UI, sent by an agent, or eventually invoked automatically;
- reconstructing the canonical prompt from chat memory is a workflow failure.

## Canonical location

A repository should normally expose reusable operational prompts under:

    prompts/

Examples:

    prompts/
      README.md
      execute-ready-goal.md
      continue-corrected-goal.md
      review-pushed-goal.md
      request-human-verification.md

Project-specific names may differ, but prompts must remain discoverable from repository entry points such as `AGENTS.md` or the work protocol.

## What belongs in a prompt artifact

A prompt artifact should contain only the invocation information that must cross the interface boundary.

Prefer pointers to durable repository contracts:

> Read `AGENTS.md` and execute the single authorized macro-goal under `docs/work/ready/`.

Do not duplicate the entire architecture, acceptance contract, or project history into the prompt.

The repository owns those facts.

## Why prompts belong in Git

Repository-native prompts are:

- **versioned** — the exact invocation contract used at a project state can be recovered;
- **reviewable** — director changes to agent instructions have visible diffs;
- **shared** — human, director, and worker can refer to the same artifact;
- **discoverable** — a new agent does not depend on hidden chat history;
- **reversible** — bad prompt changes can be reverted;
- **composable** — tooling can later invoke or render them without inventing prompt text;
- **low-ceremony** — the human does not have to preserve prompt snippets elsewhere.

## Authority

Prompt artifacts are protocol artifacts, not independent sources of architectural authority.

Their content must point into and remain consistent with higher-authority repository doctrine, architecture, goals, reviews, and current state.

If a prompt artifact conflicts with those sources, the higher-authority repository contract wins and the prompt should be corrected.

## Director responsibility

The director owns canonical operational prompt definitions **and human-facing prompt lifecycle clarity**.

When a recurring invocation changes, the director should update the repository prompt artifact rather than merely giving the human a new prose snippet in chat.

If a one-off invocation contains a generally reusable lifecycle rule, that rule should be promoted into the relevant prompt artifact and protocol documentation.

Once the director emits an actionable prompt for human submission, that human-facing prompt freezes by default. Later discussion does not mutate it unless the director explicitly declares a typed transition such as:

- `START A NEW CODEX GOAL`;
- `CONTINUE THE CURRENT CODEX GOAL`;
- `REPLACE THE PREVIOUS CODEX PROMPT`;
- `COMMENTARY ONLY — NO PROMPT CHANGE`.

See `docs/21-prompt-lifecycle-discipline.md`.

## Human responsibility

The human may paste or trigger a repository prompt when the external tool requires an explicit invocation.

The human should not have to:

- remember the wording;
- preserve the latest version in notes;
- reconstruct it from an old conversation;
- reconcile two competing chat variants;
- infer whether a later block replaces, appends to, or merely comments on an earlier prompt;
- diff two long prompt variants to discover what changed;
- act as the canonical storage location or version-control mechanism for agent instructions.

## Worker responsibility

When instructed by a repository prompt artifact, the worker should treat the prompt as an entry point into the repository, then read the referenced canonical contracts before mutating state.

The worker should not infer that the shortness of the prompt implies broad discretion.

The worker follows the invocation it actually received plus canonical repository state; it is not expected to know about later chat commentary that was never sent or promoted.

## Thinness and durability are compatible

These principles reinforce each other:

    durable prompt artifact
      + thin prompt content
      + explicit invocation lifecycle
      + rich repository contracts
      = low prompt tax without hidden state

The prompt is durable **as protocol** while remaining intentionally poor **as project memory**.

## Prompt freeze boundary

Prompt durability and prompt freeze are different but complementary concepts.

- repository artifact durability answers: **where does the reusable prompt live?**
- prompt lifecycle discipline answers: **which human-facing invocation currently governs, and how may it change?**

An actionable prompt creates a freeze boundary. Clarifying discussion does not implicitly cross it.

Before submission, a material correction should normally supersede the old prompt with one complete replacement rather than asking the human to merge fragments.

After submission, new instruction is a continuation/correction of work already invoked, not a retroactive rewrite of the original invocation.

## Hard rules

> **Do not make chat the only canonical location of a reusable prompt.**

> **Do not implicitly mutate an actionable prompt after issuance.**

If the same prompt is expected to be used again, by another session, another agent, or after the current conversation disappears, commit it to the repository.

If an already-issued prompt must change, type the transition explicitly so the human never has to infer prompt lineage.