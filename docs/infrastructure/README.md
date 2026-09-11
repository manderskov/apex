# Infrastructure records

- `topology.md` contains stable host, network, service, and relationship facts.
- `snapshots/` contains reviewed point-in-time outputs from the approved
  snapshot command.

Update stable facts only after validating them against live state. Do not store
credentials or volatile measurements in the durable inventory.
