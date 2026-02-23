# 🛡️ non_stop_watchdog.md

## What

Guarantee automatic phase progression. No confirmation prompts. Never pause before terminal.

## Biology

```
Colony never sleeps mid-trail
If food exists ahead → keep moving
Only stop at nest (terminal)
```

## Artifact

`bio/non_stop_watchdog.yaml`

## Contract

```yaml
trigger: phase_complete

action:
  - update: bio/non_stop_watchdog.yaml
  - set: last_completed_phase
  - set: next_phase
  - evaluate: blocked_reason
  - if blocked_reason == null:
      continue_without_user_input: true
  - if blocked_reason != null:
      continue_without_user_input: false
      require: explicit_reason_in_report

required_fields:
  - last_completed_phase: string   # "phase_N"
  - next_phase: string | null      # null only at terminal
  - continue_without_user_input: boolean
  - blocked_reason: string | null
```

## Auto-Transition Rules

```yaml
auto_transitions:
  - from: phase_6_ssot_frozen
    to: phase_7_readiness
    type: auto
  - from: phase_7_readiness
    to: phase_8_workers
    type: auto
  - from: phase_8_workers
    to: phase_9_final
    type: auto

no_human_gate_between:
  - [phase_6, phase_7]
  - [phase_7, phase_8]
  - [phase_8, phase_9]
```

## Pass

- `continue_without_user_input == true` for every non-terminal phase
- `next_phase` always set until terminal
- No phase waited for user input

## Fail

- User confirmation requested before terminal
- Watchdog not updated across transitions
- `next_phase == null` before terminal phase
