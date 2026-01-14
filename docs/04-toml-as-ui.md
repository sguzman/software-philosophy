# TOML as UI (Properties-Based Declarative Programming)

This is the core design move: treat config as the product surface.

## The idea

- Code implements *capabilities*.
- TOML selects and composes those capabilities into *behavior*.

If a change is "a decision" more than "an algorithm", it should be in TOML.

## Principles

### 1) Config must be validated
If TOML is the UI, invalid config is a broken UI.

- define schemas when possible
- fail fast with clear errors
- keep defaults explicit

### 2) Config should be composable
Prefer structures that combine:

- feature flags with parameters
- lists of rules
- named profiles
- clear override behavior

### 3) Config should be explainable
A reader should understand:
- what options exist
- what they do
- what the defaults are
- what happens if omitted

## A suggested shape

- `config.toml` for user-facing intent
- optional `config.schema.json` (or equivalent) for validation
- `docs/config-reference.md` if the config grows large

## Example: "rules" style config

A pattern that scales:

- `[features]` for toggles
- `[limits]` for numeric policy
- `[[rules]]` for repeated structured rules
- `[profiles.<name>]` for named compositions
