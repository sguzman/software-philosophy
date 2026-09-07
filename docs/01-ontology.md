# Ontology of Agentic Software Development

This document defines the entities in the v1 doctrine and the relations between them.

## Principal

The **principal** is the human whose software is being built.

The principal is the source of desired outcomes, taste, utility judgments, acceptable tradeoffs, and final veto.

The principal may delegate interpretation and implementation, but not authorship of their own preferences.

## Director

The **director** is the high-reasoning agent responsible for converting incomplete human intent into durable project governance.

The director owns philosophy, product scope, priorities, architecture, invariants, roadmaps, goal boundaries, semantic review, integration decisions, and current-state interpretation.

The director is a role, not a vendor or model name.

## Implementation worker

The **implementation worker** is an agent with direct repository or filesystem capability.

Its authority is local and delegated. It owns repository inspection needed to execute a goal, file mutation, compilation, deterministic testing, directly related diagnosis and repair, durable reporting, and repository-owned handoff automation assigned by the goal protocol.

It does not own the project merely because it touches the project.

## Repository

The **repository** is the canonical persistent project state visible to all roles.

It may contain product doctrine, architecture, invariants, priorities, current verified status, roadmaps, work contracts, reports, reviews, tests, code, configuration, scripts, and history.

The repository is the shared institutional memory and communication substrate.

## Doctrine

**Doctrine** is durable normative project knowledge: what the project is, what it values, what is forbidden, and how decisions are made.

Doctrine answers: **what ought to be true?**

## Doctrinal modality

A **doctrinal modality** states how much normative force a durable statement carries.

v1.3 distinguishes three primary modalities:

### Prohibition

A **prohibition** is negative doctrine: a workflow or design shape the system must not use.

Example: do not ask the principal to download and run generated development/QA payloads outside the repository.

A prohibition is stronger than a preference and broader than a goal-scoped non-goal.

### Current convention

A **current convention** is positive doctrine for the present operating environment.

It answers: given the current constraints, what mechanism should we use now?

Example: Scoop is the principal's current Windows manager for ordinary CLI dependencies.

### Latent option

A **latent option** is a durable future possibility with deliberately weak force.

It preserves memory and option value without creating roadmap priority, a queued task, implementation authorization, a deadline, or an implication that the current convention is defective.

## Human execution surface

The **human execution surface** is the smallest repository-owned interface through which the principal performs necessary local work.

Examples include `./qa.ps1`, `./deps.ps1`, or `./scripts/check`.

## External payload handoff

An **external payload handoff** occurs when ordinary development or human QA requires the principal to obtain generated runnable material outside the repository workflow, such as a CI ZIP, agent-produced archive, temporary executable bundle, or one-off downloaded script.

For the principal's normal development/testing workflow, external payload handoff is prohibited.

## Ceremony tax

**Ceremony tax** is mechanical human work imposed by the development system that does not require human judgment.

Examples include downloading generated bundles, extracting them, navigating to alternate execution directories, manually reconstructing dependency setup, remembering hidden bootstrap order, or cleaning up temporary handoff artifacts.

Prompt tax wastes human attention by requiring repeated forward coordination. Vigilance tax wastes it by requiring status polling. Ceremony tax wastes it by exporting mechanical setup/handoff work.

A mature repository should drive all three toward zero.

## Dependency declaration

A **dependency declaration** is a committed, machine-readable statement of tools/environment requirements, such as `Scoopfile.json`, `rust-toolchain.toml`, package manifests, or narrowly scoped platform workload declarations.

## Dependency materializer

A **dependency materializer** is repo-owned machinery that turns declarations into an available local environment.

It should be idempotent, inspectable, safe to rerun, and hidden behind a stable repo-owned command where practical.

## Platform profile

A **platform profile** is principal-specific operational policy layered below universal coordination doctrine.

Current Windows profile: ordinary CLI dependencies use Scoop/Scoopfile; language toolchains retain conventional native declarations where appropriate; unavoidable Microsoft compiler/workload installation may use an explicit Windows-native bootstrap exception; human QA uses a repo-owned command.

## Option promotion

**Option promotion** is the explicit act that converts a latent option into evaluated or authorized work.

Until promotion, agents must not spend implementation effort merely because the option exists.

## State

**State** is durable descriptive knowledge about what is true now.

State answers: **what is currently believed, with what evidence?**

Doctrine and state must not be conflated. A roadmap saying something should exist is not proof that it exists.

## Roadmap

A **roadmap** is an ordered theory of change. It expresses sequencing, dependencies, gates, and strategic priority.

A roadmap is director-owned because sequence embodies architecture and priority.

## Repository macro-goal

A **repository macro-goal** is a durable semantic unit of delegated work.

It specifies desired end state, starting evidence, authorized passes, constraints, non-goals, acceptance gates, validation, branch/report lineage, handoff rules, escalation conditions, and when relevant completion-observer behavior.

Its identity is the goal's semantic objective and durable contract, usually represented by a stable goal ID such as `0006`.

A macro-goal may survive multiple worker sessions, multiple candidate attempts, and multiple director reviews.

The goal is the contract. A worker session merely executes against it.

## Worker session

