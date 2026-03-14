# CLAUDE.md

## Project: VoxField
AI-powered field service assistant that lets HVAC technicians log jobs, track parts, and manage their workday via SMS and voice notes. No app required.

## Boundaries
- Only modify files within this project directory
- Never modify files in ~/, ~/.zshrc, ~/.ssh, ~/.aws, or any system directories
- Never install global npm packages without asking first
- Always confirm before running destructive commands (rm -rf, drop table, delete, etc.)
- Never commit secrets, API keys, or credentials to the repository

## Tech Stack
- Python 3.x for Lambda handlers
- AWS SAM for infrastructure-as-code
- DynamoDB for data storage (single-table design)
- Amazon Transcribe for voice-to-text
- AWS Bedrock (Claude) for AI processing
- Twilio for SMS/MMS messaging

## Conventions
- Write ADRs for every significant architectural decision in docs/decisions/
- ADR format: Title, Status, Date, Context, Decision, Consequences
- Add learning journal entries to docs/learning-journal.md after each milestone
- Use snake_case for Python files and function names
- Use UPPER_SNAKE_CASE for environment variables
- Handlers go in src/handlers/, shared logic goes in src/lib/
- Every handler should have a corresponding test in tests/

## Architecture Principles
- Event-driven: Lambda functions triggered by API Gateway, S3, or EventBridge
- Serverless-first: No EC2 instances, no always-on infrastructure
- Tenant isolation: DynamoDB partition key (TECH#phone) scopes all data per technician
- Narrow AI scope: The Bedrock prompt only parses job updates; rejects everything else

## Current Phase
Phase 0 — Environment Setup
