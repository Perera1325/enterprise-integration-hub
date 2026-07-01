# Enterprise Integration Hub

<div align="center">
  <h3>Centralized, Production-Grade Integration Platform</h3>
  <p>Powered by WSO2 Micro Integrator</p>
</div>

---

## 📖 Project Description

**Enterprise Integration Hub** is a cloud-native, centralized integration layer designed to simulate how a large-scale global enterprise connects its diverse backend ecosystems (legacy SOAP, modern SaaS REST APIs, Databases, and Event Brokers) through a unified mediation layer.

This repository serves as a flagship demonstration of **Enterprise Integration Patterns (EIP)**, production engineering, and DevSecOps best practices using **WSO2 Micro Integrator**. 

## 🏗 Architecture Overview

The integration layer sits between consumers (web, mobile, B2B partners) and backend services. It is responsible for message transformation, protocol switching, service orchestration, security enforcement, and rate-limiting.

![System Architecture Placeholder](docs/architecture/system_architecture.png)

## 🛠 Technology Stack

- **Integration Engine**: WSO2 Micro Integrator 4.2.0+
- **Languages**: XML (Synapse), JSON, DataMapper
- **Infrastructure**: Docker, Kubernetes, Docker Compose
- **Persistence**: PostgreSQL
- **CI/CD**: GitHub Actions
- **Observability**: Prometheus, Grafana, OpenTelemetry (Future)
- **Security**: OAuth2 / JWT (via WSO2 Asgardeo / API Manager)

## 📁 Repository Structure

```text
enterprise-integration-hub/
├── .github/workflows/    # CI/CD pipelines
├── docs/                 # Architecture, ADRs, and deployment docs
├── integration/          # WSO2 artifacts (APIs, Proxy Services, Sequences, Tasks)
├── configs/              # Environment-specific properties (dev, test, prod)
├── docker/               # Dockerfiles and docker-compose
├── kubernetes/           # Helm charts and K8s manifests
└── tests/                # Integration and API tests
```

## 🚀 Prerequisites

To run this project locally, you will need:
- [Docker](https://docs.docker.com/get-docker/) & Docker Compose
- [WSO2 Integration Studio](https://wso2.com/integration/integration-studio/) (for active development)
- Java 11+
- Maven 3.6+

## ⚙️ Installation & Running Locally

### Docker Setup
This project provides a production-like local environment using `docker-compose`.

```bash
cd docker
docker-compose up -d
```
*(See `docs/deployment/docker.md` for detailed instructions)*

## 🔐 Configuration & Environment Variables
Configuration is separated from code. WSO2 `deployment.toml` templating is used in conjunction with environment variables.
Secrets must **never** be hardcoded. They are expected to be injected via Kubernetes Secrets or Docker `.env` files.
See `configs/` for the deployment templates.

## 🗺 Future Roadmap
- [x] Phase 1: Foundational logging and error handling sequences.
- [x] Phase 2: Complete Customer Onboarding VETO Flow & Data Services Server (DSS).
- [x] Phase 3: Complex Order Processing Orchestration (Saga, Wire Tap, CBR).
- [x] Phase 4: Enterprise Security Architecture & OWASP Top 10 Mitigation.
- [ ] Phase 5: Implement AMQP/Kafka eventing.

## 📚 API & Flow Documentation
- [Customer API Specification](docs/apis/customer-api-openapi.yaml)
- [Customer Onboarding Sequence Diagram](docs/architecture/customer_onboarding_flow.md)
- [Order API Specification](docs/apis/order-api-openapi.yaml)
- [Order Processing Orchestration Diagram](docs/architecture/order_processing_flow.md)

## 🛡️ Security Documentation
- [Security Architecture](docs/security/01-Security-Architecture.md)
- [Authentication & Authorization](docs/security/02-Authentication-Authorization.md)
- [Secrets Management](docs/security/03-Secrets-Management.md)

## 📄 License
This project is licensed under the MIT License. See the `LICENSE` file for details.

## 🤝 Contribution Guide
Please read `CONTRIBUTING.md` and `CODE_OF_CONDUCT.md` for details on our code of conduct and the process for submitting pull requests.

---
**Status**: ✅ Phase 4: Enterprise Security Architecture Completed
