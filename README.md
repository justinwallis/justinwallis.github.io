# Justin Wallis Lab Notes

This repository powers a public-safe engineering notebook for systems, homelab, automation, storage, monitoring, and AI-assisted media workflows.

The goal is to publish **reusable architecture and code without publishing the private environment that inspired it**.

## Current focus

- Self-hosted services and automation
- NAS/NVR storage architecture
- Media ingest and production pipelines
- Monitoring and deal-watch workflows
- Networking and infrastructure patterns
- Privacy-safe examples of real operational systems

## Privacy boundary

Examples in this repository are intentionally sanitized. Public material should never include:

- real private IP addresses or hostnames
- credentials, API tokens, keys, or cookies
- camera locations, blind spots, or security topology
- property maps, addresses, or floor plans
- serial numbers or unique device identifiers
- private NAS share names when they reveal internal structure
- raw surveillance archives or private family footage
- production secrets or configuration exports copied from live systems

Use synthetic names such as `camera-a`, `nas-01`, and RFC1918 example addresses when documentation needs concrete examples.

## First project

**Wallis Lab Media Pipeline** documents a privacy-safe version of a real-world workflow:

```text
capture devices
    ↓
private NVR / surveillance retention
    ↓ selected exports only
NAS production ingest
    ↓
organize / verify / proxy
    ↓
AI-assisted edit
    ↓
short-form derivatives
    ↓
private or unlisted review
    ↓
publish
```

Security recording and media production remain separate systems. The NVR is optimized for rolling surveillance retention; the NAS is the long-term production library.

## Main site

Portfolio and professional work: https://justinwallis.com
