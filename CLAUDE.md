# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Common Commands

| Command | Purpose |
|--------|---------|
| `bash scripts/prd-gate.sh origin/main` | PRD‑First gate – ensures `docs/prd‑platform.md` is approved before code changes touch `src/`, `infra/`, or `.github/`.
| `bash scripts/evidence-lint.sh` | Evidence‑First lint – verifies every use‑case document contains an **Evidence** heading.
| `bash scripts/test-all.sh` | Run the test suite (currently a placeholder that exits `0`). Add real tests later.
| `bash scripts/new-adr.sh <number> <slug>` | Create a new Architecture Decision Record in `docs/adr/` using the template.
| `bash scripts/context-reset.sh` | Regenerate the `checkpoint.md` with the latest context map.

> **Note:** The repository currently contains only documentation and templates – there is no source code yet. The above scripts are the active parts of the CI workflow.

## Running a Single Test

The test harness is not yet implemented. When tests are added, you can run an individual test by invoking the underlying test runner directly, e.g. `pytest path/to/test_file.py` or `go test ./...`. Until then, the placeholder `bash scripts/test-all.sh` is the only supported command.

## Documentation Workflow

* All changes to documentation should follow the **PRD‑First** rule in `docs/agent/rules.md`. Before any `docs/` change that affects `src/` or `infra/`, ensure `docs/prd‑platform.md` has `status: approved`.
* Use the **Evidence‑First** rule: every use‑case document (`docs/design/usecases/*.md`) must include an `Evidence` section.
* Branch naming and commit conventions are enforced in `docs/agent/rules.md`. One task → one branch → one PR.

## High‑Level Architecture Overview

| Layer | Description |
|-------|-------------|
| **Domain (DDD)** | Multiple bounded contexts (`booking`, `payment`, `iam`, `audit`, `notification`, `ledger`). Each defines aggregates, domain events, and interfaces.
| **Ports & Adapters (Hexagonal)** | Domain is independent; adapters include Spring Boot for web, Spring Security, OpenTelemetry, PostgreSQL, Redis, Kafka/RabbitMQ/NATS for messaging.
| **Contract‑First API** | OpenAPI 3.0 specifications located in `docs/api/openapi/`. Versioning strategy: keep `v1` and `v2` side‑by‑side in `docs/api/migration/`.
| **Observability** | Structured JSON logs, metrics (RED + DB/GC), and OpenTelemetry traces.
| **Security** | OWASP Top 10 compliance, PII/secret handling, SBOM/CVE gates.
| **Infrastructure** | Docker for local/CI, Kubernetes for deployment, GitHub Actions for CI, optional Terraform for IaC.

## Tech Stack

* **Language**: Java 21 (with Loom/Virtual Threads)
* **Build**: Gradle (recommended) or Maven
* **Frameworks**: Spring Boot, Spring Security, OpenTelemetry, OpenAPI 3.0
* **Data**: PostgreSQL, Redis (optional)
* **Messaging**: Kafka / RabbitMQ / NATS (pick one)
* **Observability**: JSON logs, OpenTelemetry traces, metrics
* **Security**: OWASP compliance, PII/secret avoidance, SBOM/CVE gate

## CI Workflow

GitHub Actions (`.github/workflows/agent‑qa.yml`) runs the following jobs on PRs to `main`:
1. **PRD Gate** – runs `scripts/prd-gate.sh`.
2. **Evidence Lint** – runs `scripts/evidence-lint.sh`.
3. **Tests** – runs `scripts/test-all.sh`.

All jobs must pass for the PR to be merged.

---

This CLAUDE.md is meant to be updated as the codebase evolves. Keep it in sync with the latest CI scripts and documentation changes.
