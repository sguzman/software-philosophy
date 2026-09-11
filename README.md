# Software Philosophy v1.7

A repository-mediated operating system for agentic software development.

The core idea:

> The repository is the canonical project state and durable shared mind. Chat is a temporal projection used to inspect, discuss, and transform that state; it is never a required store of project reality. The human is the semantic control plane: intent, taste, veto, embodied observation, and exceptional authorization. The repository and agents carry state, context, transport, execution, retries, evidence, monitoring, and bookkeeping. Human cognition is the scarce, serial, context-switch-sensitive resource, so the system should minimize avoidable human cognitive load while preserving human semantic control. The director converts intent into doctrine, architecture, roadmaps, goals, review, and reusable prompt artifacts. The implementation worker performs bounded transformations. Tests produce mechanical evidence. Git transports, records, and reverses state. Completion observers return attention at terminal execution states. Repository macro-goals persist across disposable worker sessions until the director accepts, abandons, or supersedes them. Human-facing development stays repo-native: the repository declares and materializes its environment, exposes stable local entrypoints, and does not outsource routine testing, canonical prompts, required project context, or machine-shaped coordination work to the principal.

The repository has three related but distinct substantive layers plus a repository-native invocation layer:

1. **Development governance doctrine** — how the human, director, worker, repository, evidence, and work lifecycle relate.
2. **Software architecture doctrine** — how the software itself should be structured: runtime responsibilities, concurrency, state, boundaries, responsiveness, and other empirically earned architectural rules.
3. **Principal implementation profiles** — strong current defaults such as Rust-first and Windows/Scoop policy.
4. **Prompt artifacts** — durable, versioned invocation contracts under `prompts/` that point agents into the richer repository state.

The core governance doctrine is not tied to a particular programming language. The principal profiles are intentionally not language-neutral: in practice, product implementation is Rust by default.

## Operating topology

    HUMAN PRINCIPAL
      SEMANTIC CONTROL PLANE
      intent / taste / veto
      embodied observation / exceptional authority
            |
            v
    CHAT / AGENT SESSION
      temporal projection / reasoning
      proposed state delta
            |
            v
    DIRECTOR / ARCHITECT / INTEGRATOR
      philosophy / product scope / architecture
      priorities / roadmaps / macro-goals
      semantic review / integration
      canonical prompt artifacts
            |
            v
    REPOSITORY + AGENTS
      CANONICAL STATE + COORDINATION PLANE
      context / transport / execution / retries
      evidence / monitoring / bookkeeping
            |
            v
    PROMPT INVOCATION
      thin transient delivery into worker UI
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

The human is deliberately neither the courier between agents nor the polling loop around them. The human is also not the canonical storage medium for project state or prompt wording. Human attention is reserved for work that genuinely requires human authorship, judgment, embodiment, or authority.

## v1.7 doctrine

