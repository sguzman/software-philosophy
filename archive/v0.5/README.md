# Software Philosophy: Tooling + Direction

This repository is my opinionated software philosophy: a practical workflow for building reliable systems fast, with a specific blend of tools and constraints.

The central idea:

- The developer becomes the **creative director**.
- The codebase becomes a **directable system**: declarative where possible, automated where safe, and explicit about quality gates.
- AI becomes an **in-editor operator** that edits files and follows documented rules, driven by user intent and user review.

## The productive combination (my stack)

- **Rust** for general programming and long-term maintainability
- **TOML** for properties-based declarative configuration ("TOML as UI")
- **In-editor AI** that can manipulate files and follow directions
- **Docs for AI to follow** that lean heavily on user input and explicit constraints
- **Docker** for deployment and reproducibility

## Toolchain (quality + release)

These are the kinds of tools I like to standardize across projects:

- **lychee**: link checking (docs stay alive)
- **taplo**: TOML formatting/linting/validation
- **biome**: JS/TS formatting/linting (when relevant)
- **semver**: version meaning and release intent
- **git-cliff**: changelog generation from commit history
- A **generalized release runner** (cross-language "cargo-release vibe"):
  - produces a version bump
  - generates/updates changelog
  - tags/releases
  - optionally builds artifacts and publishes

I do not assume every repo is Rust-only. I want a release process that works for Rust, JS, Python, Docker images, and mixed repos.

## What this repo contains

- `docs/` holds the philosophy in depth:
  - The manifesto and constraints
  - A concrete workflow
  - How AI is used (and bounded)
  - How configuration is structured (TOML as UI)
  - How deployment works (Docker)
  - How releases and changelogs work
  - What quality gates should exist in CI

- `examples/` holds small reference templates that embody the philosophy.

## Reading order

1. `docs/00-manifesto.md` - the core principles
2. `docs/02-workflow.md` - the end-to-end workflow
3. `docs/03-ai-as-creative-director.md` - how AI actually fits
4. `docs/04-toml-as-ui.md` - declarative "properties" design
5. `docs/06-releases-changelogs.md` - the "general cargo-release" concept

## License

CC0-1.0 (public domain dedication). See `LICENSE`.
