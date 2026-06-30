# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 1.x.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

Security is a top priority for this enterprise integration platform.

If you discover a security vulnerability within this project, please DO NOT open a public issue. Instead, send a private email to the project maintainers. 

We will acknowledge your report within 48 hours, and provide a timeline for a fix. 

### Secure Coding Practices
All contributors must ensure:
1. No hardcoded secrets or passwords are included in WSO2 Synapse files.
2. WSO2 Secure Vault is used for local sensitive properties.
3. Proper Input Validation is done at the API boundary to prevent injection attacks.
4. External entity references (XXE) are disabled in XML parsers where applicable.
