# ADR 0002: Structured JSON Logging

## Status
Accepted

## Context
In a distributed microservices environment spanning multiple Kubernetes pods, traditional unstructured text logs are difficult to parse, query, and alert upon. We need a way to easily trace transactions across boundaries.

## Decision
All logs emitted by WSO2 Micro Integrator will be formatted as **Structured JSON**.
- We will configure the `log4j2.properties` to use a JSON layout.
- We will inject a `Correlation-ID` into every incoming request and propagate it to all backend calls.

## Consequences
- **Positive**: Log aggregators (Elasticsearch, Splunk, Datadog) can instantly parse and index log fields. Enables powerful dashboards and accurate tracing.
- **Negative**: JSON logs are slightly less human-readable in a raw terminal without tools like `jq`.

## Implementation Details
The global WSO2 `LogMediator` configurations will be set to output predefined keys (e.g., `transactionId`, `apiName`, `latency`, `errorCode`).
