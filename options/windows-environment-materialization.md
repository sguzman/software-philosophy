# Windows Environment Materialization — Future Options

Status: **LATENT**

## Current convention

Use Scoop for ordinary Windows CLI dependencies.

Use conventional language-toolchain declarations where appropriate, such as `rust-toolchain.toml` + rustup.

Use narrowly documented Windows-native installer/bootstrap exceptions for compiler/workload components Scoop should not own.

## Latent candidates

- **mise**
- **Nix**

## Why preserve these options

They may become attractive if:
- multi-language tool/version management grows substantially;
- Windows/Linux environment parity becomes costly;
- stronger environment reproducibility becomes valuable;
- per-repo bootstrap scripts become too complex;
- the principal wants a richer declarative environment layer.

## Non-authorization

This file does **not** authorize:
- migrating away from Scoop;
- adding Nix/mise files now;
- putting migration on the roadmap;
- assigning a Codex goal;
- treating current Scoop usage as temporary or deficient.

Promote only when an actual future constraint makes evaluation worthwhile.
