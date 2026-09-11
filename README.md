# Apex

Apex is the infrastructure and development-operations agent for `apex.lan`.
The repository is the durable, off-server source of truth for the role,
operational procedures, infrastructure context, project context, recovery
instructions, and reviewed infrastructure snapshots.

## Repository policy

- Keep stable infrastructure facts in `docs/infrastructure/`.
- Keep project and repository facts in `docs/projects/`.
- Keep remembered work, status, decisions, and follow-up items in `docs/status/`.
- Keep replacement-host and restoration procedures in `docs/recovery.md`.
- Generate runtime snapshots only with `scripts/snapshot-infrastructure`.
- Review generated snapshots before committing them.
- Never commit passwords, tokens, private keys, `.env` files, or other secrets.
- Push commits to `origin` so the operational record survives loss of Apex.

## Runtime integrations

`apex.md`, `skills/`, and `opencode.json` are the current OpenCode source
package. A Hermes-native adapter is intentionally not included yet; its design
must be approved before it is created.

## Snapshot workflow

```bash
./scripts/snapshot-infrastructure
# review the generated directory under docs/infrastructure/snapshots/
git add docs/infrastructure/snapshots/<timestamp>
git commit -m "snapshot: capture Apex infrastructure"
git push origin main
```

Snapshots describe observed runtime state at a point in time. They do not
replace the durable inventory and must not be treated as authorization to make
changes.
