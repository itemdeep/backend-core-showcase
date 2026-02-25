# Backend Core — Case Study (Public-Safe)

## Goal
Demonstrate backend operational maturity: safe environment isolation, controlled releases, incident safety controls, and auditable storage flows.

## Constraints
- Single codebase, multiple runtime identities (DEV / optional STAGING / PROD)
- Production runtime must not depend on git state
- Releases must be reversible (rollback) with clear operator steps
- Storage must be private-by-default with temporary access via signed URLs

## Key Decisions

### 1) Environment isolation (DEV / optional STAGING / PROD)
- Isolation is enforced via runtime configuration, service identity, and database access controls.
- No hidden configuration fallbacks; environment selection is explicit.
- Negative tests validate that non-PROD identities cannot access PROD data.

### 2) Release strategy (artifact-based)
- Production runs from a deploy artifact directory (git-less runtime).
- Releases use timestamped backups, a deploy “switch”, smoke checks, and a rollback checklist.

### 3) Maintenance mode (read-only emergency brake)
- Incidents are handled by switching to read-only mode:
  - write flows are blocked with maintenance responses
  - read flows remain available
  - blocked writes are auditable
- Operator procedure: announce → enable → restart → verify → disable.

### 4) Private object storage (S3-compatible) with signed URLs
- Private bucket (no public access)
- Short-TTL presigned PUT/GET URLs
- Retention/lifecycle + encryption-at-rest
- Least-privilege credentials
- Upload constraints (type/size/rate-limit) + audit trail
- Verification via repeatable smoke steps, including TTL expiry checks

## Outcome
A backend core that is deploy-safe, isolated, auditable, and operator-friendly—demonstrated via documentation and repeatable verification steps (public-safe/redacted).

## Redaction policy
This case study intentionally excludes secrets, tokens, DSNs, hostnames, IPs, internal paths, and access procedures.
