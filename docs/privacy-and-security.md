# Privacy and Security

## Objective

Define security principles for a conversational AI system that generates SQL and retrieves information from a relational database.

This document describes the intended security approach for the portfolio demonstration. It does not claim that all controls have been implemented or tested.

## 1. Credential Management

- Never commit API keys, database passwords, access tokens, or service-account credentials to GitHub.
- Store secrets in environment variables or an appropriate secrets manager.
- Keep local environment files, such as `.env`, out of version control.
- Use placeholder values in public examples and documentation.

## 2. Database Permissions

- Use a dedicated database account for the demonstration.
- Grant only the permissions required for the intended queries.
- Prefer read-only access for analytical use cases.
- Enforce permissions within PostgreSQL rather than relying solely on the AI agent's instructions.
- Avoid exposing unnecessary tables or sensitive columns to the agent.

## 3. SQL Validation

AI-generated SQL must be treated as untrusted input.

Before execution, the system should:

- Restrict queries to permitted operations.
- Reject destructive or unauthorized statements.
- Validate table and column references where practical.
- Apply reasonable query limits and execution timeouts.
- Handle invalid queries without exposing sensitive internal details.

A read-only database role provides an additional layer of protection but does not replace other validation controls.

## 4. Data Privacy

- Use fictional or otherwise authorized data in the public demonstration.
- Do not publish employer or client records, internal database schemas, proprietary prompts, private workflow exports, or confidential screenshots.
- Avoid sending unnecessary personal or sensitive data to an external LLM.
- Review logging and retention settings for database queries and AI requests.

## 5. Error Handling

The system should distinguish between:

- A valid query that returns no records
- A request for unavailable data
- Invalid SQL
- Database connection or permission errors
- A request that requires clarification

Error messages should help the user understand the issue without revealing credentials, confidential schema details, or internal system information.

## 6. Security Testing

Before considering the demonstration ready, test that:

- Invalid or prohibited SQL is rejected.
- Database permissions prevent unauthorized writes.
- Missing credentials do not expose secrets.
- Empty results are not mistaken for execution failures.
- Query errors do not produce fabricated answers.
- Public repository files contain no real credentials or confidential data.

## Current Status

This document records planned security principles. Each control should be implemented and tested before it is described as verified.

## Scope

This is a portfolio-oriented security design, not a security audit or certification.
