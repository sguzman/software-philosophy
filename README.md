# Software Philosophy v1.2

A repository-mediated operating system for agentic software development.

The core idea:

> The repository is the durable shared mind. The human supplies intent and taste. The director converts intent into doctrine, architecture, roadmaps, goals, and review. The implementation worker performs bounded transformations. Tests produce mechanical evidence. Git transports, records, and reverses state. Completion observers return attention at terminal execution states. Repository macro-goals persist across disposable worker sessions until the director accepts, abandons, or supersedes them.

This repository is not primarily about Rust, TOML, Docker, Codex, ChatGPT, PowerShell, or Windows notifications. Those are contingent tools. The doctrine is about how to organize authority, knowledge, work, evidence, communication, execution lifecycles, and human attention when software is built by a human principal plus multiple AI agents with different capabilities.

## Operating topology

    HUMAN PRINCIPAL
      intent / taste / veto
            |
            v
    DIRECTOR / ARCHITECT / INTEGRATOR
      philosophy / product scope / architecture
      priorities / roadmaps / macro-goals
      semantic review / integration
            |
            v
    REPOSITORY MACRO-GOAL G
      stable semantic identity / contract / lineage
            |
            v
    WORKER SESSION S1
      bounded execution + observer
            |
            v
    CANDIDATE C1 + REPORT + EVIDENCE
            |
            v
    DIRECTOR REVIEW
       | accept --------------------> integrate / close G
       |
       + revise/reject-correctable
            |
            v
      reopen SAME GOAL G
      durable review correction
            |
            v
    FRESH WORKER SESSION S2
      same goal ID / continuing lineage

The human is deliberately neither the courier between agents nor the polling loop around them.

## v1.2 doctrine

1. **Persist cognition that matters.** Important project knowledge belongs in the repository, not only in chat.
2. **Separate authority from execution.** The agent best suited to architecture should not spend its attention babysitting file edits; the filesystem-capable worker should not invent the project.
3. **Delegate bounded autonomy.** A worker gets enough latitude to finish a coherent goal, including directly related repair loops, but not enough authority to silently redefine architecture.
4. **Make prompts thin.** A prompt should usually point at a committed goal or correction review, not restate the project.
5. **Treat implementation as a transaction.** There is a known accepted state, an authorized transformation, candidate attempts, evidence, review, and an explicit integration decision.
6. **Type the evidence.** Compile success, deterministic tests, hosted runtime probes, real-device behavior, and human judgment are different evidence classes.
7. **Prefer truthful incompleteness over fake certainty.** Current-state docs distinguish verified, inferred, historical, blocked, and unverified claims.
8. **Spend intelligence on uncertainty.** Expensive reasoning belongs at architecture, ambiguity, prioritization, failure interpretation, and review boundaries.
9. **Reduce prompt tax.** Macro-goals collapse unnecessary human-agent round trips.
10. **Reduce vigilance tax.** Long-running delegation should notify the human at a real terminal execution state rather than requiring repeated status checks.
11. **Keep signaling separate from truth.** A notification is a wake-up interrupt, not evidence, acceptance, or integration.
12. **Separate goal identity from session identity.** One repository macro-goal may require multiple worker sessions and multiple candidate/review attempts.
13. **Reopen; do not renumber.** A director correction to the same semantic objective normally reuses the goal ID, branch/report lineage, and acceptance contract while starting a fresh worker session if the previous session terminated.
14. **Re-arm the return channel per attempt.** A correction session must not inherit stale terminal-notification state from a prior attempt.
15. **Preserve the principal veto.** No automation removes the human's authority to say: this is not what I want.

## Reading order

1. docs/00-manifesto.md
2. docs/01-ontology.md
3. docs/02-authority-and-roles.md
4. docs/03-repository-as-shared-mind.md
5. docs/04-transactional-development.md
6. docs/05-macro-goals.md
7. docs/06-evidence-and-verification.md
8. docs/07-escalation-and-review.md
9. docs/08-workflow.md
10. docs/09-adoption.md
11. docs/10-lineage.md
12. docs/11-completion-observability.md
13. docs/12-correction-continuations.md

Reusable repo templates live under templates/. Invocation prompts live under prompts/.

The pre-v1 stack-centric philosophy is preserved under archive/v0.5/.

## Version

Current doctrine: **1.2.0**.

v1.2 formalizes correction continuations: repository macro-goals are durable semantic units, while Codex/worker sessions are disposable execution containers that can be restarted under the same goal lineage after director review.
