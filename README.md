# Twin Sync

A Mac ↔ PC workflow sync layer that keeps two development machines (and the AI assistants running on them) in lockstep — shared plans, shared memory, shared skills — so switching keyboards doesn't cost you context.

> *This repo is a public overview. The running code is private.*

---

## What it is

Running Claude Code on two machines usually means two parallel universes of context: the agent on the Mac doesn't know what the agent on the PC just did. Twin Sync makes both machines read from and write to a shared source of truth — a dedicated network drive — so one session picks up exactly where the other left off.

## What it does

- **Designates the Mac as the source of truth** for plans, skills, memory, and active project files
- **Pushes updates to a shared network drive** via scheduled rsync
- **PC reads from the same drive** on agent startup — plans, memory, skill definitions are identical
- **Cross-machine messaging** through a relay API so an agent on one machine can signal the other ("done — your turn")
- **Drift detection** — the sync job reports when files changed in both places between syncs

## Software

| Layer | Tech |
|---|---|
| File transport | rsync on a schedule (launchd on Mac, Task Scheduler on PC) |
| Shared storage | Dedicated network drive (SMB) |
| Cross-machine messaging | Relay API (Next.js route, running on Mac Mini) |
| Source of truth | Mac home subset: plans, skills, memory, active-project files |

## What this demonstrates

- **Sync that respects hierarchy** — one side is canonical, conflicts resolve predictably
- **AI agents as peers** — two Claude Code instances collaborating via shared state, not shared prompts
- **Operational discipline** — scheduled jobs, drift detection, repeatable and inspectable

## Stack

![rsync](https://img.shields.io/badge/rsync-000000?style=flat&logo=gnubash&logoColor=white)
![macOS](https://img.shields.io/badge/macOS-000000?style=flat&logo=apple&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D4?style=flat&logo=windows11&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=nextdotjs&logoColor=white)

## Related in the AIOS Portfolio

- **[Remote Dev Stack](https://github.com/mikecutillo/remote-dev-stack)** — Sibling tool; Tailscale + tmux + CRD mesh access with persistent Claude Code sessions
- **[NAS Plex Tools](https://github.com/mikecutillo/nas-plex-tools)** — Python toolkit for Plex on the same NAS the sync writes to
- **[AIOS](https://github.com/mikecutillo/aios)** — The synced workload; Next.js dashboard orchestrating 16+ household and business modules

---

Part of the AIOS portfolio. See the [profile README](https://github.com/mikecutillo) for the full system map.
