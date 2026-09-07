# Correction-continuation worker invocation

Preferred prompt after the director has reopened a previously terminalized repository goal:

> This is a director correction continuation of repository Goal <ID>, not a new macro-goal. Read `AGENTS.md`, the reopened goal under `docs/work/ready/`, and `docs/work/reviews/<ID>.md`. The prior worker session has terminated, so this is a fresh worker session continuing the same durable goal lineage. Continue the existing goal branch/report lineage unless the review explicitly says otherwise, synchronize current director-owned correction/governance state from main before editing, re-arm completion observation for this new attempt so stale prior terminal state cannot retrigger, and execute all correction items until the acceptance gates pass or an escalation condition is reached.

The repository contains the actual correction contract. The prompt only establishes the identity/lifecycle relationship.

Do not allocate the next repository goal number merely because this is a new worker/Codex Goal session.
