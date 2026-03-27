# C4 Level 1: System Context

This diagram shows Team Flow Tracker as a black box, its primary user,
and the external systems it depends on. No technology or implementation
detail is shown at this level.

## Diagram
```mermaid
C4Context
    title System Context - Team Flow Tracker

    Person(coach, "Engineering Coach", "Uses the app to track and
    visualize team delivery flow during coaching engagements")

    System(tft, "Team Flow Tracker", "Enables coaches and teams to
    capture flow data and surface delivery metrics including cycle
    time, throughput, and forecasts")

    System_Ext(ld, "LaunchDarkly", "Feature flag management and
    progressive delivery control")

    System_Ext(gh, "GitHub", "Source control and CI/CD pipeline
    execution via GitHub Actions")

    Rel(coach, tft, "Captures stories, views metrics, runs forecasts")
    Rel(tft, ld, "Reads feature flag state to control rollout")
    Rel(tft, gh, "Source hosted and built here")
```

## Key decisions reflected here

- The primary user is an engineering coach, not an end-user consumer.
  This shapes the UX -- the app assumes technical literacy.
- LaunchDarkly is an external dependency, not something we build.
  This is an explicit architectural choice documented in ADR-001.
- GitHub is both infrastructure and documentation host. The CI/CD
  pipeline and the architecture diagrams live in the same place as
  the code.

## Next level

See [container.md](container.md) for the C4 Level 2 view showing
the deployable services inside Team Flow Tracker.
