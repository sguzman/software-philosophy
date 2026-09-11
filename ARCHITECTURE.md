# Documentation Architecture

This repository dogfoods the v1 doctrine: durable doctrine lives in Git, authority is explicit, historical state is separated from current authority, reusable execution contracts are repository-native, project continuation must not depend on vanished conversational state, human cognitive load is treated as a constrained resource, and declared load-bearing software receives explicit continuity protection.

## Canonical layers

### Entry points

- README.md — map and compact doctrine.
- AGENTS.md — authority and behavior for agents working on this repository.
- ARCHITECTURE.md — structure and precedence of the documentation system.

### Doctrine

docs/00-manifesto.md through docs/20-load-bearing-software-continuity.md are the canonical development-governance portion of the v1.8 theory.

They define:
- ontology;
- authority;
- repository memory;
- transactions;
- macro-goals;
- evidence;
- escalation;
- review;
- workflow;
- adoption;
- lineage;
- completion observability and the terminal return channel;
- correction continuations and the separation between logical goal identity and worker-session identity;
- doctrinal modalities: prohibitions, current conventions, and latent options;
- repo-native human execution and the external-payload prohibition;
- dependency declaration/materialization and the Windows Scoop profile;
- future-option preservation without work authorization;
- prompt artifacts as durable repository protocol distinct from transient prompt invocation;
- repository-state closure and chat as a temporal projection of canonical project state;
- the human-attention budget and semantic-control-plane model;
- private load-bearing criticality, continuity envelopes, stable/development channel governance, and evidence-gated promotion.

### Software architecture doctrine

`architecture/` is a separate canonical doctrine layer for the structure of software produced under this philosophy.

Current contents:
- `architecture/principles/` — durable invariants and prohibitions;
- `architecture/patterns/` — reusable structural patterns that satisfy those invariants.

Current hard architecture themes include interactive-thread isolation and load-bearing runtime continuity.

Project-specific `ARCHITECTURE.md` files should specialize these rules, not casually contradict hard architecture prohibitions.

### Principal implementation profiles

`profiles/` records strong current implementation defaults for the principal.

`profiles/rust-first.md` makes Rust the default product implementation language while preserving normal non-Rust configuration/shell/tooling exceptions.

Profiles are current conventions, not universal metaphysical claims.

### Reusable protocol

`templates/` contains files intended to be copied or adapted into other repositories.

Project templates now include operational-criticality and stable/dev collision-audit artifacts so load-bearing continuity can be represented durably rather than left as conversational caution.

`prompts/` contains canonical reusable **prompt artifacts**. These are first-class repository protocol files: durable, versioned, reviewable, and discoverable.

The prompt artifact is not the same thing as the prompt invocation. A Codex Goal box, chat message, CLI command, or other interface may transiently deliver the artifact, but that interface is not its canonical home.

Prompt artifacts should remain deliberately thin: they point agents at repository contracts rather than carrying project knowledge themselves.

`prompts/README.md` defines the prompt-artifact contract.

### Latent option register

`options/` records deliberately non-urgent future possibilities.

An option file is not a roadmap item, not a queued macro-goal, and not an architectural commitment. It preserves optionality until the director or principal explicitly promotes it.

### Historical material

archive/v0.5/ preserves the pre-v1 stack-centric philosophy.

Historical material is context, not current authority.

## Precedence

When material conflicts:

1. explicit human-principal direction for the current decision;
2. current v1 doctrine, including hard prohibitions;
3. software architecture hard invariants;
4. current principal/platform/language profiles;
5. repository-specific canonical architecture and project docs, including operational-criticality/continuity declarations;
6. current goal/review contracts within their delegated scope;
7. current-state evidence;
8. canonical prompt artifacts as invocation protocol;
9. latent options;
10. workflow notification state;
11. historical docs and examples.

A lower layer cannot silently overrule a higher layer.

A prompt artifact is protocol, not independent semantic authority. If it conflicts with the goal, review, doctrine, or architecture it points to, correct the prompt artifact.

A completion signal is deliberately below evidence in this ordering. It can route attention but cannot establish truth.

A worker session is deliberately below the repository goal in identity. Ending or resetting a session does not by itself create, close, or renumber durable work.

A development branch is deliberately below an accepted load-bearing continuity contract: experimental progress does not gain authority to replace the verified consumption runtime without satisfying promotion gates.

## Change policy

Changes to terminology should update all current doctrine and templates that depend on the term.

Changes to role authority, transaction semantics, or the principal veto are major-version changes.

Changes to recurring invocation behavior should update the corresponding repository prompt artifact rather than living only as revised prose in chat.

Any conversational decision that later work will depend on must be promoted into the appropriate repository artifact before it becomes a durable dependency.

When the principal reports or the director reasonably discovers that a project/capability has become load-bearing, update operational-criticality/continuity state before future invasive work depends on the old assumption that the runtime is disposable.

Implementation examples may evolve without changing doctrine when they preserve the same coordination and architecture semantics.

## Repository-state closure

The repository must be sufficient to reconstruct durable project reality at a known commit.

Chat, model memory, agent scratchpads, worker UI state, issue comments, and other transient interfaces may assist cognition and coordination, but they must not become required hidden state for continuing the project.

The hard test is:

> If the conversations and agent-session state vanished, could a capable new authorized director and worker continue correctly from the repository alone, except for intentionally external credentials and genuinely new human intent?

If not, project state has leaked outside the repository.

## Hidden-state prohibition

No issue, chat, prompt invocation, agent scratchpad, worker UI session, model memory, or transient notification should be the only location of a decision or fact required to understand or continue the project.

No transient interface should be the only canonical location of a reusable operational prompt.

No human recollection should be the only location of a load-bearing continuity requirement, stable runtime identity, promotion rule, or known collision hazard.

If it matters after the conversation ends, externalize it into the repository.

The same rule applies to human execution: normal development/QA commands, dependency declarations, fixtures, logs, reusable prompt definitions, accepted decisions, current state, authorized work, operational criticality, and continuity/collision contracts belong to the repo rather than ephemeral side channels.