A **worker session** is an ephemeral execution container: for example, one Codex Goal UI session, agent process, terminal lifecycle, or equivalent bounded runtime.

A worker session can terminate even though the repository macro-goal remains unresolved.

Session identity is operational, not semantic.

Therefore:

    repository goal identity != worker session identity

Starting a fresh worker session does not imply a new macro-goal.

## Execution attempt

An **execution attempt** is one bounded pass of a worker session against a repository macro-goal, ending in a candidate terminal state.

A single goal can have:

    G0006
      A1 / Session S1
      A2 / Session S2
      A3 / Session S3

Attempts belong to one goal lineage until the director accepts, abandons, or supersedes the goal.

## Candidate state

A **candidate state** is a worker-produced branch/commit state that claims to satisfy the current goal contract or correction contract.

It is not accepted project reality merely because it compiles, tests pass, or the worker says it is done. Acceptance requires director review.

## Terminal work state

A **terminal work state** is the repository-visible end of one execution attempt.

Typical terminal states are:
- `done`: the worker claims the current attempt satisfies the goal and is ready for director review;
- `blocked`: the current attempt cannot continue without authority or capability outside the goal.

`done` is not the same as `accepted`.

Critically, `done` is not an absorbing state for the macro-goal. A director correction may reopen the same goal:

    ready -> active(A1) -> done -> review: revise -> ready -> active(A2)

## Correction continuation

A **correction continuation** is a director-authored review delta that keeps the same repository macro-goal identity while authorizing another execution attempt.

It normally preserves:
- goal ID;
- semantic outcome;
- original constraints/non-goals unless explicitly amended;
- implementation branch lineage;
- report/review history.

If the previous worker session has terminated, the continuation runs in a **fresh worker session**.

The correction review, not the old session, carries the authority forward.

## Goal lineage

A **goal lineage** is the durable history of one macro-goal across attempts.

It includes the goal contract, candidate branch history, reports, director reviews, correction deltas, evidence, and final disposition.

Goal lineage should make it possible to answer: what was attempted, why it was rejected/revised, what changed next, and what was finally accepted?

## Completion observer

A **completion observer** is a bounded, detached mechanism that watches durable terminal state for one execution attempt and emits a best-effort terminal signal.

It should:
- be armed automatically by the worker rather than manually by the human;
- observe durable repository state or an equally durable attempt signal;
- distinguish `done` from `blocked`;
- notify exactly once per execution attempt terminalization;
- be re-armable for a later correction attempt under the same goal ID;
- survive ordinary worker turn/process changes and checkout restoration;
- exit after signaling;
- remain non-fatal to product correctness.

The observer is infrastructure, not an authority role.

## Completion signal

A **completion signal** is an attention-routing event emitted after an execution attempt terminalizes.

It says: **the current worker attempt stopped; inspect durable state now.**

It does not say the implementation is correct, validation is sufficient, the director accepts the candidate, the macro-goal is closed, or the project is integrated.

## Evidence

**Evidence** is an observation supporting a claim about project state.

Evidence is typed: static inspection, compilation, deterministic tests, hosted platform tests, runtime logs, real-device behavior, or human experiential observation.

Evidence has scope. A Linux compile does not prove Windows runtime behavior.

## Report

A **report** is the worker's durable account of what changed, what was tested, what passed, what failed, what remains uncertain, what deviated from the contract, and which execution attempt produced those claims.

Correction continuations should append or otherwise preserve attempt history rather than erasing the first pass.

A report is a claim about evidence, not a substitute for evidence.

## Review

A **review** is the director's semantic judgment of a candidate attempt against the goal, doctrine, architecture, invariants, and evidence.

A review yields accept, reject, revise, or block.

Reject/revise can either reopen the same macro-goal or, if the semantic objective itself is abandoned/superseded, close it without acceptance.

## Transaction

A **transaction** is the complete movement from one accepted project state to another.

Let:

    R_n = accepted repository state
    G   = durable repository macro-goal
    A_i = execution attempt i under G
    C_i = candidate state from A_i
    E_i = evidence for C_i
    V_i = director review of C_i

Then:

    C_i = A_i(R_n, G, review_delta_i)

    V_i(R_n, G, C_i, E_i)
      -> accept | reject | revise | block

If `revise` or a correctable `reject`:

    G remains G
    next attempt A_(i+1) may run in a fresh worker session

Only acceptance creates:

    R_(n+1)

Implementation, worker-session termination, and integration are therefore three different events.

## Escalation

An **escalation** occurs when continued execution would require authority not already delegated.

Typical escalation boundaries include changing architectural ownership, violating an invariant, selecting between materially different system designs, changing product semantics, weakening acceptance criteria, or inventing new persistence/dependency policy not authorized by the goal.

Escalation is not failure. It is correct containment of unresolved uncertainty.

## Prompt

A **prompt** is an invocation surface, not project memory.

Initial execution can often be invoked with:

> Read AGENTS.md and execute the single authorized goal in docs/work/ready/.

A correction continuation can often be invoked with:

> This is a director correction continuation of repository Goal 0006, not a new macro-goal. Read AGENTS.md, the ready goal, and its director review; continue the existing goal lineage.

If prompts must repeatedly restate architecture or correction details already committed, the repository is under-specified.
