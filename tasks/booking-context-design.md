# Task: Booking Context Design

## Task ID
`BOOK-CTX-01`

## Description
Complete Booking bounded context design including aggregates, events, and persistence.

## Context Independent
YES

## Files to Edit
- `docs/design/contexts/booking.md`

## Required Sections
1. **Purpose**: Booking context handles reservation management
2. **Aggregates**: Booking, TimeRange
3. **Context Map**: Relationships with IAM, Payment contexts
4. **Persistence**: Database schema for booking entities
5. **Domain Events**: BookingCreated, BookingUpdated, BookingCancelled
6. **Non-functional**: SLO, Observability, Security requirements
7. **Evidence**: References to PRD and spec

## Verification
- All TODO sections replaced with actual content
- Aggregate definitions include invariants (e.g., no overlapping time ranges)
- Domain events defined with payload structure
- Evidence section completed

## Evidence
- docs/prd-platform.md (Booking scope)
- spec_slo_booking_payment_ddd_v0.6.md
- docs/design/usecases/booking-create.md
- docs/design/usecases/booking-update.md
- docs/design/usecases/booking-cancel.md

## Status
- pending

## Created
2026-01-20
