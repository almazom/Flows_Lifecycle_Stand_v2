# 🛡️ stigmergy.md

## What

Coordinate via artifacts. No peer-to-peer.

## Biology

```
Ant A leaves pheromone → Environment changes → Ant B acts
```

## Artifact

`bio/stigmergy_signal_ledger.yaml`

## Contract

```yaml
deposit:
  trigger: work_complete
  action:
    - write: artifact
    - update: signal_ledger
    - fields: [event_id, phase, agent, type, artifact, timestamp]

follow:
  trigger: work_start
  action:
    - read: signal_ledger
    - find: signal_for_task
    - read: artifact
    - act: based_on_state

types: [created, updated, verified, blocked]
```

## Pass

- Phase transition has verified signal
- Block has blocked signal + reason

## Fail

- No signal at transition
