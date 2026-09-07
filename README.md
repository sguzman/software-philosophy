# Software Philosophy v1.1

A repository-mediated operating system for agentic software development.

The core idea:

> The repository is the durable shared mind. The human supplies intent and taste. The director converts intent into doctrine, architecture, roadmaps, goals, and review. The implementation worker performs bounded transformations. Tests produce mechanical evidence. Git transports, records, and reverses state. A detached completion observer returns attention to the human only when delegated work reaches a terminal state.

This repository is not primarily about Rust, TOML, Docker, Codex, ChatGPT, PowerShell, or Windows notifications. Those are contingent tools. The doctrine is about how to organize authority, knowledge, work, evidence, communication, and human attention when software is built by a human principal plus multiple AI agents with different capabilities.

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
    REPOSITORY
      canonical shared context
      current state / work queue / reports / reviews
            |
            v
    IMPLEMENTATION WORKER
      inspect / edit / compile / test / diagnose / repair
      arm completion observer
            |
            v
    CANDIDATE BRANCH + REPORT + EVIDENCE
            |
            +----> TERMINAL REPO STATE: done | blocked
                         |
                         v
                COMPLETION OBSERVER
                  best-effort return signal
                         |
                         v
                    HUMAN ATTENTION
            |
            v
    DIRECTOR REVIEW
      accept / reject / revise / integrate

The human is deliberately neither the courier between agents nor the polling loop around them.

## v1.1 doctrine

1. **Persist cognition that matters.** Important project knowledge belongs in the repository, not only in chat.
2. **Separate authority from execution.** The agent best suited to architecture should not spend its attention babysitting file edits; the filesystem-capable worker should not invent the project.
3. **Delegate bounded autonomy.** A worker gets enough latitude to finish a coherent goal, including directly related repair loops, but not enough authority to silently redefine architecture.
4. **Make prompts thin.** A prompt should usually point at a committed goal, not restate the project.
5. **Treat implementation as a transaction.** There is a known base state, an authorized transformation, a candidate result, evidence, and an explicit integration decision.
6. **Type the evidence.** Compile success, deterministic tests, hosted runtime probes, real-device behavior, and human judgment are different evidence classes.
7. **Prefer truthful incompleteness over fake certainty.** Current-state docs distinguish verified, inferred, historical, blocked, and unverified claims.
8. **Spend intelligence on uncertainty.** Expensive reasoning belongs at architecture, ambiguity, prioritization, failure interpretation, and review boundaries.
9. **Reduce prompt tax.** Macro-goals collapse unnecessary human-agent round trips.
10. **Reduce vigilance tax.** Long-running delegation should notify the human at a real terminal state rather than requiring repeated status checks.
11. **Keep signaling separate from truth.** A desktop notification is a wake-up interrupt, not evidence, acceptance, or integration.
12. **Preserve the principal veto.** No automation removes the human's authority to say: this is not what I want.

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

Reusable repo templates live under templates/. Invocation prompts live under prompts/.

The pre-v1 stack-centric philosophy is preserved under archive/v0.5/.

## Version

Current doctrine: **1.1.0**.

v1.1 adds completion observability: the worker owns automatically arming a detached return channel for long-running goals, while the repository remains the authoritative source of terminal state.
