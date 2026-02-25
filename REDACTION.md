# Redaction Policy (Public-Safe)

This repository is intentionally public-safe. Do not publish or copy-paste the following:
- secrets (tokens, DSNs, access keys, private keys)
- hostnames, IPs, internal domains
- internal filesystem paths, usernames, service names that identify infrastructure
- access procedures (SSH/VPN/Zero Trust), break-glass steps
- customer/user data

## Allowed (public-safe)
- architectural patterns and decisions (why/how)
- high-level operational procedures (deploy/rollback/maintenance) without identifiers
- verification methods (smoke checks, negative tests) without sensitive outputs
- generic technology references (e.g., “S3-compatible object storage”)

## Redaction guidance
Replace with:
- domains/hosts → `dev.example.com`, `prod.example.com`
- IPs → `10.0.0.0`
- internal paths → `/srv/app`, `/$HOME/app`
- identifiers → `service-A`, `env-prod`, `user-dev`

## Review checklist (before sharing)
- No secrets visible
- No internal hostnames/domains
- No internal paths or account names
- No access steps or credentials
- Examples anonymized (IDs and object keys)
