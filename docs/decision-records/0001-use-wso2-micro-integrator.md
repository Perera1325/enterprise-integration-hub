# ADR 0001: Use WSO2 Micro Integrator for the Integration Layer

## Status
Accepted

## Context
The enterprise has a vast ecosystem of legacy SOAP systems, modern RESTful SaaS applications, and messaging brokers. Connecting these point-to-point results in a fragile "spaghetti" architecture. We need a centralized integration platform that is cloud-native, performs well under high throughput, and supports standard Enterprise Integration Patterns (EIP).

## Decision
We will use **WSO2 Micro Integrator (MI)** as the core integration engine.
- It provides out-of-the-box support for REST, SOAP, JMS, Kafka, and JDBC.
- Unlike WSO2 ESB (legacy), Micro Integrator is lightweight, starts up in seconds, and is optimized for containerized (Docker/Kubernetes) deployments.
- It follows the configuration-driven approach using Apache Synapse XML.

## Consequences
- **Positive**: Rapid development of integrations via Integration Studio. High scalability in Kubernetes. Seamless connection to legacy systems.
- **Negative**: Requires engineers to understand Apache Synapse XML syntax and WSO2 specific mediators. 

## Alternatives Considered
- *Apache Camel / Spring Boot*: More code-heavy. Requires Java development for every integration, whereas WSO2 provides configuration-based rapid development.
- *WSO2 API Manager*: APIM includes MI, but coupling API lifecycle management with deep mediation logic violates separation of concerns. We will use MI purely for integration.
