# Releases, Changelogs, and SemVer

This doc explains how I want "meaningful releases" to work.

## SemVer as the contract

SemVer is a promise to downstream users:

- MAJOR: breaking change
- MINOR: new features, backwards compatible
- PATCH: bug fixes, backwards compatible

Even if the world argues about SemVer, I use it as an internal discipline tool:
it forces me to say what kind of change I believe I made.

## Changelog generation (git-cliff model)

The changelog should be:

- generated from commit history
- grouped by type (feat/fix/etc.)
- edited only when necessary (not handcrafted by default)

## Commit conventions (for clean automation)

I prefer commits that are machine-readable and human-meaningful.

A generic pattern (example):

- `feat(scope): add X`
- `fix(scope): correct Y`
- `refactor(scope): simplify Z`
- `docs(scope): update usage`
- `chore(scope): tooling`

If you want breaking-change detection, include an explicit marker and make it consistent.

## The generalized release runner

The job is to make releases boring across languages.

The release runner should:

1. ensure clean working tree
2. run quality gates
3. generate changelog
4. bump version (major/minor/patch or pre-release)
5. commit changelog + version bump
6. tag
7. trigger CI publish/build jobs

## Outputs of a release

At minimum:

- a git tag
- a changelog entry
- a GitHub Release (optional but preferred)

Optionally:

- published packages
- built binaries
- Docker image pushes
