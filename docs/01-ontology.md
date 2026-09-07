# Ontology of Agentic Software Development

This document defines the entities that exist in the v1.0 model and the relations between them.

## Principal

The **principal** is the human whose software is being built.

The principal is the source of:
- desired outcomes;
- taste;
- utility judgments;
- acceptable tradeoffs;
- final veto.

The principal may delegate interpretation and implementation, but not authorship of their own preferences.

## Director

The **director** is the high-reasoning agent responsible for converting incomplete human intent into durable project governance.

The director owns:
- philosophy;
- product scope;
- priorities;
- architecture;
- invariants;
- roadmaps;
- goal boundaries;
- semantic review;
- integration decisions;
- current-state interpretation.

The director is a role, not a vendor or model name.

## Implementation worker

The **implementation worker** is an agent with direct repository or filesystem capability.

Its authority is local and delegated. It owns repository inspection needed to execute a goal, file mutation, compilation, deterministic testing, directly related diagnosis and repair, and a durable report of work and evidence.

It does not own the project merely because it touches the project.

## Repository

The **repository** is the canonical persistent project state visible to all roles.

It may contain:
- product doctrine;
- architecture;
- invariants;
- priorities;
- current verified status;
- roadmaps;
- work contracts;
- reports;
- reviews;
- tests;
- code;
- configuration;
- scripts;
- history.

The repository is the shared institutional memory and communication substrate.

## Doctrine

**Doctrine** is durable normative project knowledge: what the project is, what it values, what is forbidden, and how decisions are made.

Doctrine answers: **what ought to be true?**

## State

**State** is durable descriptive knowledge about what is true now.

State answers: **what is currently believed, with what evidence?**

Doctrine and state must not be conflated. A roadmap saying something should exist is not proof that it exists.

## Roadmap

A **roadmap** is an ordered theory of change. It expresses sequencing, dependencies, gates, and strategic priority.

A roadmap is director-owned because sequence embodies architecture and priority.

## Macro-goal

A **macro-goal** is a temporary delegation of transformation authority.

It specifies:
- desired end state;
- starting evidence;
- authorized passes;
- constraints;
- non-goals;
- acceptance gates;
- validation;
- branch and handoff rules;
- escalation conditions.

The goal is the contract. The prompt merely invokes it.

## Candidate state

A **candidate state** is a worker-produced branch or commit that claims to satisfy a macro-goal.

It is not accepted project reality merely because it compiles, tests pass, or the worker says it is done. Acceptance requires review.

## Evidence

**Evidence** is an observation supporting a claim about project state.

Evidence is typed: static inspection, compilation, deterministic tests, hosted platform tests, runtime logs, real-device behavior, or human experiential observation.

Evidence has scope. A Linux compile does not prove Windows runtime behavior.

## Report

A **report** is the worker's durable account of what changed, what was tested, what passed, what failed, what remains uncertain, and what deviated from the contract.

A report is a claim about evidence, not a substitute for evidence.

## Review

A **review** is the director's semantic judgment of a candidate state against the goal, doctrine, architecture, invariants, and evidence.

A review yields:
- accept;
- reject;
- revise;
- block.

## Transaction

A **transaction** is the complete movement from one accepted project state to another.

Let:

    R_n = accepted repository state
    G   = authorized macro-goal
    W   = worker transformation
    C   = candidate state
    E   = evidence
    V   = director review

Then:

    C = W(R_n, G)

    V(R_n, G, C, E)
      -> accept | reject | revise | block

Only acceptance creates:

    R_(n+1)

Implementation is therefore not the same thing as integration.

## Escalation

An **escalation** occurs when continued execution would require authority not already delegated.

Typical escalation boundaries:
- changing architectural ownership;
- violating an invariant;
- selecting between materially different system designs;
- changing product semantics;
- weakening acceptance criteria;
- inventing new persistence or dependency policy not authorized by the goal.

Escalation is not failure. It is correct containment of unresolved uncertainty.

## Prompt

A **prompt** is an invocation surface, not project memory.

A mature repository should make many prompts extremely small:

> Read AGENTS.md and execute the single authorized goal in docs/work/ready/.

If a prompt must repeatedly restate architecture, the repository is under-specified.
