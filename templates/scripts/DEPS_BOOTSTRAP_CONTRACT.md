# Dependency Bootstrap Contract

A repo-owned dependency bootstrap should:

- read committed dependency declarations;
- be idempotent or safely rerunnable;
- support a check-only mode when useful;
- install/materialize only the declared environment;
- emit actionable missing-dependency diagnostics;
- use the current platform policy;
- preserve explicit exceptions rather than hiding manual prerequisites;
- work from the repository root without external payload handoff.

On the principal's current Windows profile, ordinary CLI tools should flow through Scoop/Scoopfile.
