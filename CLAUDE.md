# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Common Commands

| Purpose | Command |
|---------|---------|
| Run CI quality gates (lint, tests, PRD gate) | `bash scripts/prd-gate.sh origin/main` + `bash scripts/evidence-lint.sh` + `bash scripts/test-all.sh` |
| Run tests individually (no tests currently defined) | `bash scripts/test-all.sh` (will exit immediately; replace with real test command when adding tests) |

> **Note:** This repository currently contains only documentation and CI scripts; there is no build or testable code yet.

## High‑Level Architecture

- **Docs** – `docs/` contains Markdown documentation for the project, including:
  - Design overviews, contexts, and use cases under `docs/design/`.
  - Agent policies and workflow guides under `docs/agent/`.
  - API specifications in `docs/api/openapi/`.
  - Security policies under `docs/security/`.
  - Runbooks and test plans under `docs/runbook/` and `docs/test/`.
- **CI** – GitHub Actions workflow `agent-qa.yml` orchestrates quality gates:
  1. PRD Gate (`scripts/prd-gate.sh`)
  2. Evidence lint (`scripts/evidence-lint.sh`)
  3. Tests (`scripts/test-all.sh`)
- **Scripts** – Helper shell scripts for gating, linting, and test orchestration in `scripts/`.
- **Git** – Standard Git configuration; the main branch is `main`.

## Important Files

- `scripts/prd-gate.sh` – Validates that a PR satisfies the PRD gate before merging.
- `scripts/evidence-lint.sh` – Runs linting checks on documentation and CI scripts.
- `scripts/test-all.sh` – Placeholder for running tests; currently exits with success.
- `docs/agent/reference/agentic_architect_initialization.md` – Core reference for initializing agents in this project.

## Future Development

- Add source code under `src/` and corresponding tests under `tests/`.
- Implement real build and lint scripts.
- Update `test-all.sh` to execute unit tests once code is added.

---

Generated with Claude Code