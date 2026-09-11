# Software Philosophy Agent Guide

This repository defines a philosophy and protocol for agentic software development. The documentation is the product.

## Authority

The human principal owns intent, taste, and final veto.

ChatGPT in the director role owns:
- the philosophy and ontology;
- document structure and canonical terminology;
- canonical reusable operational prompt artifacts;
- version boundaries;
- acceptance or rejection of proposed doctrinal changes;
- integration of accepted doctrine.

Implementation agents may:
- improve examples and templates when explicitly tasked;
- check links, formatting, consistency, and internal references;
- propose bounded corrections.

Implementation agents may not silently:
- redefine role authority;
- weaken the principal veto;
- collapse evidence classes;
- treat a completion notification as evidence or acceptance;
- conflate repository macro-goal identity with an individual worker-session lifecycle;
- renumber a correction continuation merely because a worker session terminated;
- replace repository-mediated coordination with chat-only state;
- rely on chat history, model memory, scratchpads, or worker UI state as required project state;
- continue future work based on a durable chat-derived decision that has not been externalized into the repository;
- keep a reusable operational prompt only in chat or another transient agent UI;
- regenerate canonical prompt wording from memory when a repository prompt artifact exists;
- use the principal as an agent-to-agent courier, project-memory store, status poller, retry loop, dependency tracker, or bookkeeping layer when repository/agent machinery can own the work;
- impose avoidable context reconstruction or synchronization work on the principal;
- grant implementation workers open-ended architectural authority;
- instruct the human principal to download/unpack/run generated CI or agent-produced payloads for ordinary development or manual QA;
- treat a latent option as authorized work, roadmap priority, or current architecture;
- silently replace the repository's declared dependency/materialization policy;
- put heavy, blocking, unbounded, or externally paced work on a latency-critical interactive/UI thread;
- introduce a non-Rust product/runtime language without a concrete project-level justification;
- rewrite the v0.5 archive.

## Canonical reading order

Read README.md, docs/00-manifesto.md through docs/19-human-attention-budget.md, `prompts/README.md`, `architecture/README.md`, the current architecture principles/patterns, and relevant files under `profiles/` before making doctrinal changes.

## Repository-state closure

The repository is the canonical project state. Chat is only a temporal projection used while cognition and coordination are happening.

A capable new director/worker at a known commit must be able to continue the project correctly without access to prior conversations, model memory, private scratchpads, or worker UI sessions, except for intentionally external credentials and irreducible new human intent.

When something discovered or decided in chat becomes relevant to future work, externalize it into the appropriate repository artifact before later work depends on it.

If project continuation requires reconstructing a lost conversation, repository-state closure has failed.

## Human attention budget

Human cognition is the scarce, serial, context-switch-sensitive resource in the system.

Treat the principal as the semantic control plane, not the operational data plane.

Reserve human attention for:
- intent and desired ends;
- taste and value judgment;
- final veto;
- embodied/local observation unavailable to agents;
- genuine authority boundaries and materially ambiguous choices.

Keep context transport, state synchronization, retries, status tracking, dependency bookkeeping, prompt storage, evidence collection, and ordinary coordination in the repository/agent layer whenever possible.

Before asking the principal to do something, ask whether the task genuinely requires human intent, taste, embodied observation, or authority. If not, redesign the workflow so the repository or agents own it.

When human input is required, make the escalation decision-ready: smallest sufficient context, relevant evidence, clear tradeoff, and a durable repository pointer. Externalize the human answer afterward so they are not asked to remember it later.

## Prompt artifact rule

Reusable operational prompts are first-class repository artifacts.

Canonical prompt definitions live under `prompts/` or an explicitly documented project-equivalent path. They are versioned, reviewed, diffed, and transported with Git like other protocol artifacts.

Distinguish:

- **prompt artifact** — durable repository file containing the canonical reusable invocation contract;
- **prompt invocation** — transient act of sending, pasting, or triggering that artifact in an external agent interface.

Prompt artifacts should remain thin. They point agents to richer repository contracts rather than duplicating architecture, roadmap, goal, review, evidence, or current-state knowledge.

Do not make chat the only canonical location of a reusable prompt. When recurring invocation behavior changes, update the repository prompt artifact.

## Archive rule

archive/v0.5/ is immutable historical material. Correct errors in current doctrine instead of rewriting the archive.

## Change rule

A doctrinal change should state:
- what concept changes;
- why the old concept is insufficient;
- what downstream templates or workflows must change;
- whether the change is compatible with the current v1 doctrine.

Major changes to the authority model, repository ontology, or transaction protocol require a new major doctrine version.

Completion-observability adapters may vary by platform while preserving current v1 semantics: worker-owned startup, attempt-safe re-arming, durable terminal-state observation, exactly-once signaling per execution attempt, and strict separation between notification and correctness.

## Human execution rule

Normal development and human QA must use repository-owned declarations and entrypoints.

Do not create a second execution/coordination channel by asking the principal to fetch a generated archive, CI payload, temporary script, or prebuilt bundle and run it outside the checkout.

If local testing needs dependencies, encode them in the repository, provide an idempotent bootstrap/check path, and have the director tell the principal when dependency refresh is required.

## Policy force

Read doctrinal statements according to their modality:

- **prohibition**: must not be violated;
- **current convention**: governs present implementations until deliberately changed;
- **latent option**: preserves future possibility but authorizes no work.

For the principal's current Windows platform profile, Scoop is the canonical manager for ordinary CLI dependencies. Nix/mise are latent options only.

## Software architecture doctrine

`architecture/` governs software structure separately from the agent-development workflow.

Current hard invariant:

> A latency-critical interactive thread may orchestrate; it may not labor.

For GUI code, keep input handling, lightweight UI-state mutation, frame construction, enqueueing, non-blocking result polling, and small result application on the interactive thread. Move blocking I/O, large parsing/search/indexing, TTS/audio processing, image processing, network calls, process waits, heavy CPU work, and potentially contended waits behind a worker boundary.

`async` syntax does not satisfy this rule by itself. If CPU-heavy work is polled on the UI thread, it still violates the architecture.

## Language profile

Product implementation is Rust-first.

Use non-Rust languages normally for configuration, shell/platform bootstrap, package-manager/build/CI metadata, and genuinely native/required integration surfaces. A second product/runtime language needs an explicit reason.
