# Changelog

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
