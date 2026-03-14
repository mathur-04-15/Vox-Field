# ADR 001: Use scoped IAM user instead of root account for development

**Status:** Accepted
**Date:** 2026-03-13

## Context

AWS root accounts have unrestricted access to all services and billing.
During development, I need access to DynamoDB, Lambda, API Gateway, S3,
Transcribe, and Bedrock. Using root credentials for development creates
unnecessary risk — a leaked root key means total account compromise.

## Decision

Created a dedicated IAM user with managed policies scoped to only the
AWS services needed for VoxField. Development access uses this user's
credentials via the AWS CLI.

## Consequences

- If credentials are compromised, blast radius is limited to VoxField services
- Cannot accidentally modify billing, account settings, or unrelated services
- Slightly more initial setup than just using root
- Will need to add permissions if new AWS services are introduced in later phases
- Follows AWS Well-Architected Framework security pillar best practices
