# Documentation Architecture

This repository dogfoods the v1 doctrine: durable doctrine lives in Git, authority is explicit, historical state is separated from current authority, and reusable execution contracts are repository-native.

## Canonical layers

### Entry points

- README.md — map and compact doctrine.
- AGENTS.md — authority and behavior for agents working on this repository.
- ARCHITECTURE.md — structure and precedence of the documentation system.

### Doctrine

docs/00-manifesto.md through docs/11-completion-observability.md are the canonical v1.1 theory.

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
- completion observability and the terminal return channel.

### Reusable protocol

templates/ contains files intended to be copied or adapted into other repositories.

prompts/ contains deliberately thin invocation prompts. They point agents at repository contracts rather than carrying project knowledge themselves.

### Historical material

archive/v0.5/ preserves the pre-v1 stack-centric philosophy.

Historical material is context, not current authority.

## Precedence

When material conflicts:

1. explicit human-principal direction for the current decision;
2. current v1 doctrine;
3. repository-specific canonical architecture and project docs;
4. current goal/review contracts within their delegated scope;
5. current-state evidence;
6. workflow notification state;
7. historical docs and examples.

A lower layer cannot silently overrule a higher layer.

A completion signal is deliberately below evidence in this ordering. It can route attention but cannot establish truth.

## Change policy

Changes to terminology should update all current doctrine and templates that depend on the term.

Changes to role authority, transaction semantics, or the principal veto are major-version changes.

Implementation examples may evolve without changing doctrine when they preserve the same coordination semantics.

## Hidden-state prohibition

No issue, chat, prompt, agent scratchpad, or transient notification should be the only location of a decision required to understand current doctrine.

If it matters after the conversation ends, externalize it into the repository.
