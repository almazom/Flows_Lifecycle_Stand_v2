# 🛡️ pilot_satisfaction.md

## What

Make pilot-run satisfaction and confidence scoring explicit, reproducible, and evidence-linked.

## Artifacts

```
swarm_review/pilot_stand/006_epub/templates/SATISFACTION_SCORE_TEMPLATE.yaml
swarm_review/pilot_stand/006_epub/STABLE_REGISTRY.md
```

## Contract

```yaml
scoring:
  source_rules: E01..E22
  formula: "mean(E01..E22) with P0 penalty"
  evidence_links_required: true

stable_gate:
  thresholds:
    satisfaction_percent: 95
    confidence_percent: 95
  requires:
    - open_p0_gaps: 0
    - mandatory_artifacts_complete: true
    - signed_run_reference: true
```

## Pass

- Scorecard has explicit formula and evidence links
- Stable mark only when thresholds are met with signed run reference

## Fail

- Manual stable declaration without score evidence
- Missing formula/evidence linkage in score artifacts
