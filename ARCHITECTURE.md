# Documentation Architecture

This repository dogfoods the v1 doctrine: durable doctrine lives in Git, authority is explicit, historical state is separated from current authority, and reusable execution contracts are repository-native.

## Canonical layers

### Entry points

- README.md — map and compact doctrine.
- AGENTS.md — authority and behavior for agents working on this repository.
- ARCHITECTURE.md — structure and precedence of the documentation system.

### Doctrine

docs/00-manifesto.md through docs/16-latent-options.md are the canonical v1.3 theory.

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
- future-option preservation without work authorization.

### Reusable protocol

templates/ contains files intended to be copied or adapted into other repositories.

prompts/ contains deliberately thin invocation prompts. They point agents at repository contracts rather than carrying project knowledge themselves.

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
3. current principal/platform conventions;
4. repository-specific canonical architecture and project docs;
5. current goal/review contracts within their delegated scope;
6. current-state evidence;
7. latent options;
8. workflow notification state;
9. historical docs and examples.

A lower layer cannot silently overrule a higher layer.

A completion signal is deliberately below evidence in this ordering. It can route attention but cannot establish truth.

A worker session is deliberately below the repository goal in identity. Ending or resetting a session does not by itself create, close, or renumber durable work.

## Change policy

Changes to terminology should update all current doctrine and templates that depend on the term.

Changes to role authority, transaction semantics, or the principal veto are major-version changes.

Implementation examples may evolve without changing doctrine when they preserve the same coordination semantics.

## Hidden-state prohibition

No issue, chat, prompt, agent scratchpad, worker UI session, or transient notification should be the only location of a decision required to understand current doctrine.

If it matters after the conversation ends, externalize it into the repository.

The same rule applies to human execution: normal development/QA commands, dependency declarations, fixtures, and logs belong to the repo contract rather than an ephemeral download side channel.
