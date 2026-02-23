# 🛡️ mode_executability.md

## What

Separate analysis and implementation honestly. Claims must match detected capability.

## Biology

```
Scout reports what it found — not what it imagined
Worker builds only what scout confirmed
```

## Artifact

`bio/mode_executability_report.yaml`

## Modes

```yaml
defaults:
  selected_mode: implementation
  analysis_only_requires_explicit_opt_in: true

modes:
  analysis_only:
    allowed_terminal:
      - ANALYSIS_READY
      - ANALYSIS_READY_WITH_RISKS
    forbidden_claims:
      - all_cards_implemented
      - pr_created
      - code_committed
    phase_8: not_applicable

  implementation:
    allowed_terminal:
      - COMPLETE
      - COMPLETE_WITH_LIMITATIONS
      - BLOCKED
    requires:
      - cards_exist
      - ssot_frozen
      - workers_available
```

## Contract

```yaml
preflight_check:
  - detect: available_agents
  - detect: agent_profile_health
  - detect: git_access
  - detect: write_permissions
  - resolve: mode (analysis_only | implementation)
  - resolve: expert_profile_fallback_order [explorer, default, worker]
  - deny: impossible_claims_upfront

required_fields:
  - selected_mode: analysis_only | implementation
  - analysis_only_explicit_opt_in: boolean
  - available_agents: array[string]
  - active_profile_per_role: map[string,string]
  - profile_fallback_used: boolean
  - profile_fallback_reason: string | null
  - distinct_producer_capacity: integer
  - distinct_producer_capacity_method: distinct_agent_sessions | distinct_profiles
  - strict_parallel_claim_allowed: boolean
  - git_access: boolean
  - spawn_context_pack_ready: boolean
```

## Pass

- Mode is explicitly set
- If selected_mode is analysis_only, explicit opt-in is present
- All claims bounded by detected capacity
- Analysis mode never claims code completion

## Fail

- Mode unspecified
- analysis_only selected without explicit opt-in
- Claims exceed detected capability
- Implementation claims in analysis_only mode
