# Task: Payment Context Design

## Task ID
`PAY-CTX-01`

## Description
Complete Payment bounded context design including aggregates, events, and persistence.

## Context Independent
YES

## Files to Edit
- `docs/design/contexts/payment.md`

## Required Sections
1. **Purpose**: Payment context handles payment processing
2. **Aggregates**: Payment, PaymentStatus
3. **Context Map**: Relationships with Booking, IAM contexts
4. **Persistence**: Database schema for payment entities
5. **Domain Events**: PaymentCreated, PaymentCaptured, PaymentRefunded
6. **Non-functional**: SLO, Observability, Security requirements
7. **Evidence**: References to PRD and spec

## Verification
- All TODO sections replaced with actual content
- Aggregate definitions include invariants
- Domain events defined with payload structure
- Evidence section completed

## Evidence
- docs/prd-platform.md (Payment scope)
- spec_slo_booking_payment_ddd_v0.6.md
- docs/design/usecases/payment-create.md
- docs/design/usecases/payment-capture.md
- docs/design/usecases/payment-refund.md

## Status
- pending

## Created
2026-01-20
