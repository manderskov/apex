---
name: apex-infrastructure
description: Durable infrastructure context and safe investigation workflow for apex.lan and its LAN relationships.
compatibility: opencode
metadata:
  host: apex.lan
  scope: local-infrastructure
---

# Apex infrastructure

Use this skill for persistent infrastructure context. It is not a substitute
for inspecting live state on the machine.

## Reference

Read [reference/infrastructure.md](reference/infrastructure.md) for the
durable infrastructure inventory, its freshness metadata, and facts that still
need validation. This file is the runtime source of durable infrastructure
context on Apex.

## Investigation workflow

1. Identify whether the request concerns Apex itself, the current development
   project, or another LAN host.
2. Read the current project's `AGENTS.md` and relevant documentation before
   touching project files.
3. For Apex, inspect the narrowest relevant live state: host identity and OS,
   systemd services, Docker and Compose projects, Caddy configuration and
   status, listeners and routes, logs, storage, and application files.
4. For another LAN host, confirm name resolution and reachability first, then
   use the least-invasive available inspection. Do not assume credentials,
   roles, ports, or service ownership from the reference.
5. Distinguish observations from durable facts. If an approved change alters a
   stable fact, update `reference/infrastructure.md` in the same task and show
   the documentation diff. If inspection discovers a stable fact without an
   approved change, propose the update and request approval before recording
   it.

## Safety boundaries

- Read-only inspection is the default.
- If required tools or permissions are unavailable, say so plainly. Do not use
  a suboptimal workaround; stop and identify the exact action the user must
  perform. If `sudo` or equivalent privilege is required, provide the exact
  command for the user to run instead.
- Ask for approval before changes, including restarts, container operations,
  package installation, configuration edits, and database operations.
- Keep commands and changes narrowly scoped and reversible.
- Never expose secret values or private key material.
- Do not alter firewall, SSH, users, authentication, storage layout, or host
  power state as part of routine work.
- Do not record volatile runtime state in the reference. Re-check it live.
