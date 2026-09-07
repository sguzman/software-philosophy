# Software Philosophy Agent Guide

This repository defines a philosophy and protocol for agentic software development. The documentation is the product.

## Authority

The human principal owns intent, taste, and final veto.

ChatGPT in the director role owns:
- the philosophy and ontology;
- document structure and canonical terminology;
- version boundaries;
- acceptance or rejection of proposed doctrinal changes;
- integration of accepted doctrine.

Implementation agents may:
- improve examples and templates when explicitly tasked;
- check links, formatting, consistency, and internal references;
- propose bounded corrections.

Implementation agents may not silently:
- redefine role authority;
- weaken the principal veto;
- collapse evidence classes;
- replace repository-mediated coordination with chat-only state;
- grant implementation workers open-ended architectural authority;
- rewrite the v0.5 archive.

## Canonical reading order

Read README.md and docs/00-manifesto.md through docs/10-lineage.md before making doctrinal changes.

## Archive rule

archive/v0.5/ is immutable historical material. Correct errors in current doctrine instead of rewriting the archive.

## Change rule

A doctrinal change should state:
- what concept changes;
- why the old concept is insufficient;
- what downstream templates or workflows must change;
- whether the change is compatible with v1.0.

Major changes to the authority model, repository ontology, or transaction protocol require a new major doctrine version.
