# 🛡️ flow_version_lock.md

## What

Execution uses only the active contract version. No mixed-version runs.

## Biology

```
Queen's current pheromone = active version
Old queen's trail = archived, do not follow
```

## Artifact

`reports/preflight/flow_version_lock_report.yaml`

## Contract

```yaml
preflight_gate:
  validate:
    - resolved_start_path: must_match_active_version_start_md
    - flow_version_in_manifest: must_match_current_symlink_target
    - guards_root: must_resolve_to_shared_guards
    - templates_root: must_resolve_to_shared_templates

  fail_policy: block  # hard block — cannot continue with wrong version

required_fields:
  - expected_version: string
  - resolved_start_path: string
  - flow_version_match: boolean
  - guards_root_valid: boolean
  - status: pass | fail
```

## Pass

- `flow_version_match == true`
- `resolved_start_path` ends in `current/START.md` or `v{version}/START.md`
- `status == pass`

## Fail

- Mixed-version execution
- START path mismatch from symlink target
- Guards loaded from wrong version folder
