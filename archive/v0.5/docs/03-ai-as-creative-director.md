# AI as Creative Director

The phrase "the user becomes the creative director" means:

- The human sets goals, constraints, and taste.
- The AI is an operator that executes changes and proposes options.
- The repo is shaped so an AI can be useful without being dangerous.

## What AI is good for

- editing and refactoring files
- generating boilerplate
- wiring configs and documentation
- suggesting edge cases
- producing consistent formatting and structure
- writing migration notes and release notes (from diffs)

## What AI is not allowed to decide

- product direction
- security posture changes without explicit instruction
- licensing changes
- dependency additions without explicit instruction
- silent behavior changes that violate documented intent

## The "AI rules" pattern

Every repo should include a doc the AI must follow (example in `examples/ai-guides/AI_RULES.md`).

That rules doc should specify:

- required checks to run
- how to format/validate files
- what constitutes "done"
- what to do when something fails
- logging expectations
- how to write commits and changelog entries

## A practical collaboration loop

1. Human: "Here is the intent and constraints."
2. AI: proposes plan + file list + risks.
3. Human: confirms direction (not implementation details).
4. AI: makes edits, runs checks, reports results.
5. Human: reviews diff and outcome.
6. Repeat in small increments.
