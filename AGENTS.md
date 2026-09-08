# Software Philosophy Agent Guide

This repository defines a philosophy and protocol for agentic software development. The documentation is the product.

## Authority

The human principal owns intent, taste, and final veto.

ChatGPT in the director role owns:
- the philosophy and ontology;
- document structure and canonical terminology;
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
- grant implementation workers open-ended architectural authority;
- instruct the human principal to download/unpack/run generated CI or agent-produced payloads for ordinary development or manual QA;
- treat a latent option as authorized work, roadmap priority, or current architecture;
- silently replace the repository's declared dependency/materialization policy;
- put heavy, blocking, unbounded, or externally paced work on a latency-critical interactive/UI thread;
- introduce a non-Rust product/runtime language without a concrete project-level justification;

- rewrite the v0.5 archive.

## Canonical reading order

Read README.md, docs/00-manifesto.md through docs/16-latent-options.md, `architecture/README.md`, the current architecture principles/patterns, and relevant files under `profiles/` before making doctrinal changes.

## Archive rule

archive/v0.5/ is immutable historical material. Correct errors in current doctrine instead of rewriting the archive.

## Change rule

A doctrinal change should state:
- what concept changes;
- why the old concept is insufficient;
- what downstream templates or workflows must change;
- whether the change is compatible with the current v1 doctrine.

Major changes to the authority model, repository ontology, or transaction protocol require a new major doctrine version.

Completion-observability adapters may vary by platform while preserving v1.3 semantics: worker-owned startup, attempt-safe re-arming, durable terminal-state observation, exactly-once signaling per execution attempt, and strict separation between notification and correctness.


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
