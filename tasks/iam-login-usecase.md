# Task: IAM Login Use Case

## Task ID
`IAM-UC-01`

## Description
Complete IAM login use case design with all required sections.

## Context Independent
YES

## Files to Edit
- `docs/design/usecases/iam-login.md`

## Required Sections
1. **Purpose/Background**: Why login is needed
2. **Ubiquitous Language**: Terms used in this use case
3. **Input/Output**: Request/Response structure
4. **Domain Model**: Aggregate (User), Invariants
5. **API**: Reference to OpenAPI spec
6. **Failure Modes**: Timeout, Retry, Idempotency handling
7. **Observability**: Logs, Metrics, Traces to emit
8. **Security**: AuthN/AuthZ, PII handling
9. **Test Strategy**: Unit/Integration/Contract/E2E tests
10. **Evidence**: Root evidence for design decisions
11. **Open Issues**: Any unresolved questions

## Verification
- All TODO sections replaced with actual content
- Evidence section present (required for evidence-lint.sh)
- References to glossary and OpenAPI

## Evidence
- docs/prd-platform.md (IAM requirements)
- docs/api/openapi/iam.yaml (API contract)
- docs/test/test-plan.md (test strategy)

## Status
- pending

## Created
2026-01-20
