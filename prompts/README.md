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
- Humans may paste/trigger prompts when an external interface requires it, but they should not have to remember, reconstruct, diff, merge, or reconcile canonical wording.

## Human-facing invocation lifecycle

Repository storage does not by itself solve conversational prompt ambiguity.

Once the director issues an actionable prompt for the human to submit, that prompt is **frozen by default**.

Follow-up discussion does not modify it unless the director explicitly declares a typed transition.

Use these labels when applicable:

- **START A NEW CODEX GOAL** — the following text is the complete invocation for a fresh Goal/session.
- **CONTINUE THE CURRENT CODEX GOAL** — send the following instruction to the already-invoked current work/session; do not create a new semantic repository goal merely because new instruction is needed.
- **REPLACE THE PREVIOUS CODEX PROMPT** — the earlier unsubmitted prompt is superseded; discard it; the following text is the complete replacement. Do not merge variants.
- **COMMENTARY ONLY — NO PROMPT CHANGE** — explanatory/planning text only; the frozen prompt remains authoritative.
- **DO NOT START CODEX — PLANNING ONLY** — no actionable invocation has been issued.

A heading like `Goal:` by itself is not a lifecycle instruction.

## Replacement vs continuation

Before submission, a material correction should normally be a **full replacement**, not `append this`.

After submission, the original invocation is historical fact. New instruction should be a **continuation/correction**, not a retroactive rewrite of the first prompt.

Literal fragment-appending is exceptional and should be used only when the external interface genuinely requires it. If used, the target and ordering must be explicit.

See `docs/21-prompt-lifecycle-discipline.md` for the full protocol.

## Current artifacts

- `execute-ready-goal.md` — invoke the single authorized ready macro-goal.
- `continue-corrected-goal.md` — continue a director-corrected repository goal in a fresh worker session when needed.
- `review-pushed-goal.md` — invoke director review of a pushed candidate attempt.
- `request-human-verification.md` — issue a repo-native human verification request.

The goal is a stable repository-native invocation surface with explicit lifecycle semantics, not a large prompt library that duplicates project knowledge.