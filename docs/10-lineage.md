# Lineage: From Tooling Preferences to Repository-Mediated Agency

The v1 doctrine emerged from real development friction rather than from a hypothetical multi-agent framework.

## Legacy v0.5 — stack-centric direction

The early philosophy emphasized Rust, TOML as a declarative product surface, Docker, quality gates, release automation, and AI as an editor/operator.

That material remains useful and is preserved under archive/v0.5/.

Its limitation is that it mainly answers what tools a repository should use and how changes should be made reliably. It does not fully answer authority, durable multi-agent cognition, human-courier removal, or bounded execution autonomy.

## Caliberate — transactional agent development

Caliberate introduced repository documentation as the system of record, AGENTS as an entry point, explicit architect/worker roles, bounded work items, branch/report handoff, architecture escalation, and direct GitHub review/integration.

The key conceptual shift was:

> The implementation worker can write code without being allowed to invent the project.

This moved project intelligence from prompt repetition into repository doctrine.

## Caliberate's remaining friction

The work-item model was still too conversationally granular.

Even when architecture was sound, many implementation passes required another prompt and another human relay.

The system reduced coding burden but still imposed coordination burden.

## Lantern Leaf — macro-goals and removal of the human courier

Lantern Leaf pushed the model further.

Its repository explicitly makes ChatGPT director, architect, and integrator; Codex the implementation worker; and the human maintainer the local operator rather than the normal courier.

Work lives in durable states. The worker continues through multiple authorized passes until acceptance or a true architectural blocker. The director reviews pushed branches directly.

The important invention is the **macro-goal**.

Instead of:

    prompt -> edit -> failure -> prompt -> repair -> prompt -> test -> prompt

the structure becomes:

    director-owned goal
      -> worker diagnosis
      -> implementation
      -> repair
      -> retest
      -> additional authorized subtrack
      -> final report
      -> director review

One human invocation can produce a much larger coherent unit of progress.

## Lantern Leaf — completion observability

The next friction appeared after macro-goals became large enough to run unattended: the human no longer had to keep pushing the worker forward, but still had to remember to check whether the worker had finished.

Lantern Leaf answered by making detached terminal goal notifications part of the repository workflow.

Codex became responsible for automatically launching a repository-owned Windows watcher. The watcher observes the macro-goal reaching `done` or `blocked`, emits one desktop notification, and exits. The human does not run a second command.

This exposed a second coordination cost:

- **prompt tax**: paying attention to keep work moving;
- **vigilance tax**: paying attention to discover that work stopped.

The watcher also forced an important epistemic distinction: notification is a return signal, not evidence or acceptance.

## v1.0 synthesis

The first general theory extracted from Caliberate and early Lantern Leaf was:

1. The repo is shared institutional memory.
2. The human is principal, not courier.
3. The director owns semantics.
4. The worker owns bounded mutation.
5. Goals delegate authority.
6. Macro-goals minimize prompt tax.
7. Evidence is typed.
8. Git is state identity, transport, and rollback.
9. Reports carry execution claims.
10. Reviews convert candidate state into accepted state.
11. Escalation contains unresolved architecture.
12. Human taste remains sovereign.

## v1.1 refinement

v1.1 adds:

13. Long-running delegation has a return channel.
14. The worker owns arming repository completion observation.
15. Terminal `done`/`blocked` state is distinct from director acceptance.
16. Completion signals route human attention but do not establish truth.
17. Agentic systems should minimize both prompt tax and vigilance tax.

Caliberate demonstrated that bounded agent work can be governed through repository contracts.

Lantern Leaf demonstrated first that contracts can be made large enough to remove conversational babysitting, and then that terminal observation can remove the need to watch those long-running goals.

## Lantern Leaf — correction continuations

Goal 0006 exposed the next lifecycle bug.

The first Codex Goal session terminalized and claimed DONE. Director review then found bounded evidence and behavior gaps. The repository goal was still semantically Goal 0006, but the Codex UI required a fresh Goal session to continue.

This exposed another category distinction:

- repository macro-goal = durable semantic work identity;
- Codex Goal session = disposable execution container;
- execution attempt = one review-bounded pass of a session against the goal.

The correct continuation was therefore:

    Goal 0006 / Session A -> DONE claim -> director REVISE
    Goal 0006 / Session B -> correction attempt -> review again

not:

    Goal 0006 -> rejected -> Goal 0007

The same event also exposed stale completion-sentinel risk when a goal ID is reused for a later attempt, requiring the notification channel to become attempt-aware/re-armable.

## v1.2 refinement

v1.2 adds:

18. Repository macro-goal identity is distinct from worker-session identity.
19. One macro-goal may span multiple execution attempts and director reviews.
20. Correctable review reopens the same goal instead of renumbering it.
21. A fresh worker session is normal when a prior session has terminalized.
22. Goal branch/report lineage is preserved by default across correction attempts.
23. Completion observers are exactly-once per attempt and must be safely re-armed for later attempts under the same goal ID.

v1.2 turns the Goal 0006 failure into a general rule: **tool lifecycle must not dictate project ontology.**


## Lantern Leaf — the QA payload failure

After automated non-PDF parity was accepted, Lantern Leaf briefly moved human desktop verification into a precompiled GitHub Actions QA bundle.

Mechanically, the bundle was attractive: it could include an executable, Pandoc, fixtures, a one-command launcher, and logs without requiring the principal's machine to have a build environment.

Operationally, it violated the deeper repository model.

The principal would have had to download a large generated archive, depend on network quality for the handoff, extract it into a second execution location, trust/run material assembled outside the checkout, and keep track of the relationship between that payload and repository state.

The automation had reduced machine setup by increasing human ceremony.

The corrected model became:

    repo is workspace
      -> repo declares dependencies
      -> repo materializes dependencies
      -> repo builds itself
      -> repo launches QA
      -> repo keeps logs

Lantern Leaf first implemented this with a custom Windows dependency declaration/bootstrap and then refined the policy to use Scoop's own dependency representation for ordinary CLI tools.

Current concrete shape:

    Scoopfile.json
    rust-toolchain.toml
    deps.ps1
    qa.ps1

This exposed another coordination cost: **ceremony tax** — mechanical setup, transfer, extraction, environment reconstruction, or provenance bookkeeping imposed on the human that repository machinery could own.

## v1.3 refinement

v1.3 adds:

24. Doctrine has explicit modalities: prohibitions, current conventions, and latent options.
25. External payload handoff is prohibited for the principal's ordinary development/manual-QA workflow.
26. The repository is the human execution surface as well as the agent communication substrate.
27. Dependency requirements are durable repository state and should be machine-readable where practical.
28. Repo-owned bootstrap/check machinery materializes the local environment and should be idempotent.
29. The director owns telling the human when dependency refresh is required; the human should not infer hidden environment drift.
30. Scoop is the current Windows policy for ordinary CLI dependencies.
31. Language-native toolchain declarations and unavoidable platform-native installer exceptions remain valid when they are the natural owner of that dependency class.
32. Latent options preserve future technologies such as Nix or mise without creating roadmap pressure or authorization.

v1.3 turns the QA bundle mistake into a general rule: **automation must not reduce agent friction by exporting ceremony to the principal.**
