# ADR-002: Use synchronous REST for all service communication

## Status

Accepted

## Context

Team Flow Tracker consists of three services: a React Native mobile
app, a Spring Boot API, and a Python analytics service. A decision
is required on how these services communicate with each other.

The two primary options are synchronous communication via REST over
HTTPS, or asynchronous communication via a message broker such as
RabbitMQ or Kafka.

## Decision

All service-to-service communication will use synchronous REST over
HTTPS at this stage of the project. The mobile app calls the API
service. The analytics service calls the API service to read data
and returns computed results synchronously.

## Alternatives considered

**Asynchronous messaging via a message broker (RabbitMQ, Kafka)**
Asynchronous communication decouples services in time - a slow
analytics computation would not block the mobile app. This pattern
is appropriate when services need to operate independently or when
event history needs to be replayed. Rejected because it adds
significant infrastructure complexity (a broker to run, monitor,
and reason about) that is not justified at this project scale.
It also makes the system harder to demo and explain to a newcomer
in a single session.

**GraphQL**
GraphQL allows the mobile client to request exactly the fields it
needs, reducing over-fetching. Rejected because REST is sufficient
for the data shapes we need and is more familiar across the widest
range of engineering teams - which matters for a project used in
coaching contexts.

**gRPC**
gRPC offers strong typing via Protocol Buffers and efficient binary
serialisation. Rejected because the operational overhead and
tooling complexity are not justified here, and JSON over REST is
more readable for demonstration purposes.

## Consequences

**Easier:**
- Simple mental model: every service interaction is a standard
  HTTP request and response
- Easy to inspect with curl, Postman, or browser DevTools
- Familiar to the widest range of developers
- Straightforward to test with standard mocking tools

**Harder:**
- If the API service is slow or unavailable, the analytics service
  and mobile app are directly affected
- Long-running analytics computations (such as large Monte Carlo
  simulations) will block the caller until complete
- Revisiting this decision later and introducing async messaging
  would require significant rework

## Review trigger

Revisit this decision if Monte Carlo simulation requests exceed
five seconds of response time in practice.
