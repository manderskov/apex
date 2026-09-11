# Apex recovery

This document describes the recovery target. Keep it procedural and free of
secrets.

## Recovery goals

A replacement host should be able to recover:

1. The Apex role and its skills from this repository.
2. The durable infrastructure and project inventories.
3. The reviewed operational procedures.
4. The current remembered project status and outstanding work.
5. Service configuration from separately protected secret/configuration backups.

## Recovery procedure

The exact host provisioning, operating-system, Docker, Caddy, DNS, and secret
restore procedures are not yet validated. Do not infer them from snapshots.
Record each procedure here only after it has been tested on a replacement or
recovery environment.

At minimum, a future validated procedure must specify:

- host naming and LAN addressing
- required packages and versions or compatibility constraints
- service ownership and startup order
- Docker Compose project locations and commands
- Caddy configuration installation and reload procedure
- secret restoration source, without recording secret values
- health checks and rollback/cleanup steps
- Hermes installation and native Apex adapter installation

## Backup boundary

GitHub protects this repository and its history. It does not protect secrets,
Docker volumes, databases, or uncommitted host configuration. Those require a
separate, tested backup plan.
