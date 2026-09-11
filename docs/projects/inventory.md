# Apex development project reference

This document is the durable runtime inventory for development projects stored
on Apex. It lives with the installed `apex-projects` skill and should be
updated in the same approved task whenever a stable project fact changes.

## Defaults

- Local project root: `~/code/`
- GitHub namespace: `https://github.com/manderskov`
- Preferred Git transport: SSH
- Preferred remote shape: `git@github.com:manderskov/<repository>.git`
- Source: user-provided persistent context, 2026-09-04

The GitHub namespace is a repository location, not authorization to push or
change remote state. Verify repository identity, branch, and remotes before
remote operations. Never record SSH key paths, tokens, or other credentials.

## Project inventory

No individual projects have been inventoried yet. Discover them from
`~/code/` and add one entry per project after validation.

### `elements-ds`

- Local path: `~/code/elements-ds`
- Runtime: Node.js static test-bench server
- Lifecycle: `npm run dev` / stop the foreground process
- Tests: `npm run check`
- Build: `npm run build`
- Health check: `http://127.0.0.1:4173/` locally or `http://192.168.86.201:4173/` from the LAN
- Ports: `4173` static test bench; binds to `0.0.0.0` by default
- Notes: Override the bind address with `DESIGN_SYSTEM_HOST` and the port with `DESIGN_SYSTEM_PORT`.
- Validated: 2026-09-09, server binding and local HTTP response

Use this format:

### `<project-name>`

- Local path: `~/code/<project-name>`
- Repository: `git@github.com:manderskov/<repository>.git` or another verified remote
- Default branch: `<branch>`
- Runtime: `<runtime or container model>`
- Lifecycle: `<start command>` / `<stop command>` / `<restart command>`
- Tests: `<test command>`
- Build: `<build command>`
- Health check: `<command or URL>`
- Ports: `<port and purpose>`
- Dependencies: `<service or host relationships>`
- Notes: `<stable operational convention>`
- Validated: `<date and scope>`

Do not record current process state, current container state, resource usage,
software versions, environment values, passwords, private keys, or tokens.

## Discovery checklist

For each project, inspect only what is relevant and safe to expose:

- Directory and repository identity.
- `AGENTS.md`, README, package manifests, lockfiles, and Compose files.
- Existing scripts and documented lifecycle/test commands.
- systemd units or Compose project names when present.
- Listening ports and local health endpoints.
- Stable relationships to Caddy, PostgreSQL, CouchDB, LiteLLM, or other
  infrastructure services.

Record validated durable facts, not guesses. If a command or endpoint is
unclear, leave it out until confirmed.
