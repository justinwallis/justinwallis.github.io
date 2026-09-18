---
title: "Wallis Lab: NVR → NAS → AI Media Pipeline"
date: 2026-09-18 12:47:00 -0400
categories: [Homelab, Media]
tags: [nas, nvr, synology, automation, ai, media-pipeline, self-hosted]
---

A surveillance recorder and a media-production library solve different problems. Combining them into one undifferentiated storage pool creates retention, privacy, and workflow problems.

The architecture below keeps those jobs separate while still allowing useful footage to move from security capture into a production workflow.

## Design goals

1. Keep continuous surveillance private and disposable according to a retention policy.
2. Preserve selected project footage and camera originals on higher-capacity NAS storage.
3. Avoid copying every security recording into the production archive.
4. Make media ingest simple enough that footage is actually captured consistently.
5. Keep automated publishing behind a deliberate approval gate.
6. Make the public documentation reusable without exposing the live environment.

## High-level architecture

```text
                 ┌─────────────────────┐
                 │ Security Cameras    │
                 │ continuous capture  │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ NVR / Surveillance  │
                 │ rolling retention   │
                 │ private by default  │
                 └──────────┬──────────┘
                            │ selected clips only
                            ▼
┌──────────────┐   ┌─────────────────────┐   ┌──────────────────────┐
│ Phone /      │   │ NAS Media Ingest    │   │ Drone / Action /     │
│ Mirrorless   ├──►│ RAW-INBOX / project │◄──┤ Other Cameras        │
└──────────────┘   └──────────┬──────────┘   └──────────────────────┘
                              │
                              ▼
                   ┌─────────────────────┐
                   │ Verify + Organize   │
                   │ hash / metadata /   │
                   │ optional proxies    │
                   └──────────┬──────────┘
                              │
                              ▼
                   ┌─────────────────────┐
                   │ AI-Assisted Edit    │
                   │ transcript + visual │
                   │ selection / cleanup │
                   └──────────┬──────────┘
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
          ┌─────────────────┐  ┌─────────────────┐
          │ Long-form Master│  │ Shorts / Reels  │
          └────────┬────────┘  └────────┬────────┘
                   └─────────┬───────────┘
                             ▼
                  ┌──────────────────────┐
                  │ Private / Unlisted   │
                  │ Review + Approval    │
                  └──────────┬───────────┘
                             ▼
                        Publish
```

## Storage roles

### NVR / surveillance storage

The NVR should be optimized for:

- continuous camera recording
- predictable retention windows
- event search and playback
- fast overwrite of old footage
- security access controls

It is **not** the canonical archive for mirrorless, phone, drone, or action-camera originals.

### NAS / production storage

The NAS should be optimized for:

- original production footage
- selected exports from the NVR
- project organization
- edit assets and proxies
- finished masters
- long-term retention
- backup workflows

A production path can be as simple as:

```text
Media/
  RAW-INBOX/
  Projects/
    Example-Project/
      Originals/
      NVR-Selects/
      Audio/
      Proxies/
      Exports/
      Shorts/
```

The names above are examples, not live share names.

## Selective bridge from NVR to production

The useful bridge is not "copy all surveillance forever."

It is:

```text
camera + date/time window
        ↓
export relevant clip
        ↓
copy to project/NVR-Selects
        ↓
production pipeline
```

That keeps security retention independent from content retention and prevents a public-media workflow from having unrestricted access to the full surveillance archive.

## Deal-watch / acquisition layer

The same homelab can also support equipment acquisition automation.

A safe pattern is:

```text
approved public listing sources
        ↓
changedetection.io / source-native alerts
        ↓
filters (model, price, condition)
        ↓
notification service
        ↓
human review
```

Authenticated marketplaces should use their native alerts or explicitly permitted integrations rather than relying on brittle credential-sharing scrapers.

## Public/private boundary

This repository documents patterns, not the live system.

Public examples should use:

- `nas-01`, not a real hostname
- `camera-a`, not a real location
- example/private RFC1918 addressing
- synthetic project names
- placeholder secrets
- redacted or recreated diagrams

The live NVR topology, camera placement, private storage structure, credentials, property information, and raw recordings remain outside the public repository.

## Next build steps

- Add a generic Docker Compose example for change monitoring and notifications.
- Add a media-ingest script that creates project folders and verifies copied files.
- Add a generic NVR-export manifest format.
- Add an approval-state file format for automated publishing workflows.
- Add sanitized diagrams for storage, notifications, and media lifecycle.
