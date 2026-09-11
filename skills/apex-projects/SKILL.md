---
name: apex-projects
description: Discover, test, start, stop, troubleshoot, and document development projects stored under ~/code/ on apex.lan.
compatibility: opencode
metadata:
  host: apex.lan
  project-root: ~/code
  github-namespace: manderskov
---

# Apex development projects

Use this skill whenever the request concerns a development project hosted on
Apex. All projects are stored locally under `~/code/` unless the user
explicitly identifies another path.

## Durable project context

Read [reference/projects.md](reference/projects.md) for the project inventory,
repository mappings, lifecycle conventions, test commands, ports, health
checks, and validation status. The reference is the runtime home for durable
project knowledge on Apex.

## Project workflow

1. Identify the project from the current working directory, the user's name,
   or the inventory. If it is not known, inspect `~/code/` and the relevant
   repository metadata.
2. Read the project's `AGENTS.md`, README, package manifest, Compose files,
   service definitions, and other local instructions before changing or
   running it. Do not read secret values from `.env` files.
3. Inspect current state before acting: repository status, processes, service
   status, containers, listeners, logs, and the project's own health checks.
4. Prefer the project's existing scripts and documented commands for install,
   development, build, test, start, stop, and verification. Do not invent a
   replacement workflow when the project already defines one.
5. For repository operations in the user's namespace, use SSH remotes such as
   `git@github.com:manderskov/<repository>.git`. Verify the repository and
   branch before fetch, pull, push, or other remote operations. Never expose
   SSH keys or credentials.
6. Before a normal change or lifecycle operation, state the exact project,
   command, expected effect, and verification plan. Let OpenCode request
   approval. This includes starting, stopping, restarting, building, pulling,
   installing, deploying, editing, and database operations.
7. After an approved operation, verify the result with the narrowest useful
   test: service status, logs, a project test, a health endpoint, or a local
   request as appropriate.
8. If an approved operation changes a durable project fact—path, repository,
   branch convention, service owner, lifecycle command, test command, port,
   health check, deployment method, or dependency relationship—update
   `reference/projects.md` in the same task and show the documentation diff.
9. If inspection discovers a durable fact without an approved change, propose
   the reference update and request approval before recording it.

## Safety boundaries

- Read-only inspection is the default.
- If required tools or permissions are unavailable, say so plainly. Do not use
  a suboptimal workaround; stop and identify the exact action the user must
  perform. If `sudo` or equivalent privilege is required, provide the exact
  command for the user to run instead.
- A project command is not automatically safe because it appears in a package
  script; inspect what it does before granting it approval.
- Keep repository changes scoped to the user's request and preserve unrelated
  worktree changes.
- Do not force-push, rewrite history, delete projects, remove volumes, or
  destroy databases as part of routine project management.
- Do not store secrets or tokens in the project inventory.
