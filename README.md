# Team Flow Tracker

A full-stack application for tracking team delivery flow, built to
demonstrate XP engineering practices, Lean metrics, TDD, CI/CD, and
modern software engineering principles across a mobile, API, and
analytics stack.

## What this project is

Team Flow Tracker helps engineering teams visualize and improve their
delivery flow. It surfaces cycle time, throughput, WIP aging, Monte
Carlo forecasts, and Value Stream health.

## Why this project exists

This project demonstrates end-to-end software engineering discipline
across a realistic, multi-layer stack. The full software delivery
lifecycle is simulated and documented - including architectural
decisions, test-driven development, CI/CD pipelines, and mobile
engineering practices.

## Tech stack

| Layer        | Technology              | Why                                                                 |
|--------------|-------------------------|---------------------------------------------------------------------|
| Mobile       | React Native (Expo)     | Cross-platform iOS and Android from a single codebase               |
| API          | Java / Spring Boot      | Industry-standard enterprise backend with strong TDD ecosystem      |
| Analytics    | Python / FastAPI        | Best-in-class data processing and Monte Carlo simulation            |
| Database     | PostgreSQL              | Relational model fits flow metrics data well                        |
| Feature flags| LaunchDarkly            | Progressive delivery and controlled feature rollout                 |
| CI/CD        | GitHub Actions + Docker | Fully observable pipeline, industry standard                        |

## Repository structure

This repository uses a monorepo layout. All three services live in one
repository to simplify CI configuration, shared documentation, and
architectural decision records for a project maintained by a small team.

See [ADR-001](docs/decisions/ADR-001-monorepo.md) for the full
decision record on this choice.

## Architecture

This project uses the C4 model to document architecture at four levels:
Context, Container, Component, and Code. Diagrams are written in
Mermaid and render directly in GitHub.

Architecture documentation lives in `docs/architecture/`.

## Architectural Decision Records

All significant technical decisions are documented in `docs/decisions/`.
Each ADR captures context, the decision, alternatives considered, and
consequences.

## SDLC

This project simulates a full software delivery lifecycle:

- Product inception and vision
- Architecture design with documented decisions
- TDD-first development across all layers
- CI/CD pipeline with quality gates
- Iterative delivery in small batches
- Flow metrics tracked on the project itself

## Project status

Currently in inception phase. Follow the commit history to see the
project evolve from first principles.
