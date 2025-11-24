# DS Microservices (Spring Cloud) — Overview

This repository contains three Spring Boot microservices that illustrate a small
Spring Cloud microservices architecture. Below is a short description of the
typical technical roles found in such an architecture and an example tool for
each role.

1) API Gateway
- Purpose: Single entry point for clients; routes requests to backend
  microservices, performs cross-cutting concerns such as authentication,
  rate limiting, request routing and load balancing.
- Example tool: Spring Cloud Gateway or Netflix Zuul.

2) Service (Stateless Business Microservice)
- Purpose: Implements domain logic, exposes a REST API, is independently
  deployable and scales horizontally. Services are usually stateless and may
  persist state in external databases.
- Example tool: Spring Boot + Spring Web / Spring Data (e.g., a `client-service`).

3) Data/Stateful or Backend Service
- Purpose: Responsible for durable storage and data access patterns. In
  microservices you often separate the bounded-context service from its data
  store; sometimes specialized services (e.g., account-service) encapsulate
  data access and business rules.
- Example tool: Spring Boot talking to PostgreSQL, MongoDB, or a managed
  database; use Spring Data for repository abstractions.

Cross-cutting components (examples)
- Service discovery: Eureka (Spring Cloud Netflix) or static DNS/sidecars.
- Configuration: Spring Cloud Config / HashiCorp Consul for centralized
  configuration management.
- Circuit breaker / Resilience: Resilience4j or Hystrix (legacy).
- Observability: Micrometer + Prometheus for metrics; Zipkin / Sleuth for tracing;
  centralized logging with ELK (Elasticsearch, Logstash, Kibana) or Loki.

How this repo maps to roles
- `ds-api-gateway` : API Gateway implementation (routing + cross-cutting).
- `ds-client-service` : Example stateless business microservice exposing client APIs.
- `ds-account-service` : Example service managing accounts and persistent data.

Running locally (quick)
- Build a service: `./mvnw -f ds-client-service package` (or run the appropriately
  named module). Each service produces a jar under `target/`.
- Docker: Each service has a `Dockerfile` — CI builds images and pushes them to
  Docker Hub in the provided workflow.

Notes
- The goal of this README is to document the technical roles for the three
  services in the project and provide references to common production tools.
