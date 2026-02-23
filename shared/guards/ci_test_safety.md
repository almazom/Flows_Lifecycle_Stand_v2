# 🛡️ ci_test_safety.md

## What

Prevent unsafe CI/test recommendations (destructive or manual-only paths leaking into default automated pipelines).

## Artifact

`reports/preflight/ci_test_safety_gate_report.yaml`

## Contract

```yaml
preflight_gate:
  validate:
    - no_destructive_test_in_default_ci: true
    - manual_or_local_only_tests_marked: true
    - no_env_mutation_test_without_isolation: true

required_fields:
  - destructive_tests_detected: integer
  - unmarked_manual_tests_detected: integer
  - env_mutation_tests_detected: integer
  - status: pass | fail
```

## Pass

- `status == pass`
- No destructive/manual leaks into default CI recommendation set

## Fail

- Any destructive/manual test path can be selected by default CI
