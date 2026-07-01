# Authentication and Authorization

This guide outlines how authentication and authorization function within the integration platform.

## JSON Web Tokens (JWT)
All protected APIs require a JWT passed via the `Authorization` header.

```http
Authorization: Bearer eyJhbGciOi...
```

### Required Claims
The JWT must contain the following standard claims:
- `sub`: The subject (often the User ID or Customer ID). Used for Broken Object Level Authorization (BOLA) validation.
- `exp`: Expiration time.
- `roles`: An array of roles assigned to the identity.

Example Payload:
```json
{
  "sub": "cust_12345",
  "exp": 1720000000,
  "roles": ["user"]
}
```

## Authorization (RBAC)
Micro Integrator evaluates the `roles` extracted from the JWT.

### Defined Roles
- `admin`: Permitted to execute administrative and creation endpoints (e.g., Customer Onboarding).
- `user`: Permitted to execute user-scoped operations (e.g., Order Processing) bounded to their own `sub`.

## Testing

For testing, you must generate a valid JWT payload structure. Since signature verification is handled at the gateway layer (or mocked for development), ensuring the payload JSON is Base64 encoded correctly is sufficient for local sequence testing.