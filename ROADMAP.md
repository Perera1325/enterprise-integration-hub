# Project Roadmap

This roadmap defines the strategic direction of the **Enterprise Integration Hub**.

## Phase 1: Foundation (Current)
- [x] Repository structure definition.
- [x] Base documentation scaffolding.
- [ ] Global fault sequences and JSON logging mediators.
- [ ] Docker containerization strategy.
- [ ] GitHub Actions CI/CD implementation.

## Phase 2: Core Integrations
- [ ] Implementation of REST-to-SOAP mediation proxy.
- [ ] Implementation of API Aggregation (Scatter-Gather EIP).
- [ ] Integration with a mock PostgreSQL database via DSS (Data Services Server features of MI).

## Phase 3: Security & Observability
- [ ] OpenTelemetry integration for distributed tracing.
- [ ] OAuth2 token validation (JWT signature verification).
- [ ] Prometheus metrics exposure and Grafana dashboard generation.

## Phase 4: Event-Driven Architecture
- [ ] Implementation of AMQP/Kafka inbound endpoints.
- [ ] Asynchronous messaging (Store and Forward pattern).
- [ ] Dead Letter Queue (DLQ) implementation.
