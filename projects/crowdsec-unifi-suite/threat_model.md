# Threat model: crowdsec-unifi-suite

One-command installer that deploys the full CrowdSec + UniFi security stack (bouncer,
parser, blocklist-import) via shell and docker-compose. Runs with elevated privileges on
home gateways and servers during setup.

## Untrusted input
- Environment variables and .env configuration supplied at install time.
- Downloaded artifacts and compose/service definitions applied during install.

## In scope
- Command injection and unsafe quoting in the install shell scripts.
- Secret handling: API keys and credentials in .env must not leak into logs or the
  compose configuration.
- Unsafe defaults (world-readable credentials, overly permissive services, disabled
  verification).
- Supply-chain weaknesses in how the installer fetches and verifies components.

## Out of scope
- The components it installs (covered by their own enrollments) and UniFi OS itself.

## Severity guidance
- Command execution as root during install: critical.
- Credential exposure or weak default permissions: high.
- Supply-chain gaps (unverified downloads): high.
- Install failure without security impact: low.

## Report format
Minimal reproducer plus a small candidate patch; one issue per report, deduplicated by
root cause.
