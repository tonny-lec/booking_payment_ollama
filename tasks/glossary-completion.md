# Task: Glossary Completion

## Task ID
`GLOS-01`

## Description
Complete the domain glossary with key terms for Booking/Payment/IAM contexts.

## Context Independent
YES

## Files to Edit
- `docs/domain/glossary.md` (create if doesn't exist)

## Required Terms
- Booking: Booking, TimeRange, IdempotencyKey, Conflict Prevention
- Payment: Payment, Capture, Refund, IdempotencyKey, PaymentStatus (pending, completed, failed, refunded)
- IAM: User, Session, Token, Authentication, Authorization
- Common: Aggregate, Domain Event, Bounded Context

## Verification
- All terms defined with clear explanations
- References to use cases where terms are used
- No TODO sections remaining

## Evidence
- spec_slo_booking_payment_ddd_v0.6.md (domain terminology)
- docs/design/usecases/*.md (usage examples)

## Status
- pending

## Created
2026-01-20
