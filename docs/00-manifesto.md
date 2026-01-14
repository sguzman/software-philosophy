# Manifesto

This is a philosophy for building software that stays readable, operable, and shippable.

## First principles

### 1) Direction beats speed
Shipping fast is only good if you can keep shipping. I optimize for a compounding workflow:
- clear intent
- reproducible builds
- automated checks
- predictable releases

### 2) Declarative beats imperative for "product intent"
Imperative code is powerful, but configuration is where product intent should live.
If a value is a "product decision" (not an algorithm), it belongs in declarative config.

### 3) Constraints are a feature
Tools, formats, and conventions are constraints that:
- reduce decision fatigue
- increase mechanical sympathy
- enable automation and AI assistance

### 4) Automation should be boring
CI and release automation should be unsurprising:
- deterministic
- explainable
- reversible when possible
- logs-first

### 5) AI is an operator, not an authority
AI edits files, proposes patches, and follows documented rules.
The human sets direction and approves outcomes.

## The stack I choose

- Rust: correctness, performance, explicitness, robust tooling culture
- TOML: human-editable configuration that supports structure
- AI-in-editor: fast iteration, but constrained by rules + user intent
- Docs-for-AI: contracts the AI must follow
- Docker: reproducible runtime and deployable units

## What "good" looks like

A good repo has:

- A single "map" document (README) and a small set of deep docs
- A standardized quality gate set (format/lint/validate/test)
- A release pipeline that:
  - knows what changed
  - updates changelog
  - bumps version intentionally
  - tags and publishes predictably
- A configuration surface that:
  - is consistent
  - is validated
  - makes "how to change behavior" obvious

## Anti-goals

- Cleverness as a default
- Hidden build steps
- Implicit version bumps
- "Just trust the AI"
- Unreviewable diff spam
