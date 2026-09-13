# Case Study — Edge TTS Prompt Lifecycle Ambiguity

## Incident

During Edge TTS development, the director correctly identified a bounded new Codex Goal for repairing Online Natural playback in the isolated development profile.

The director issued a complete actionable Goal prompt.

The principal then asked a clarification about worker model/effort and confirmed the correct project folder/branch.

Instead of answering that clarification while preserving the already-settled prompt, the director emitted a second, expanded full Goal prompt without first saying whether it:

- replaced the earlier prompt;
- appended to it;
- merely restated it;
- or represented a new Goal.

The principal was therefore forced to ask which prompt to use.

## Why this was a protocol failure

The content of the second prompt may have been reasonable.

The failure was not primarily semantic quality. It was **untyped prompt mutation**.

The director had cheap access to both prompt variants and implicitly knew their relationship. The principal did not.

The workflow exported several avoidable costs to the human:

- determine which prompt is authoritative;
- compare long variants;
- infer whether instructions should be merged;
- infer whether another Goal/session should be created;
- retain prompt lineage in working memory.

This violated the human-attention principle even though repository-state and implementation architecture were otherwise disciplined.

## Immediate correction

The director eventually stated explicitly:

- use the newer prompt;
- discard the older one;
- do not compare or merge them;
- once an actionable prompt is issued, freeze it;
- if a later replacement is genuinely necessary, explicitly label it as replacement.

That correction became the seed for v1.9 prompt lifecycle doctrine.

## Generalized lesson

Prompt generation is cheap for an agent but prompt reconciliation is expensive for a human.

Therefore:

> **Issuing an actionable prompt creates a freeze boundary.**

Clarification does not dissolve that boundary.

A later semantic change must be typed:

- start new Goal;
- continue current Goal;
- replace prior unsubmitted prompt;
- commentary only / no change.

## Pre-submission vs post-submission

The incident also exposed an important temporal distinction.

### Before submission

If a material defect is discovered, the director may replace the prompt, but must:

1. say `REPLACE THE PREVIOUS CODEX PROMPT`;
2. state briefly why;
3. provide the complete replacement;
4. tell the principal to discard the old prompt;
5. require no manual diff/merge.

### After submission

The original invocation already occurred.

Additional instruction is not a replacement of history. It is:

- continuation of the active session; or
- repository correction continuation if another execution attempt is required.

## What not to do

Do not use these shapes:

    actionable prompt P1
      -> clarification
      -> unlabeled prompt P2
      -> human asks which one governs

or:

    actionable prompt P1
      -> several chat messages
      -> "append this"
      -> "also append this"
      -> human becomes the prompt assembler

## Correct shape

    START A NEW CODEX GOAL
      -> complete prompt P1
      -> P1 frozen

    clarification
      -> COMMENTARY ONLY — NO PROMPT CHANGE

    material pre-submission defect, if any
      -> REPLACE THE PREVIOUS CODEX PROMPT
      -> complete P2
      -> P1 superseded
      -> P2 frozen

    after submission
      -> CONTINUE THE CURRENT CODEX GOAL
      -> bounded additional instruction

## Resulting doctrine

See:

- `docs/21-prompt-lifecycle-discipline.md`;
- `docs/17-prompts-as-repository-artifacts.md`;
- `prompts/README.md`.

The governing human-interface rule is:

> **The principal is not the prompt diff/merge/version-control layer.**
