# Repository Prompt Artifacts

This directory contains canonical reusable operational prompts.

A file here is a **prompt artifact**: durable, versioned, reviewable protocol state.

The act of pasting, sending, or otherwise invoking that file in ChatGPT, Codex, a CLI, or another interface is a **prompt invocation**: transient delivery.

## Rules

- Reusable prompts live in the repository.
- Chat is not the canonical storage location for a reusable prompt.
- Prompt artifacts should stay thin and point to richer repository contracts.
- Architecture, roadmap, goal, evidence, and state knowledge should not be duplicated into prompt prose when the agent can read it from the repo.
- Changes to recurring invocation behavior should update the corresponding prompt artifact.
- Prompt artifacts are subordinate to higher-authority doctrine, architecture, goal, and review contracts.
- Humans may paste/trigger prompts when an external interface requires it, but they should not have to remember or reconstruct canonical wording.

## Current artifacts

- `execute-ready-goal.md` — invoke the single authorized ready macro-goal.
- `continue-corrected-goal.md` — continue a director-corrected repository goal in a fresh worker session when needed.
- `review-pushed-goal.md` — invoke director review of a pushed candidate attempt.
- `request-human-verification.md` — issue a repo-native human verification request.

The goal is a stable repository-native invocation surface, not a large prompt library that duplicates project knowledge.