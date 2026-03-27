# C4 Level 2: Container Diagram

This diagram opens the Team Flow Tracker system and shows the
deployable services, their technologies, and how they communicate.
No internal component detail is shown at this level.

## Diagram
```mermaid
C4Container
    title Container Diagram - Team Flow Tracker

    Person(coach, "Engineering Coach", "Primary user of the system")

    System_Boundary(tft, "Team Flow Tracker") {
        Container(mobile, "Mobile App", "React Native / Expo", "Cross-platform iOS and Android app. Primary interface for capturing stories and viewing flow metrics.")
        Container(api, "API Service", "Java / Spring Boot", "Handles all business logic, domain rules, and data persistence. Exposes REST endpoints consumed by the mobile app and the analytics service.")
        Container(analytics, "Analytics Service", "Python / FastAPI", "Computes flow metrics, runs Monte Carlo simulations, and produces Value Stream data. Reads from the API service via REST.")
        ContainerDb(db, "Database", "PostgreSQL", "Stores stories, flow entries, team records, and survey responses. Owned exclusively by the API service.")
    }

    System_Ext(ld, "LaunchDarkly", "Feature flag management")

    Rel(coach, mobile, "Uses", "iOS / Android")
    Rel(mobile, api, "Reads and writes flow data", "REST / HTTPS")
    Rel(mobile, ld, "Reads feature flag state", "LaunchDarkly SDK")
    Rel(api, db, "Reads and writes", "JDBC")
    Rel(analytics, api, "Reads story and flow data", "REST / HTTPS")
    Rel(api, ld, "Reads feature flag state", "LaunchDarkly Java SDK")
```

## Key decisions reflected here

- The API service is the only service that talks to the database.
  The analytics service reads data through the API, not directly
  from PostgreSQL. This keeps the database schema a private
  implementation detail of the API service.

- Both the mobile app and the API service integrate LaunchDarkly
  independently. The mobile app uses the React Native SDK to
  control UI-level feature rollout. The API uses the Java SDK
  to control server-side behaviour. This mirrors the pattern
  used in production mobile coaching engagements.

- All service-to-service communication is synchronous REST at
  this stage. See ADR-002 for the rationale.

## Next level

See [component.md](component.md) for the C4 Level 3 view showing
the internal structure of each service.
