# Prompt Lifecycle Discipline

Modality: **HARD PROTOCOL / HUMAN-ATTENTION SAFETY RULE**

## Core rule

> **Once the director issues an actionable prompt for the human to submit, that prompt is frozen by default. Later discussion does not modify it unless the director explicitly declares a typed prompt transition.**

The human must never have to infer:

- whether a later prompt-like block replaces an earlier one;
- whether it should be appended;
- whether it starts a new Goal;
- whether it continues the current Goal;
- whether it is merely explanatory text;
- which of two competing prompt variants is authoritative.

If the human must compare, merge, or mentally reconcile prompt variants, the protocol has failed.

## Why this rule exists

A language model can generate revised instructions cheaply and repeatedly.

A human cannot cheaply maintain the same prompt lineage in working memory.

Without lifecycle discipline, an apparently helpful clarification creates **prompt synchronization tax**:

    prompt P1 issued
      -> discussion
      -> prompt-shaped P2 appears
      -> human must infer P2 relation to P1
      -> perhaps append, replace, merge, or start another Goal

That pushes machine-easy state reconciliation onto the human.

The correct design is:

    prompt P1 issued
      -> P1 freezes
      -> discussion is commentary by default
      -> any mutation requires explicit typed transition

This is a direct application of the human-attention budget.

## Prompt states

### Draft / planning text

Text is exploratory and not yet authorized for submission.

It should be labeled when confusion is plausible:

> **DO NOT START CODEX — PLANNING ONLY**

A heading such as `Goal:` by itself must not imply that the human should launch a Goal.

### Actionable prompt

An **actionable prompt** is text the director explicitly instructs the human to submit to an external agent/session.

It must declare its invocation relationship.

Examples:

> **START A NEW CODEX GOAL**

or:

> **CONTINUE THE CURRENT CODEX GOAL**

Once emitted as actionable, the prompt enters the **frozen** state.

### Frozen prompt

A **frozen prompt** remains the authoritative human-facing invocation text until one of the explicit transitions below occurs.

Follow-up questions, explanations, planning, interpretation, or ordinary conversation do not mutate it.

Silence means:

> **NO PROMPT CHANGE.**

### Superseded prompt

A prompt becomes superseded only when the director explicitly issues a replacement transition.

The old prompt must be treated as discarded for future submission.

A replacement does not require the human to compare versions or manually merge deltas.

## Required transition vocabulary

When prompt state changes, use an explicit transition label.

### START A NEW CODEX GOAL

Meaning:

- create/use a fresh Goal/session;
- the following prompt is the complete invocation for that new Goal;
- do not append it to an old session unless the text explicitly says otherwise.

The label must be followed by the complete prompt or a canonical repository prompt artifact/path to invoke.

### CONTINUE THE CURRENT CODEX GOAL

Meaning:

- do not create a new semantic repository goal;
- send the following instruction to the currently active worker session when that session remains usable;
- the text is a continuation/correction/addendum to already-submitted work, not a replacement of historical invocation state.

If the prior worker session has terminalized, correction-continuation doctrine decides whether a fresh session should continue the same repository macro-goal.

### REPLACE THE PREVIOUS CODEX PROMPT

Meaning:

- the earlier **unsubmitted** actionable prompt is superseded;
- discard it;
- do not merge or append it;
- the following block is the complete replacement.

The director should state the reason for replacement briefly.

A replacement should normally provide the full prompt, not a patch for the human to apply mentally.

### COMMENTARY ONLY — NO PROMPT CHANGE

Meaning:

- the director is answering questions, explaining, reasoning, or planning;
- the currently frozen actionable prompt remains unchanged;
- do not paste the commentary into Codex unless separately instructed.

Use this label proactively when discussion occurs after an actionable prompt and prompt-like wording could otherwise be mistaken for a mutation.

## Append/addendum discipline

`Append this` is not the default mechanism for changing an unsubmitted prompt.

Before submission:

- if the change is trivial and does not alter execution semantics, prefer commentary and leave the frozen prompt alone;
- if the change materially affects what the worker should receive, issue **REPLACE THE PREVIOUS CODEX PROMPT** and provide one complete replacement.

After submission:

