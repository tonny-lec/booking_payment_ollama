---
doc_type: "outstanding_tasks"
id: "outstanding-tasks"
version: "1.0"
last_updated: "2026-01-24"
status: "active"
---

# Outstanding Tasks - Booking & Payment DDD Platform

**Status Legend**: ![PENDING] = Not started | ![IN_PROGRESS] = In progress | ![BLOCKED] = Blocked

---

## Critical Gate

### G0-1: PRD Approval (BLOCKING ALL IMPLEMENTATION)
- **File**: `docs/prd-platform.md`
- **Current Status**: `proposed` (needs `approved`)
- **Action Required**: Human approval needed before any code implementation
- **Validation**: `bash scripts/prd-gate.sh`

---

## Phase 0: Design Completion

### P0-1: Domain Glossary
- ![IN_PROGRESS] `docs/domain/glossary.md` - Draft v0.2, consolidated

### P0-2: Context Design (6 contexts)

#### IAM Context
- ![TEMPLATE] `docs/design/contexts/iam.md` - TODO placeholders only
- ![IN_PROGRESS] `docs/design/contexts/iam-context.md` - Has content (v0.2 draft)

#### Booking Context
- ![TEMPLATE] `docs/design/contexts/booking.md` - TODO placeholders only
- ![IN_PROGRESS] `docs/design/contexts/booking-context.md` - Has content (v0.2 draft)

#### Payment Context
- ![TEMPLATE] `docs/design/contexts/payment.md` - TODO placeholders only
- ![IN_PROGRESS] `docs/design/contexts/payment-context.md` - Has content (v0.2 draft)

#### Other Contexts (All Templates)
- ![TEMPLATE] `docs/design/contexts/audit.md`
- ![TEMPLATE] `docs/design/contexts/notification.md`
- ![TEMPLATE] `docs/design/contexts/ledger.md`

### P0-3: Use Case Design (10 use cases)

#### Completed (with Evidence)
- ![IN_PROGRESS] `docs/design/usecases/iam-login-uc.md` - Complete with Evidence
- ![IN_PROGRESS] `docs/design/usecases/booking-create-uc.md` - Complete with Evidence
- ![IN_PROGRESS] `docs/design/usecases/payment-create-uc.md` - Complete with Evidence

#### Templates (TODO only)
- ![TEMPLATE] `docs/design/usecases/booking-update.md`
- ![TEMPLATE] `docs/design/usecases/booking-cancel.md`
- ![TEMPLATE] `docs/design/usecases/payment-capture.md`
- ![TEMPLATE] `docs/design/usecases/payment-refund.md`
- ![TEMPLATE] `docs/design/usecases/notification-send.md`
- ![TEMPLATE] `docs/design/usecases/audit-record.md`
- ![TEMPLATE] `docs/design/usecases/ledger-project.md`

**Validation**: `bash scripts/evidence-lint.sh` checks for Evidence sections

### P0-4: OpenAPI Specifications (ALL EMPTY)

All OpenAPI files exist but have empty `paths: {}`:
- ![PENDING] `docs/api/openapi/iam.yaml` - Needs POST /auth/login, /auth/refresh
- ![PENDING] `docs/api/openapi/booking.yaml` - Needs POST /bookings
- ![PENDING] `docs/api/openapi/payment.yaml` - Needs POST /payments
- ![PENDING] `docs/api/openapi/audit.yaml`
- ![PENDING] `docs/api/openapi/notification.yaml`
- ![PENDING] `docs/api/openapi/gateway.yaml`
- ![MISSING] `docs/api/openapi/ledger.yaml` - FILE DOES NOT EXIST

**Required per file**: paths, request/response schemas, error design, auth/authorization, compatibility policy

### P0-5: Test Plan
- ![IN_PROGRESS] `docs/test/test-plan.md` - Draft, needs specific strategies

### P0-6: Supporting Design Docs
- ![IN_PROGRESS] `docs/design/observability.md` - Draft, minimal content
- ![IN_PROGRESS] `docs/design/security.md` - Draft, minimal content

### P0-7: Architecture Decision Records
- ![MISSING] `docs/adr/` - DIRECTORY DOES NOT EXIST
- ![PENDING] `docs/adr/001-jwt-token-usage.md` - Referenced in IAM context
- ![PENDING] `docs/adr/002-password-hashing.md` - Referenced in IAM context
- ![PENDING] `docs/adr/003-conflict-prevention.md` - Referenced in Booking context
- ![PENDING] `docs/adr/004-booking-state-management.md` - Referenced in Booking context
- ![PENDING] `docs/adr/005-idempotency-implementation.md` - Referenced in Payment context
- ![PENDING] `docs/adr/006-payment-status-management.md` - Referenced in Payment context

---

## Slice A: Minimum MVP

### A1: IAM Login
- ![IN_PROGRESS] Context: `docs/design/contexts/iam-context.md`
- ![IN_PROGRESS] Use Case: `docs/design/usecases/iam-login-uc.md`
- ![PENDING] OpenAPI: `docs/api/openapi/iam.yaml`
- ![PENDING] ADRs: 001, 002

### A2: Booking Create
- ![IN_PROGRESS] Context: `docs/design/contexts/booking-context.md`
- ![IN_PROGRESS] Use Case: `docs/design/usecases/booking-create-uc.md`
- ![PENDING] OpenAPI: `docs/api/openapi/booking.yaml`
- ![PENDING] ADRs: 003, 004

### A3: Payment Create
- ![IN_PROGRESS] Context: `docs/design/contexts/payment-context.md`
- ![IN_PROGRESS] Use Case: `docs/design/usecases/payment-create-uc.md`
- ![PENDING] OpenAPI: `docs/api/openapi/payment.yaml`
- ![PENDING] ADRs: 005, 006

### A4: Observability
- ![IN_PROGRESS] Design: `docs/design/observability.md`

---

## File Cleanup (Technical Debt) - COMPLETED

1. ![COMPLETED] Consolidated duplicate context files (removed `*-context-design.md`)
2. ![COMPLETED] Consolidated duplicate usecase files (decided naming convention: `*-uc.md`)
3. ![COMPLETED] Removed `docs/domain/glossary-updated.md` (consolidated into glossary.md)
4. ![PENDING] Create `docs/adr/` directory
5. ![PENDING] Add missing `docs/api/openapi/ledger.yaml`
6. ![COMPLETED] Removed `tasks/` directory (temporary task management files)

---

## Priority Actions

1. **Get PRD approved** - Blocks all implementation
2. **Create ADR directory** - Prerequisite for context design
3. **Complete OpenAPI for IAM/Booking/Payment** - Slice A requirements

---

**Last Updated**: 2026-01-25
**File Cleanup**: Completed