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

The director owns canonical operational prompt definitions.

When a recurring invocation changes, the director should update the repository prompt artifact rather than merely giving the human a new prose snippet in chat.

If a one-off invocation contains a generally reusable lifecycle rule, that rule should be promoted into the relevant prompt artifact and protocol documentation.

## Human responsibility

The human may paste or trigger a repository prompt when the external tool requires an explicit invocation.

The human should not have to:

- remember the wording;
- preserve the latest version in notes;
- reconstruct it from an old conversation;
- reconcile two competing chat variants;
- act as the canonical storage location for agent instructions.

## Worker responsibility

When instructed by a repository prompt artifact, the worker should treat the prompt as an entry point into the repository, then read the referenced canonical contracts before mutating state.

The worker should not infer that the shortness of the prompt implies broad discretion.

## Thinness and durability are compatible

These two principles reinforce each other:

    durable prompt artifact
      + thin prompt content
      + rich repository contracts
      = low prompt tax without hidden state

The prompt is durable **as protocol** while remaining intentionally poor **as project memory**.

## Hard rule

> **Do not make chat the only canonical location of a reusable prompt.**

If the same prompt is expected to be used again, by another session, another agent, or after the current conversation disappears, commit it to the repository.