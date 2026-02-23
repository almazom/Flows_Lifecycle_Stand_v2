# 🛡️ pheromone.md

## What

Old priorities decay.

## Biology

```
Fresh = strong → Old = weak → Ancient = gone
```

## Schedule

| Priority | Half-Life | Decays To |
|----------|-----------|-----------|
| P0 | 24h | P1 |
| P1 | 72h | P2 |
| P2 | 168h | Backlog |

## Artifact

`bio/pheromone_decay.yaml`

## Contract

```yaml
trigger: watchdog_tick

check:
  - P0 unverified > 24h: decay_to P1
  - P1 unverified > 72h: decay_to P2
  - P2 unverified > 168h: backlog
```
