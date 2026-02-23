# 🛡️ step_coverage.md

## What

Every phase 0→9 must have explicit status. No silent skipping.

## Biology

```
Every chamber in the nest = inspected
Empty chamber without note = alarm
```

## Artifact

`bio/step_coverage_report.yaml`

## Contract

```yaml
required_phases: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

allowed_statuses:
  - pass
  - fail
  - not_applicable_by_mode

rules:
  no_phase_with_missing_status: true
  critical_phases_cannot_be_not_applicable: [0, 1, 2, 3, 4, 5, 6, 9]
  mode_dependent_phases: [8]   # phase_8 = not_applicable in analysis_only

trigger: phase_complete
action:
  - append: bio/step_coverage_report.yaml
  - set_phase_status: pass | fail | not_applicable_by_mode
```

## Required Artifact Fields

```yaml
step_coverage_report:
  required_span: "0->9"
  allow_phase_skip: false
  allow_silent_skip: false
  phases:
    - phase_id: string
      status: pass | fail | not_applicable_by_mode
      artifact_refs: array[string]
      note: string | null
  all_required_phases_present: boolean
  no_critical_phase_skipped: boolean
  status: pass | fail
```

## Pass

- All phases 0-9 have explicit status
- No critical phase is `not_applicable_by_mode`
- `status == pass`

## Fail

- Any phase without status → fail
- Critical phase silently skipped → fail
