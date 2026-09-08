# Software Architecture Doctrine

This layer governs the structure of the software itself.

It is deliberately separate from the agent-development doctrine under `docs/`.

The distinction is:

    development doctrine
      -> who decides, who executes, how work moves, how evidence is reviewed

    software architecture doctrine
      -> how runtime responsibilities, state, concurrency, boundaries, and data flow should be structured

    principal profiles
      -> current implementation defaults such as Rust-first

These layers interact, but they answer different questions.

## Purpose

This directory is the durable home for architectural rules discovered through repeated implementation experience.

A rule can begin as an empirical complaint:

> The GUI keeps freezing because expensive work is being performed in the egui update path.

and be promoted into durable architecture doctrine:

> A latency-critical interactive thread may orchestrate; it may not labor.

## Modalities

Architecture entries use the same doctrinal modalities as the rest of the philosophy:

- **PROHIBITION** — must not be violated without an explicit principal/director exception;
- **CURRENT CONVENTION** — preferred architecture now, revisable when circumstances justify it;
- **PATTERN** — a reusable implementation shape that satisfies one or more principles;
- **LATENT OPTION** — remembered future possibility, not authorized work.

## Current architecture principles

1. `principles/0001-interactive-thread-isolation.md` — keep latency-critical GUI/UI threads free of heavy, blocking, unbounded, or externally paced work.

## Current patterns

1. `patterns/work-queue-boundary.md` — move heavy work through a worker boundary and return typed results to the interactive thread.

## Adding new principles

Prefer rules earned by repeated failures or clear architectural reasoning.

A good architecture principle states:
- the failure mode;
- the invariant;
- what is prohibited;
- what remains allowed;
- default implementation patterns;
- exceptions and how they are justified;
- review questions.

Do not turn every coding preference into architecture doctrine.

Architecture doctrine should constrain decisions that materially affect responsiveness, correctness, ownership, composability, recoverability, or long-term structure.