- the original invocation already happened and cannot be retroactively rewritten;
- use **CONTINUE THE CURRENT CODEX GOAL** for bounded additional instruction;
- if repository review requires another execution attempt, use the correction-continuation protocol rather than pretending the first prompt changed.

Only use a literal append instruction when the external interface or workflow genuinely requires fragment composition and there is no cleaner repo-native mechanism. If used, it must say exactly what artifact/message receives the append and whether ordering matters.

## Clarifying questions do not dissolve the freeze

The human may ask questions after receiving a prompt.

The director should answer them without casually regenerating the prompt.

Clarification has three possible outcomes:

1. **No semantic change** — answer the question; prompt remains frozen.
2. **Material defect discovered before submission** — explicitly replace the prompt in full.
3. **Material change discovered after submission** — continue/correct the current repository goal; do not rewrite history.

The existence of a better wording is not by itself a reason to replace a settled prompt.

## Invocation relation must be explicit

Every actionable human-facing prompt should make its relation to existing work obvious:

- new Goal / fresh session;
- continuation of current session;
- correction continuation of same repository macro-goal in a fresh session;
- replacement of an unsubmitted prompt;
- human verification request;
- commentary only / no invocation.

Do not rely on the human to infer this relation from headings, wording, or conversation position.

## Prompt identity

An actionable prompt should have enough identity that the director and human can refer to it unambiguously.

Preferred identity comes from repository state, for example:

- prompt artifact path;
- repository macro-goal ID;
- review/correction path;
- branch/commit when relevant.

For a one-off chat-rendered invocation, a concise semantic name is sufficient if repository identity is already clear.

The goal is not ceremony. The goal is to avoid phrases such as `the newer prompt` when multiple variants exist.

## Relationship to repository prompt artifacts

Repository prompt artifacts remain canonical reusable protocol.

This lifecycle doctrine governs **human-facing invocation state**, including cases where a repository artifact is rendered or where a one-off goal invocation is produced in chat.

The preferred shape is:

    durable repo goal/review/state
      -> canonical thin prompt artifact
      -> explicitly typed invocation
      -> frozen human-facing prompt

If recurring invocation behavior changes, update the repository artifact as already required by `docs/17-prompts-as-repository-artifacts.md`.

Do not solve lifecycle ambiguity by making prompts giant or duplicating project state into chat.

## Relationship to human cognitive load

Prompt ambiguity creates several avoidable taxes:

- **prompt synchronization tax** — determining which prompt is current;
- **merge tax** — manually composing fragments/addenda;
- **invocation ambiguity tax** — determining whether to start, continue, or do nothing;
- **version-comparison tax** — comparing two long prompts to discover what changed.

These are machine-shaped coordination costs and should stay below the human layer.

## Director responsibility

The director owns prompt lifecycle clarity.

The director must:

- explicitly mark actionable invocation type;
- freeze prompts by default after issuance;
- avoid casual rewrites during clarification;
- use full replacement for material pre-submission changes;
- use continuation/correction after submission;
- state when old text is superseded;
- keep commentary visibly non-authoritative when confusion is plausible;
- avoid requiring the human to diff, merge, or infer prompt lineage.

## Human responsibility

The human should only need to:

- submit the clearly identified actionable prompt when ready;
- report whether a requested real-machine observation passed or failed;
- supply intent/clarification when genuinely needed.

The human should not be responsible for prompt version control.

## Worker responsibility

The worker follows the invocation it actually received plus the canonical repository contracts it references.

A worker should not be expected to know about later chat commentary that was never sent and never promoted into repository state.

## Hard review test

After issuing an actionable prompt, ask:

1. Is there exactly one currently authoritative prompt for the human to submit?
2. Is its relation to the worker lifecycle explicit?
3. Would follow-up discussion leave that answer unchanged unless a typed transition occurs?
4. If replacement is necessary, can the human discard the old text without comparing or merging it?
5. If work was already submitted, are new instructions modeled as continuation/correction rather than retroactive prompt mutation?

If any answer is no, the prompt interface is imposing avoidable cognitive load.

## Governing sentences

> **Prompt issuance creates a freeze boundary.**

> **No implicit prompt mutation.**

> **The human must never be the prompt diff/merge engine.**
