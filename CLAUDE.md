# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository is a **DDD (Domain-Driven Design) Agent Pack** for building a booking and payment microservices platform. It follows a contract-first, observability-first, and PRD-first approach with strong emphasis on documentation and structured development workflows.

### Key Principles
- **PRD-First**: All implementation changes require approved PRD (Product Requirements Document)
- **Evidence-First**: All proposals, changes, and reviews must include evidence (differences, logs, measurements, specifications)
- **Small Changes**: Changes should be minimal and verifiable
- **Context Independent Planning**: Tasks should be documented to be executable without conversation history

## Architecture & Structure

### High-Level Architecture
- **Design Methodology**: DDD + Hexagonal Architecture + Contract-first API + SLO/Observability-first
- **Bounded Contexts**: IAM, Booking, Payment, Notification, Audit, Ledger
- **Tech Stack**: Java 21+, Spring Boot, Spring Security, OpenTelemetry, PostgreSQL, Kafka

### Directory Structure
```
/
├── docs/                          # Main documentation (SSOT - Single Source of Truth)
│   ├── agent/                     # Agent workflow and rules
│   │   ├── rules.md                # Must/Must Not rules and Git flow
│   │   ├── workflow.md             # Workflow for agent operations
│   ├── api/                       # API specifications
│   │   └── openapi/                # OpenAPI 3.0 contract files
│   ├── design/                    # Domain design
│   │   ├── contexts/               # Bounded context definitions
│   │   ├── usecases/               # Use case designs
│   ├── plan/                      # Structured implementation plans
│   ├── test/                      # Test strategies
│   ├── prd-platform.md            # Platform PRD (status: proposed/approved)
│   ├── prd-devex-ai.md            # DevEx AI PRD
│   └── tech-stack.md              # Technology stack and constraints
├── scripts/                      # CI/CD and validation scripts
├── spec_slo_booking_payment_ddd_v0.6.md  # Main specification document
└── CLAUDE.md                     # This file
```

## Development Workflow

### Branch Naming Convention
- `feature/` - New features or documentation additions
- `fix/` - Bug fixes
- `refactor/` - Refactoring
- `docs/` - Documentation-only changes
- `chore/` - Configuration or tool changes

### Git Flow Rules
1. Always start from latest `main` branch
2. Create feature branches from main
3. One task = One PR (One Task, One PR principle)
4. Never push directly to main
5. Use descriptive commit messages with type (feat, fix, docs, etc.)

### Standard Commands

#### PRD Approval Gate
```bash
bash scripts/prd-gate.sh
```
- Checks if code/infra changes have approved PRD
- Required before implementing any code changes

#### Evidence Lint
```bash
bash scripts/evidence-lint.sh
```
- Validates that all usecase documents include Evidence section

#### Test All
```bash
bash scripts/test-all.sh
```
- Runs all tests

#### Create ADR
```bash
bash scripts/new-adr.sh 0001 decision-slug
```
- Creates Architecture Decision Record

#### Context Reset
```bash
bash scripts/context-reset.sh
```
- Regenerates checkpoint documentation

### Documentation Requirements

#### OpenAPI Specification (Contract-First)
Each OpenAPI file must include:
- `paths` (API endpoints)
- `request/response schemas` (required/optional fields, constraints, types)
- Error design (common error format, HTTP status usage)
- Authentication/Authorization (Security Scheme, RBAC)
- Compatibility policy (change rules aligned with migration)

#### Use Case Documentation
Each use case document must include:
- Purpose/Background
- Ubiquitous language (reference glossary)
- Input/Output (Command/Query/Event)
- Aggregate/Invariants/State transitions
- Failure modes and recovery (timeout/retry/idempotency/409 conflicts)
- Observability (what logs/metrics/traces to emit)
- Security (authentication/authorization/audit/PII handling)
- Test strategy (unit/integration/contract/e2e + boundaries/regressions)
- Evidence section (mandatory - see evidence-lint.sh)

## Implementation Slices

