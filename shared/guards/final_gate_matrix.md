# 🛡️ final_gate_matrix.md

## What

Make final gate outcomes deterministic and evidence-linked.

## Artifact

`reports/execution/gate_review_swarm_matrix.yaml`

## Contract

```yaml
required_fields_per_gate:
  - gate: string
  - status: pass | fail
  - evidence_refs: array[string]
  - checked_by: array[string]
  - checked_at: string
  - rule_version: string

aggregate:
  - overall_status: derived
  - fail_if_any_gate_fail: true
```

## Pass

- Every gate has evidence refs and checker identities
- `overall_status` is derived from per-gate statuses

## Fail

- Manual overall pass without per-gate evidence
- Missing gate rows or missing evidence refs
