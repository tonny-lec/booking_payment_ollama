# Outstanding Tasks for Booking & Payment DDD Platform

## Overview
This document outlines the incomplete tasks and documentation that needs to be completed for the booking and payment microservices platform following DDD principles.

## 1. PRD Approval Required
- **Status**: PRD currently in `proposed` status
- **Action**: Get `docs/prd-platform.md` approved before implementing any code changes

## 2. Documentation Completion - Context Design
The following context design documents are incomplete (status: draft):
- `docs/design/contexts/iam.md` - IAM context design
- `docs/design/contexts/booking.md` - Booking context design
- `docs/design/contexts/payment.md` - Payment context design

## 3. Documentation Completion - Use Cases
The following use case documents are incomplete (status: draft):
- `docs/design/usecases/iam-login.md` - IAM login use case
- `docs/design/usecases/booking-create.md` - Booking creation use case
- `docs/design/usecases/payment-create.md` - Payment creation use case

## 4. API Contract Completion
The following OpenAPI specifications are incomplete (paths are empty):
- `docs/api/openapi/iam.yaml` - IAM API contract
- `docs/api/openapi/booking.yaml` - Booking API contract
- `docs/api/openapi/payment.yaml` - Payment API contract

## 5. Supporting Documentation
- `docs/domain/glossary.md` - Missing - needs to be created
- `docs/design/observability.md` - Draft status
- `docs/design/security.md` - Draft status

## 6. Test Plan
- `docs/test/test-plan.md` - Draft status, needs to be fully fleshed out with specific test strategies for each use case

## 7. Implementation Plan
Based on `docs/plan/structured-plan.md`, the following tasks need to be completed:
1. Gate 0: PRD approval (currently in proposed state)
2. Phase 0: Design completion (context design, use case design, API contracts)
3. Slice A: Documentation completion for all MVP features

## 8. Validation Requirements
The project has validation scripts that check:
- `scripts/prd-gate.sh` - Ensures PRD approval before code changes
- `scripts/evidence-lint.sh` - Ensures all use case documents have Evidence section

## Summary of Work Needed
All the files are currently in draft form and need to be fully developed according to the templates and standards established in the project documentation. The main work that needs to be completed includes:

1. Completing the PRD approval process
2. Filling out all context design documents with proper domain modeling
3. Implementing the use case specifications with complete evidence sections
4. Developing the API contracts with proper paths and schemas
5. Creating the domain glossary
6. Finalizing the test strategy

This represents the core work needed to establish the foundation for the booking and payment microservices platform following DDD principles.