1. **Persist cognition that matters.** Important project knowledge belongs in the repository, not only in chat.
2. **Separate authority from execution.** The agent best suited to architecture should not spend its attention babysitting file edits; the filesystem-capable worker should not invent the project.
3. **Delegate bounded autonomy.** A worker gets enough latitude to finish a coherent goal, including directly related repair loops, but not enough authority to silently redefine architecture.
4. **Make prompts repository-native and thin.** Reusable operational prompts are first-class versioned repository artifacts. Their content should point at committed goals/reviews/doctrine rather than restating the project.
5. **Separate prompt artifact from prompt invocation.** The file in Git is canonical; pasting/sending it into ChatGPT, Codex, a CLI, or another UI is a transient delivery event.
6. **Never make chat the only canonical prompt store.** If an invocation is expected to recur across sessions, agents, or time, commit it under `prompts/` or a documented project-equivalent path.
7. **Treat implementation as a transaction.** There is a known accepted state, an authorized transformation, candidate attempts, evidence, review, and an explicit integration decision.
8. **Type the evidence.** Compile success, deterministic tests, hosted runtime probes, real-device behavior, and human judgment are different evidence classes.
9. **Prefer truthful incompleteness over fake certainty.** Current-state docs distinguish verified, inferred, historical, blocked, and unverified claims.
10. **Spend intelligence on uncertainty.** Expensive reasoning belongs at architecture, ambiguity, prioritization, failure interpretation, and review boundaries.
11. **Reduce prompt tax.** Macro-goals collapse unnecessary human-agent round trips.
12. **Reduce vigilance tax.** Long-running delegation should notify the human at a real terminal execution state rather than requiring repeated status checks.
13. **Keep signaling separate from truth.** A notification is a wake-up interrupt, not evidence, acceptance, or integration.
14. **Separate goal identity from session identity.** One repository macro-goal may require multiple worker sessions and multiple candidate/review attempts.
15. **Reopen; do not renumber.** A director correction to the same semantic objective normally reuses the goal ID, branch/report lineage, and acceptance contract while starting a fresh worker session if the previous session terminated.
16. **Re-arm the return channel per attempt.** A correction session must not inherit stale terminal-notification state from a prior attempt.
17. **Preserve the principal veto.** No automation removes the human's authority to say: this is not what I want.
18. **Give doctrine explicit force.** Distinguish hard prohibitions, current positive conventions, and latent future options instead of mixing them into one undifferentiated wish list.
19. **Keep human execution repo-native.** The principal should test from the checked-out repository through repository-owned entrypoints, not through ad hoc downloaded execution payloads.
20. **Reject external payload handoff for development/QA.** Do not ask the principal to download, unpack, trust, and run a generated CI bundle or other side-channel payload to test current project state.
21. **Materialize dependencies from repo declarations.** The repository declares the tools it needs and owns idempotent bootstrap/check machinery.
22. **Use Scoop as the current Windows CLI dependency policy.** Ordinary Windows command-line dependencies are declared through Scoop/Scoopfile where appropriate; language toolchains and unavoidable platform-native workloads may retain their native managers.
23. **Preserve future options without scheduling them.** Nix, mise, or other environment systems may be recorded as latent options without creating roadmap priority, work authorization, or dissatisfaction with the current Scoop policy.
24. **Separate development governance from software architecture.** Agent workflow rules and runtime/software-structure rules are related but should live in distinct doctrine layers.
25. **Protect latency-critical interactive threads.** GUI/UI threads may orchestrate lightweight interaction but must not perform heavy, blocking, unbounded, or externally paced work.
26. **Move labor behind an execution boundary.** Expensive UI-triggered work should normally cross a typed work-queue/worker boundary and return results asynchronously.
27. **Do not mistake `async` for background execution.** CPU-heavy work still blocks if it is polled on the interactive thread.
28. **Use Rust first.** Product implementation defaults to Rust; non-Rust product runtimes require a concrete justification, while configuration/shell/package-manager/platform glue remain normal exceptions.
29. **Enforce repository-state closure.** Everything required to understand, continue, execute, review, or coordinate durable project work must exist in the repository or be explicitly declared there as an external prerequisite.
30. **Treat chat as a temporal projection, not project state.** Conversations may explore or propose the next state, but project reality is the committed repository state.
31. **Externalize before dependency.** Once a chat-derived fact or decision matters to later work, commit it to the appropriate repository artifact before another human or agent is expected to rely on it.
32. **Budget human cognition.** Treat human attention and working memory as the scarce, serial, context-switch-sensitive resource in the system.
33. **Use the human as control plane, not data plane.** Human attention belongs on intent, taste, veto, embodied observation, and true authority boundaries; repository and agents carry context, state, transport, retries, monitoring, and bookkeeping.
34. **Do not export machine-shaped work to the principal.** If an agent or deterministic repository mechanism can own a task without human judgment, keep it out of the human layer.
35. **Escalate decision-ready.** When human input is genuinely required, present the smallest sufficient decision or observation with relevant evidence and tradeoffs already prepared, then externalize the answer into repository state.

## Reading tracks

### Development governance doctrine

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
14. docs/13-doctrinal-modalities.md
15. docs/14-repo-native-human-interface.md
16. docs/15-dependency-materialization.md
17. docs/16-latent-options.md
18. docs/17-prompts-as-repository-artifacts.md
19. docs/18-repository-state-closure.md
20. docs/19-human-attention-budget.md

### Software architecture doctrine

1. architecture/README.md
2. architecture/principles/0001-interactive-thread-isolation.md
3. architecture/patterns/work-queue-boundary.md

### Principal implementation profiles

1. profiles/README.md
2. profiles/rust-first.md

### Prompt artifacts

1. prompts/README.md
2. prompts/execute-ready-goal.md
3. prompts/continue-corrected-goal.md
4. prompts/review-pushed-goal.md
5. prompts/request-human-verification.md

Reusable repo templates live under templates/. Invocation prompt artifacts live under `prompts/`.

The pre-v1 stack-centric philosophy is preserved under archive/v0.5/.

## Version

Current doctrine: **1.7.0**.

v1.7 makes human cognitive load an explicit system constraint and optimization target: the principal is the semantic control plane, the repository and agents absorb machine-shaped coordination work, and human interruptions should be decision-ready and irreducible.
