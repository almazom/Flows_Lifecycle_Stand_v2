# 🛡️ requirements_backlog_traceability.md

## What

Ensure every fused finding is mapped either to an implemented card or to an explicit backlog record.

## Artifacts

```
reports/execution/requirements_traceability.yaml
reports/execution/requirements_backlog_traceability.yaml
```

## Contract

```yaml
mapping_rule:
  - each_fusion_finding_must_map_to_exactly_one_path:
      implemented_card | deferred_backlog_item
  - no_unmapped_finding_ids: true
  - no_duplicate_mapping_paths_for_same_finding: true

required_backlog_fields:
  - finding_id: string
  - reason_deferred: string
  - target_run: string
  - owner: string
  - status: open | planned | done
```

## Pass

- All fusion IDs are mapped exactly once
- Deferred items exist in backlog traceability artifact

## Fail

- Any fusion ID missing from both artifacts
- Any finding mapped ambiguously to multiple paths
