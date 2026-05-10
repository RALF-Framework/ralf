# Security Policy

RALF is currently in early framework design.

## Reporting security issues

Do not open public issues for security vulnerabilities.

Until a dedicated security contact is published, report security-sensitive concerns privately to the maintainers through the official project contact channel.

## Security scope

This repository currently contains framework documentation and examples.

Future security-sensitive areas may include:

- schema validation
- runtime adapter contracts
- tool permission models
- context packet compilation
- trace and provenance records
- domain pack imports
- AI-assisted workflow execution

## Security principles

RALF designs should follow these principles:

1. Least privilege for tools and data access.
2. Human approval for high-risk actions.
3. Traceability for important actions and outputs.
4. Clear separation between draft, recommendation, and execution authority.
5. Explicit handling of sensitive data.
6. No silent production-impacting automation.

## Sensitive data guidance

Do not include customer data, secrets, credentials, internal system URLs, proprietary domain knowledge, or regulated personal data in public examples or issues.
