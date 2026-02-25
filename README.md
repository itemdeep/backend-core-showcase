# Backend Core — Operational Showcase

This repository is a **public-safe** showcase of backend operational maturity:
- DEV/PROD isolation (single codebase, separate identities)
- Artifact-based deploy with rollback discipline (git-less prod runtime)
- Read-only maintenance mode (emergency brake)
- S3-compatible private object storage with short-lived signed URLs
- SSOT/Runbook-driven operations (repeatable, auditable procedures)

> Public-safe note: hostnames, paths, tokens, and secrets are intentionally redacted.

**Case study:** see `CASE_STUDY.md`
**Redaction:** see `REDACTION.md`

---

## What this proves (evidence-driven)

Evidence examples include: negative tests for environment/DB isolation, repeatable smoke checks after deploy/rollback, and signed URL TTL verification steps.

### 1) DEV/PROD Isolation (single codebase)
Optional STAGING can be introduced using the same isolation rules and release gates (artifact deploy, smoke checks, rollback).
Separation is enforced via runtime configuration and service identity (not separate codebases):
- canonical env sources (no hidden fallback)
- explicit runtime environment selection
- isolated deploy roots for DEV vs PROD
- database access controls that prevent DEV from reaching PROD (negative test)

### 2) Deploy strategy: artifact switch + rollback
Production runs from a deploy artifact directory (not a git repository). Releases use:
- timestamped backups
- deploy “switch” (canonical shortcut)
- post-deploy smoke checks
- rollback checklist when needed

### 3) Maintenance mode (read-only emergency brake)
A safe mode for incidents (abuse spikes, payment/ledger anomalies, DB degradation, post-deploy critical bugs):
- blocks write flows with maintenance responses (e.g., service unavailable)
- keeps read flows available
- blocked write attempts are auditable
- operator procedure: announce → enable → restart → verify → disable

### 4) Private object storage with signed URLs (S3-compatible)
For file/proof flows:
- presigned PUT/GET URLs with short TTL (e.g., 300s)
- private bucket (no public access)
- retention/lifecycle policy and encryption-at-rest
- least-privilege credentials and strict upload constraints (type/size/rate-limit)
- verification via repeatable smoke steps

### 5) SSOT + Runbook discipline
Operations are documented and enforced via:
- a single source of truth (SSOT) for invariants
- runbooks for deploy/rollback/maintenance/storage incidents
- “drift prevention” rules (ports, environments, operator steps)

---

## Deliverables I can provide (for clients/teams)
- MVP/Backend blueprint: requirements, risks, architecture boundaries, milestones
- Dev/Prod environment strategy: isolation rules, env/secrets discipline, DB access controls
- Deploy strategy: artifact-based release, rollback plan, smoke checks
- Maintenance mode: read-only policy, guardrails, operator checklist
- Storage hardening: signed URL flows, retention, audit trail, constraints
- Runbook + SSOT templates to keep systems maintainable over time

---

## Security & Redaction Policy
This repo is intentionally redacted. It never includes:
- secrets, tokens, DSNs, access keys
- hostnames, IPs, internal paths
- detailed access procedures (SSH/VPN/Zero Trust)

If you need deeper verification, I can provide additional evidence under NDA or via screenshared walkthrough.
