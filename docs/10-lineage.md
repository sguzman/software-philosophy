# Lineage: From Tooling Preferences to Repository-Mediated Agency

v1.0 emerged from real development friction rather than from a hypothetical multi-agent framework.

## Legacy v0.5 — stack-centric direction

The early philosophy emphasized Rust, TOML as a declarative product surface, Docker, quality gates, release automation, and AI as an editor/operator.

That material remains useful and is preserved under archive/v0.5/.

Its limitation is that it mainly answers:
- what tools should a repository use?
- how should changes be made reliably?

It does not fully answer:
- who has authority in a multi-agent system?
- where project cognition should live?
- how two agents should communicate without a human courier?
- how to distinguish execution autonomy from architectural autonomy?

## Caliberate — transactional agent development

Caliberate introduced the stronger pattern:
- repository documentation as the system of record;
- AGENTS as an entry point rather than a giant project brain;
- explicit architect versus implementation-worker roles;
- bounded work items;
- branch and report handoff;
- architecture escalation instead of improvisation;
- direct GitHub review and integration.

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

## v1.0 synthesis

The general theory extracted from that evolution is:

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

Caliberate demonstrated that bounded agent work can be governed through repository contracts.

Lantern Leaf demonstrated that the contracts can be made large enough to remove most conversational babysitting.

v1.0 turns those project-specific practices into a reusable ontology.
