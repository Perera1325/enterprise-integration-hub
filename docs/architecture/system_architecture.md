# System Architecture

The Enterprise Integration Hub acts as the centralized mediation layer for the entire organization.

## Architecture Diagram

```mermaid
graph TD
    Client[Consumers / Web / Mobile] --> |HTTPS/REST| Gateway[API Gateway / Load Balancer]
    Gateway --> |OAuth2 / JWT| MI[WSO2 Micro Integrator Layer]
    
    subgraph WSO2 Micro Integrator
        Proxy[Proxy Services]
        API[REST APIs]
        Inbound[Inbound Endpoints]
        Seq[Mediation Sequences]
        Proxy --> Seq
        API --> Seq
        Inbound --> Seq
    end
    
    Seq --> |SOAP 1.1/1.2| LegacyBackend[Legacy Mainframe / SOAP Services]
    Seq --> |REST/JSON| ModernSaaS[Modern SaaS Endpoints]
    Seq --> |JDBC| DB[(Enterprise Database)]
    Seq --> |AMQP/Kafka| EventBus[Enterprise Event Bus]
```

## Layers Explained
1. **Presentation Layer (Consumers)**: Clients connecting over standard protocols (HTTP/REST).
2. **Gateway / Security**: Handles API Lifecycle, throttling, and initial token verification. 
3. **Integration Layer (WSO2 MI)**:
   - **Proxy Services**: Used for SOAP-to-REST or routing.
   - **REST APIs**: Native RESTful endpoint definitions.
   - **Sequences**: The core business logic of integration (transformation, filtering, cloning).
4. **Backend Services**: The diverse ecosystem of the enterprise.