### Slice A: Minimum MVP (Current Focus)
1. **IAM**: Login/Refresh functionality
   - OpenAPI: `docs/api/openapi/iam.yaml`
   - Use Case: `docs/design/usecases/iam-login.md`
2. **Booking**: Create booking with conflict prevention
   - OpenAPI: `docs/api/openapi/booking.yaml`
   - Use Case: `docs/design/usecases/booking-create.md`
3. **Payment**: Create payment with idempotency
   - OpenAPI: `docs/api/openapi/payment.yaml`
   - Use Case: `docs/design/usecases/payment-create.md`
4. **Observability**: Minimum tracing and metrics
   - Design: `docs/design/observability.md`

### Slice B: E2E Completion
- Payment capture/refund
- Notification sending
- Audit recording

### Slice C: Compatibility and Operations
- v1/v2 coexistence and phased deprecation
- SLO/SLI and runbooks
- Incident response training

### Slice D: Event-Driven Architecture
- Ledger projections
- Event ordering/duplicate handling/reprocessing strategies

## Key Files and References

### SSOT (Single Source of Truth) Priority Order
1. `docs/agent/rules.md` - Must/Must Not rules
2. `docs/agent/workflow.md` - Workflow and 5 Commandments
3. `docs/prd-platform.md` - Platform PRD (must be approved before implementation)
4. `docs/prd-devex-ai.md` - DevEx AI PRD
5. `docs/tech-stack.md` - Technology stack and constraints
6. `docs/domain/glossary.md` - Domain glossary
7. `docs/api/openapi/*.yaml` - API contracts
8. `docs/design/usecases/*.md` - Use case designs
9. `docs/design/contexts/*.md` - Bounded context designs
10. `docs/plan/structured-plan.md` - Implementation plan
11. `docs/test/test-plan.md` - Test strategy

### Templates
- `docs/templates/usecase-template.md` - Use case template
- `docs/templates/context-template.md` - Context template
- `docs/templates/adr-template.md` - ADR template
- `docs/templates/postmortem-template.md` - Postmortem template

## Important Notes

1. **PRD Approval Required**: Before making any implementation code changes, ensure `docs/prd-platform.md` has `status: approved`

2. **Evidence Required**: All changes must include evidence. Use `# Evidence` section in documentation.

3. **No Secrets/PII**: Never include secrets or personally identifiable information in logs, traces, or AI outputs

4. **Context Efficiency**: Declare reference domains (Frontend/Backend/Auth/DB/Messaging/Observability/Security) at start of work

5. **Checkpoint Management**: For long-running tasks, update `checkpoint.md` to summarize progress

6. **Structured Planning**: Update `docs/plan/structured-plan.md` to make tasks context-independent

## Getting Started

1. Read the main specification: `spec_slo_booking_payment_ddd_v0.6.md`
2. Review agent workflow: `docs/agent/workflow.md`
3. Check current rules: `docs/agent/rules.md`
4. Understand PRD requirements: `docs/prd-platform.md`
5. Review tech stack: `docs/tech-stack.md`
6. Check structured plan: `docs/plan/structured-plan.md`

## Common Tasks

### Creating a New Feature Branch
```bash
# Update main
git checkout main
git pull origin main

# Create feature branch
git checkout -b feature/your-feature-name

# Work on feature
# Commit changes
git add .
git commit -m "feat: your feature description"

# Push to remote
git push -u origin feature/your-feature-name

# Create PR against main
```

### Running Validation Scripts
```bash
# Check PRD gate (before code changes)
bash scripts/prd-gate.sh

# Check evidence in usecase docs
bash scripts/evidence-lint.sh

# Run all tests
bash scripts/test-all.sh
```

### Working on OpenAPI Specifications
```bash
# Create branch for specific endpoint
git checkout -b docs/openapi-iam-login

# Edit docs/api/openapi/iam.yaml
# Add paths, schemas, security, etc.

# Edit docs/design/usecases/iam-login.md
# Add use case details following template

# Verify evidence section exists
bash scripts/evidence-lint.sh

# Commit and create PR
```
