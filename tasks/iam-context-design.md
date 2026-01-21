# Task: IAM Context Design

## Task ID
`IAM-CTX-01`

## Description
Complete IAM bounded context design including aggregates, events, and persistence.

## Context Independent
YES

## Files to Edit
- `docs/design/contexts/iam.md`

## Required Sections
1. **Purpose**: IAM context handles authentication and authorization
2. **Aggregates**: User, Session, Token
3. **Context Map**: Relationships with other contexts
4. **Persistence**: Database schema for IAM entities
5. **Domain Events**: UserCreated, SessionCreated, TokenRefreshed
6. **Non-functional**: SLO, Observability, Security requirements
7. **Evidence**: References to PRD and spec

## Verification
- All TODO sections replaced with actual content
- Aggregate definitions include invariants
- Domain events defined with payload structure
- Evidence section completed

## Evidence
- docs/prd-platform.md (IAM scope)
- spec_slo_booking_payment_ddd_v0.6.md
- docs/design/usecases/iam-login.md

## Status
- pending

## Created
2026-01-20
