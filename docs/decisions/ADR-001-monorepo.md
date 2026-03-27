# ADR-001: Use a monorepo for all services

## Status

Accepted

## Context

Team Flow Tracker consists of three distinct services: a React Native
mobile application, a Spring Boot API, and a Python analytics service.
A decision is required on whether these services should live in a single
repository (monorepo) or in separate repositories (polyrepo).

This project is maintained by a single engineer and serves as both a
working application and a reference for demonstrating software
engineering practices. Cross-service changes will be frequent during
early development. CI configuration, architectural documentation, and
decision records should be easy to find and maintain together.

## Decision

All three services will live in a single repository named
team-flow-tracker. The repository will be organized with a top-level
directory per service, plus a shared docs directory for architecture
and decisions.

## Alternatives considered

**Polyrepo (separate repository per service)**
Each service would have its own repository, its own CI pipeline, and
its own README. This is a common pattern in large organizations where
teams deploy independently and need strong ownership boundaries.
Rejected because the coordination overhead outweighs the autonomy
benefits for a single-engineer project, and it would scatter the
portfolio artifact across multiple URLs.

**Monorepo with a build tool (Nx, Turborepo, Gradle multi-project)**
Tools like Nx or Turborepo add dependency-aware build caching and
affected-project detection to monorepos. Rejected for now because
the added tooling complexity is not justified at this project scale.
This decision can be revisited if build times become a problem.

## Consequences

**Easier:**
- One place to find all code, documentation, and CI configuration
- Cross-service changes are a single commit and a single pull request
- Architecture decision records apply across all services naturally
- One repository URL to share as a portfolio piece

**Harder:**
- A single broken CI pipeline blocks all services
- Repository size will grow as all three services accumulate history
- Developers working only on one service must clone the whole repo
