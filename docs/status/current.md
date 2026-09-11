# Apex operating status

This is the durable status record for remembered project work and operational
follow-up. Keep entries concise, dated, and free of secrets.

## Active work

- 2026-09-11: Establish the infrastructure required to run `~/code/euai-api/` on Apex. Move dependencies from `prime.lan` to Apex over time, making the full application and infrastructure reproducible on Apex when needed. Establish components and make architecture decisions incrementally with the user. No infrastructure or application changes authorized by this plan alone.
- 2026-09-11: Target service inventory: `euai-api`; PostgreSQL; LiteLLM model gateway; private `euai-pii` screening service; TEI serving locally pinned `BAAI/bge-m3` weights; PostgreSQL `pgvector`; private S3-compatible object storage; Docling Serve; and Caddy reverse proxy. Also establish the supporting secret custody, persistent storage, backups, monitoring, health checks, and recovery procedures needed for a reproducible deployment. This is a planning inventory, not evidence that all components are currently deployed.

## Project status

_No project status recorded yet._

## Decisions

_No decisions recorded yet._

## Follow-up

_No follow-up items recorded yet._

## Update convention

When the user says to remember a status, decision, task, or follow-up, record it
here or in the relevant project document, commit it, and push it to `origin`.
Do not rely on conversational memory as the sole copy.
