# Repository State Closure

Modality: **HARD INVARIANT / PROHIBITION**

## Core rule

> **The repository is the canonical project state. Chat is only a temporal projection of that state while work is being performed.**

Any durable fact, decision, constraint, goal, architecture rule, current-state claim, prompt, dependency requirement, workflow rule, evidence reference, review result, or future-work obligation that another human or agent may need must exist in the repository before later work is allowed to depend on it.

The repository is not merely a convenient archive of important notes. It is the coordination substrate from which project reality must be reconstructible.

## Repository-state closure

A project satisfies **repository-state closure** when a capable authorized agent at a known repository commit can determine, without access to prior chat history:

- what the project is and what it is for;
- what doctrine and architecture are authoritative;
- what the principal currently wants that has been accepted into project state;
- what is known to be true now and with what evidence;
- what work has been completed, accepted, rejected, revised, blocked, or superseded;
- what work is authorized next;
- what constraints and non-goals govern that work;
- what prompts invoke the recurring workflows;
- how dependencies and local execution are materialized;
- what validation and evidence are required;
- what would require escalation;
- how another agent or human should continue the project correctly.

If any of those answers require reconstructing a conversation, asking the human to remember prior wording, consulting an agent's private scratchpad, or depending on undocumented local knowledge, the repository is not closed.

## Chat as temporal projection

Chat is useful for exploration, incomplete intent, argument, provisional hypotheses, clarification, live review discussion, discovering new doctrine or architecture, and deciding what should change next.

But chat is not project state merely because something was said there.

A conversation is a **temporal projection**: a temporary working view over the project while cognition is occurring.

The lifecycle is:

    canonical repository state R_n
      -> chat / agent reasoning / human discussion
      -> proposed delta
      -> durable repository mutation
      -> canonical repository state R_(n+1)

The conversation may generate the next state. It does not replace it.

## Promotion rule

When a chat-derived fact becomes relevant to future work, the director must promote it into the appropriate repository artifact before relying on it.

Examples:

- a new architectural rule -> architecture doctrine or project architecture;
- a product decision -> product scope / decision record;
- a new priority -> roadmap / priorities;
- a correction -> durable review contract;
- a recurring invocation -> prompt artifact;
- a discovered dependency -> dependency declaration/bootstrap;
- a test observation -> report/current-state evidence;
- a future possibility -> latent option;
- a new human preference that changes implementation -> project philosophy/profile/goal as appropriate.

Do not leave the operative version only in chat and proceed as though it were committed state.

## Hard prohibitions

Do not:

- require access to this conversation to continue the project correctly;
- rely on remembered chat decisions that are absent from the repository;
- make another agent ask the human what the previous agent already learned and should have externalized;
- keep architecture, acceptance criteria, correction instructions, prompt wording, or work state only in an agent UI;
- use model memory as a substitute for repository state;
- treat an uncommitted conversational decision as durable project authority across sessions;
- maintain a hidden second project state in notes, scratchpads, local-only files, or transient interfaces.

## External resources and secrets

Repository-state closure does **not** mean every byte required by the project must literally be committed to Git.

Some values and resources should remain external, especially secrets, credentials, large generated artifacts, external services, platform installations, or datasets that are naturally fetched/materialized.

The requirement is that the repository durably declares enough information to understand and materialize those dependencies safely.

For example:

    secret value                  -> external
    required secret name/purpose  -> repository

    compiler binary               -> external installation
    required version/bootstrap    -> repository

    large external dataset        -> external
    source/version/checksum/fetch contract -> repository

The repo must contain the **contract** even when it should not contain the payload.

## Conversation-loss test

Use this as a hard repository-health test:

> **If every chat transcript, model memory, agent scratchpad, and worker UI session disappeared right now, could a capable new director and worker continue correctly from the repository alone, except for intentionally external credentials and irreducible new human intent?**

If no, project state has leaked outside the repository.

Repair the repository before treating the workflow as durable.

## Multi-agent consequence

Repository-state closure is what makes heterogeneous coordination possible.

Humans and agents do not need shared conversational memory if they share the same canonical commit and repository contracts.

The repository therefore serves simultaneously as institutional memory, project constitution, current-state ledger, work queue, invocation protocol, evidence index, architecture record, and coordination bus.

This is why repository sovereignty is load-bearing rather than stylistic.
