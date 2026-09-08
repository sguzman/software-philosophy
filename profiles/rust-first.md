# Rust-First Implementation Profile

Status: **CURRENT CONVENTION**

## Default

> **Product implementation is Rust by default.**

When the principal starts a new software project, the director should assume Rust unless a concrete constraint makes another language materially more appropriate or unavoidable.

This is not a claim that Rust is universally the best language.

It is the principal's actual implementation environment and should be represented explicitly rather than hidden behind false language neutrality.

## What should normally be Rust

Prefer Rust for:
- application/product logic;
- desktop applications;
- CLIs;
- services/daemons;
- libraries;
- parsers and data pipelines;
- engines and long-lived subsystems;
- performance-sensitive utilities;
- core state machines and domain models.

## Normal non-Rust exceptions

Using another language is normal when the artifact belongs natively to another layer, for example:
- TOML/JSON/YAML or equivalent declarative configuration;
- PowerShell for Windows shell/bootstrap integration;
- shell scripts where the host environment genuinely requires them;
- package-manager/build/CI metadata;
- SQL/schema languages;
- vendor-required or platform-required glue where Rust cannot reasonably own the surface.

These are not failures of the Rust-first convention.

## Non-Rust product code requires a reason

Do not introduce Python, JavaScript/TypeScript, C#, Go, or another product/runtime language merely because a local task seems quicker to write there.

A second runtime/language adds:
- dependency surface;
- packaging complexity;
- cross-language state/ownership boundaries;
- debugging/toolchain overhead;
- more environment materialization;
- more architecture for agents to understand.

Use it when those costs are justified, not casually.

## Rust defaults

Unless a project has a reason to differ:
- use stable Rust;
- use edition 2024 for new crates;
- keep toolchain requirements in `rust-toolchain.toml` when useful;
- keep core domain state strongly typed;
- prefer ownership and explicit data flow over global mutable state;
- prefer typed messages across concurrency boundaries;
- keep platform-specific behavior behind explicit modules/traits/`cfg` boundaries;
- make blocking vs async vs CPU-worker execution explicit.

## GUI/concurrency consequence

For Rust GUI applications, especially egui:

    interactive thread
      -> input + lightweight UI state + enqueue + nonblocking result apply

    worker boundary
      -> heavy CPU / I/O / parse / decode / synthesis / search

Rust's safety does not make architectural blocking safe.

An `Arc<Mutex<_>>` that causes the UI to wait is still a bad UI architecture.

An async function that performs CPU-heavy work on the UI executor is still a bad UI architecture.

## Architecture review question

When reviewing a non-Rust addition, ask:

> Is another language genuinely the natural owner of this surface, or are we buying a new runtime to avoid writing Rust?

If the answer is the latter, keep it in Rust.
