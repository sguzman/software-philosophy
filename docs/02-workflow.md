# Workflow

This is the end-to-end workflow I want every repo to follow.

## 0) Establish the contract

Every repo should have:

- README map
- docs describing rules the AI and humans follow
- a small set of quality gates (format/lint/validate/test)
- a release process (even if manual at first)

## 1) Start with intent

A change starts with a short "direction statement":

- what are we building?
- what does success look like?
- what must not change?
- what constraints exist (perf, compatibility, licensing, etc.)?

This can be written in an issue, a PR description, or a short note.

## 2) Configure first (when possible)

If the change is primarily "product behavior":
- add or update TOML config (properties)
- validate it
- only then implement the code that consumes it

## 3) Implementation loop (tight)

- make a small change
- run the relevant checks
- keep diffs reviewable

## 4) Quality gates (the minimum set)

A good default:

- formatting (taplo/biome/others)
- lint/static checks (when applicable)
- validation (schemas, config sanity)
- tests (unit/integration if present)
- docs link checks (lychee) on CI or periodically

## 5) Commit discipline

Commits should be written so tools can generate changelogs cleanly.
That means consistent structure and meaningful scope.

(Exact commit conventions belong in `docs/06-releases-changelogs.md`.)

## 6) Release discipline

Releases should be boring:

- changelog updated mechanically
- version bump is intentional
- tags match the version
- artifacts come from CI when possible

## 7) Docker deployment loop

- build image deterministically
- run minimal smoke checks
- treat compose as a reproducible "stack contract"
