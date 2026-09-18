# Public / Private Boundary

This repository is designed to document real engineering patterns without documenting the private environment itself.

## Never commit

- passwords, cookies, API keys, access tokens, SSH private keys
- exported live configuration containing credentials
- public or private IP mappings that identify the real environment
- Tailscale device names or sensitive internal DNS names
- real camera placement, security blind spots, or coverage maps
- home/property address or parcel information
- serial numbers, MAC addresses, account IDs, or other unique identifiers
- raw surveillance video
- private family media
- private Drive documents or screenshots containing sensitive data

## Safe substitutes

Use:

- `nas-01`
- `nvr-01`
- `camera-a`
- `project-example`
- `192.168.50.0/24` or another synthetic private network
- `CHANGEME` / environment variables for credentials

## Review rule

Before publishing a screenshot, configuration snippet, log, diagram, or video frame, ask:

> Could this materially help someone reconstruct the real network, security layout, property, credentials, or private life?

If yes, recreate it with synthetic data rather than redacting a live export.
