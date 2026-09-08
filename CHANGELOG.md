# Changelog

## [1.4.0] - 2026-09-08

### Doctrine

- Added a separate **software architecture doctrine** layer distinct from agent-development governance.
- Added **Interactive Thread Isolation** as the first hard architecture invariant: latency-critical GUI/UI threads may orchestrate but must not perform heavy, blocking, unbounded, or externally paced work.
- Clarified legitimate UI-thread work: input handling, lightweight state transitions, frame construction, enqueueing, non-blocking result polling, small result application, and repaint scheduling.
- Added a classification rule based on latency boundedness rather than whether code appears small.
- Added the **Work Queue Boundary** as the current default pattern for expensive UI-triggered work, including cancellation, backpressure, stale-result protection, progress events, and non-blocking result delivery.
- Explicitly documented that Rust `async` does not imply background execution.
- Added a **Rust-first principal implementation profile**: product logic defaults to Rust; configuration, shell/platform bootstrap, package/build metadata, and required integration glue remain normal non-Rust exceptions.
- Added project templates and review checks for architecture principles and language-profile compliance.
- Added first-class ontology for software architecture doctrine, architecture principles/patterns, principal implementation profiles, interactive threads, and work boundaries.
- Documented the v1.4 lineage from repeated egui responsiveness failures to cross-project architecture doctrine.


## [1.3.0] - 2026-09-07

### Doctrine

- Added explicit doctrinal modalities: **prohibition**, **current convention**, and **latent option**.
- Added **ceremony tax** for mechanical human setup/transfer/provenance work that repository automation should own.
- Made the repository the canonical human development/QA execution surface.
- Prohibited asking the principal to download/unpack/run generated CI or agent payloads for ordinary development/manual testing.
- Formalized committed dependency declarations plus idempotent repo-owned materializers/bootstrap.
- Made the director responsible for telling the principal when dependency refresh is required.
- Added the principal's current Windows platform profile: Scoop for ordinary CLI dependencies, ecosystem-native language toolchain declarations, and narrow Windows-native workload exceptions.
- Added a latent-option register so Nix/mise and similar future technologies can be remembered without roadmap pressure or work authorization.
- Added reusable negative-doctrine, options, Windows dependency, bootstrap, and human-verification templates.
- Documented the Lantern Leaf QA-bundle failure and its replacement with `Scoopfile.json`, `deps.ps1`, `qa.ps1`, and repo-owned logs.


## [1.2.0] - 2026-09-07

### Doctrine

- Separated durable **repository macro-goal identity** from ephemeral **worker-session identity**.
- Added **execution attempt**, **goal lineage**, and **correction continuation** as first-class concepts.
- Formalized that worker `done` / `blocked` terminalize an attempt, not necessarily the macro-goal.
- Added cyclic goal transitions: director `REVISE` or correctable rejection can reopen the same goal `done -> ready` for another attempt.
- Required a fresh worker/Codex Goal session when the previous execution session has terminated, while preserving the same repository goal ID.
- Made same-branch/report lineage the correction default, with director authority to require replacement implementation branches when needed.
- Added current-main governance/review synchronization as a correction-session requirement.
- Made completion observation **attempt-aware/re-armable** so stale terminal/ack state from an earlier attempt cannot falsely trigger a later continuation.
- Added reusable correction-review/report/goal templates and a thin correction-continuation prompt.
- Documented the Lantern Leaf Goal 0006 lifecycle bug that motivated the refinement.

## [1.1.0] - 2026-09-07

### Doctrine

- Added **vigilance tax**: the human attention cost of polling long-running delegated work for completion.
- Added the **completion observer** and **completion signal** as first-class workflow concepts.
- Formalized the distinction between worker terminal states (`done` / `blocked`) and director acceptance.
- Defined mature delegation as having both a durable forward contract and a best-effort terminal return channel.
- Made completion-observer startup the implementation worker's responsibility when repository machinery exists.
- Required completion signaling to be detached, durable-state-driven, exactly once, checkout-restoration-safe, and non-fatal to product correctness.
- Explicitly classified notifications as attention routing rather than evidence, review, or integration.
- Added reusable templates for completion-observer behavior and reporting.
- Documented the Lantern Leaf evolution that motivated terminal Windows notifications.

## [1.0.0] - 2026-09-07

### Doctrine

- Recast the project as a repository-mediated operating theory for agentic software development.
- Defined the human principal, director/architect/integrator, implementation worker, repository, doctrine, state, roadmap, macro-goal, evidence, report, review, transaction, and escalation as first-class entities.
- Formalized bounded worker autonomy and director-owned semantic authority.
- Added the architecturally closed macro-goal as the preferred unit of work.
- Added typed evidence and truthful current-state rules.
- Added durable review, integration, and escalation protocols.
- Added reusable project/work templates and thin invocation prompts.
- Documented the lineage from the legacy philosophy through Caliberate and Lantern Leaf.
- Archived the pre-v1 documentation under archive/v0.5/.

## [0.2.0] - 2026-01-14

Legacy stack-centric philosophy generation. Preserved under archive/v0.5/.
