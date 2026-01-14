# Toolchain

This document describes the *kinds* of tools I standardize on, what job each tool does, and how they work together.

## Categories

### Formatting
Goal: make diffs meaningful and consistent.

- taplo (TOML)
- biome (JS/TS/JSON)
- (language-specific formatters as needed)

### Linting / Static analysis
Goal: detect mistakes early.

- biome (JS/TS)
- language-specific lints (Rust clippy, etc.) when applicable

### Validation
Goal: reject invalid config/data.

- taplo for TOML validation (schema-based when possible)
- YAML validation where needed (compose files, CI configs)

### Link / reference integrity
Goal: docs should not rot.

- lychee for link checking

### Versioning + changelogs + releases
Goal: releases should be mechanical, not emotional.

- semver as the public contract
- git-cliff for changelog generation
- a generalized "release runner" for bump/tag/release/build

## The generalized release runner (cargo-release vibe, cross-language)

I want one mental model:

1. Decide release intent (major/minor/patch, or pre-release).
2. Ensure the repo is clean and checks pass.
3. Generate/update changelog from commit history.
4. Bump version in the canonical version file(s).
5. Commit the bump + changelog.
6. Tag the release.
7. Publish artifacts as relevant (crates, containers, binaries, etc.).

This should work for:
- Rust workspaces
- JS packages
- Python packages
- Docker images
- Mixed monorepos

The implementation can vary per ecosystem, but the *sequence and contract* stay the same.

## Practical notes

- Tooling should be pinned or at least version-tracked.
- CI should run the same checks developers run locally.
- Tools should be chosen to minimize “it works on my machine”.
