# Docker for Deployment

Docker is not just deployment. It's a reproducibility boundary.

## Why Docker fits this philosophy

- builds are explicit (Dockerfile)
- runtime dependencies are captured
- environments are reproducible across machines
- CI can build exactly what production runs

## The contract

- images should be buildable from a clean checkout
- configuration should be injected (env vars, mounted config, secrets)
- containers should log clearly
- health checks should exist for services

## Compose as a stack contract

For multi-service systems:

- compose is documentation that runs
- networks and dependencies are explicit
- the stack becomes testable as a unit

## Minimal expectations

- deterministic base images (pin when reasonable)
- clear exposed ports
- volumes explicit
- one obvious entrypoint
