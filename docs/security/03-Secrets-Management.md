# Secrets Management

Enterprise security mandates that no credentials or secrets are ever stored in source code.

## WSO2 Secure Vault
For traditional VM-based or static deployments, use the WSO2 Secure Vault (`cipher-tool.bat` / `cipher-tool.sh`).

1. Define passwords in `conf/security/cipher-text.properties`.
2. Map aliases in `conf/security/cipher-tool.properties`.
3. Reference in code using: `wso2:vault-lookup('alias')`.

## Environment Variables (Cloud Native)
For Kubernetes and Docker deployments, environment variables injected via Kubernetes Secrets are the preferred standard.

### Usage in Micro Integrator
Environment variables can be referenced in `.xml` endpoints or Data Services using the `$SYSTEM:` prefix.

Example Data Service Connection:
```xml
<property name="password">$SYSTEM:SYSTEM_DB_PASSWORD</property>
```

### Local Development
When developing locally using Docker, pass the secrets via `.env` files or `-e` flags.

```bash
docker run -p 8290:8290 -e SYSTEM_DB_PASSWORD=MySecurePassword123! my-integration-hub:latest
```

## Hardcoded Value Audits
Continuous CI/CD scanning (e.g., TruffleHog, Gitleaks) must be integrated to ensure no developer inadvertently commits passwords, API keys, or certificates into this repository.