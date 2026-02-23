# 🛡️ colony_memory.md

## What

Learn between runs. Never repeat mistakes.

## Artifacts

```
shared/colony_memory/
├── patterns.yaml       ← What works
├── anti_patterns.yaml  ← What to avoid
└── lessons.yaml        ← Insights
```

## Contract

```yaml
pre_run:
  - read: patterns → inject context
  - read: anti_patterns → warn if matched

post_run:
  - write: patterns (retention by priority)
  - write: anti_patterns (forever)
  - write: lessons
```

## Retention

| Content | Keep |
|---------|------|
| P0 patterns | Forever |
| Anti-patterns | Forever |
| P1 patterns | 30 runs |
| Lessons | 50 runs |
