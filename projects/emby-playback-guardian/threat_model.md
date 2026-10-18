# Threat model: emby-playback-guardian

Python Docker container that watches Emby/Jellyfin playback and pauses library tasks,
kills stuck scans, and throttles download clients (Sonarr/Radarr/qBittorrent-class APIs)
during active streaming. Holds admin API keys for media services and runs unattended.

## Untrusted input
- Emby/Jellyfin API session and webhook data, which reflects client-controlled state.
- Download-client API responses.
- Environment/.env configuration.

## In scope
- API key and token leakage into logs, metrics, or error output.
- Injection into commands or API calls sent to download clients.
- Unsafe process-kill or task-control logic that could be driven by crafted session data.
- Denial of service of the host media services through the guardian's control plane.

## Out of scope
- Emby/Jellyfin and the download clients themselves.

## Severity guidance
- Credential exposure or takeover of connected media services: high.
- Injection reaching download clients: high.
- Crash or control-loop denial of service: medium.
- Cosmetic issues: low.

## Report format
Minimal reproducer plus a small candidate patch; one issue per report, deduplicated by
root cause.
