# Apex infrastructure reference

This document is the durable runtime context for the `apex` agent. It lives
with the installed skill on Apex and should be updated in the same approved
task whenever a stable infrastructure fact changes.

It intentionally does not record volatile facts such as current processes,
containers, disk usage, RAM usage, service state, or software versions. The
agent must inspect those directly.

## Inventory metadata

- Last supplied inventory: 2026-08-26
- Source: user-provided persistent context
- Freshness: potentially stale; verify relevant details before relying on them

The inventory below is durable context, not authorization to connect, deploy,
or modify services.

## Network

Hostnames are lowercase. Local DNS for the `.lan` domain is handled by
`router.lan`.

### `router.lan` — `192.168.86.1`

- UCG Ultra router
- DHCP range: `192.168.86.6–192.168.86.199`
- Local DNS for `.lan`
- WireGuard network: `192.168.2.0/24`
- WireGuard port: `51820`

### `prime.lan` — `192.168.86.200`

Unraid server.

Known service endpoints:

| Service | Host or endpoint | Notes |
| --- | --- | --- |
| LiteLLM | `litellm.lan`, `192.168.86.200:4000` | Service endpoint |
| PostgreSQL 18 | `postgres.lan`, `192.168.86.200:5432` | Shared database candidate |
| pgAdmin 4 | `pgadmin4.lan`, `192.168.86.200:8792` | Database administration |
| SABnzbd | `192.168.86.200:8080`, `:8090` | Two reported endpoints; verify purpose |
| Sonarr | `192.168.86.200:8989`, `:9897` | Two reported endpoints; verify purpose |
| Code Server | `192.168.86.200:8443` | Development service |
| CouchDB | `192.168.86.200:5984` | Database/service endpoint |
| Plex Media Server | `192.168.86.200` | Port not specified; inspect live configuration |

### `apex.lan` — `192.168.86.201`

Development and infrastructure host for this agent.

Known services and endpoints:

| Service | Host or endpoint | Notes |
| --- | --- | --- |
| Caddy | Local service | Reverse proxy |
| XDB | `xdb.lan`, `192.168.86.201:3000` | Application |
| XDB Scanner | `scanner.xdb.lan`, `192.168.86.201:3001` | Application |

All development projects are stored locally under `~/code/` on Apex. Project
inventory, lifecycle commands, tests, ports, and health checks are maintained
by the `apex-projects` skill rather than duplicated here.

## Reverse proxy and relationships

- Caddy runs on `apex.lan`.
- Caddy reportedly proxies `litellm.lan` to LiteLLM on `prime.lan`.
- Caddy reportedly proxies `pgadmin4.lan` to pgAdmin on `prime.lan`.
- `postgres.lan` reportedly points directly to PostgreSQL on `prime.lan`.
- The exact Caddy configuration path, ownership convention, and reload method
  must be inspected before changing proxy configuration.

## Validation checklist

When validating or refreshing this reference, inspect only the relevant scope
and record stable facts such as:

- Apex's purpose and ownership.
- Canonical project roots and deployment locations.
- Caddy configuration location and route ownership convention.
- Docker Compose project locations and lifecycle convention.
- Database hosts, ownership, and connection boundaries.
- Relationships to `router.lan`, `prime.lan`, and other LAN machines.
- Any service-specific operational conventions.

Do not add credentials, private keys, tokens, connection secrets, or volatile
measurements here. When a reported fact is disproven, update or remove it as
part of an approved documentation change and preserve the source/date note when
useful.
