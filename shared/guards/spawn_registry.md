# 🛡️ spawn_registry.md

## What

Every spawned subagent is registered with full context pack. Auditable spawn trail.

## Biology

```
Queen dispatches workers → Each worker tracked
Colony knows: who went where, what they carried
```

## Artifact

`bio/spawn_registry.yaml`

## Contract

```yaml
trigger: subagent_spawn

action:
  - create: registry_entry
  - fill: context_pack_fields
  - append: bio/spawn_registry.yaml

required_context_pack_fields:
  - SUBAGENT        # agent name/type
  - TASK_ID         # unique task identifier
  - PHASE           # phase number
  - BIO_CASTE       # scout|masticator|comb_builder|nurse|worker
  - ROLE            # specific role within caste
  - GOAL            # exact goal statement
  - INPUT_ARTIFACTS # list of input paths
  - CONSTRAINTS     # non-stop|md-only|no-fabrication
  - OUTPUT_ARTIFACTS # expected outputs
  - OUTPUT          # summary|changed_files|risks
  - spawned_at      # ISO8601
  - started_at      # ISO8601
  - finished_at     # ISO8601

phase_1_expert_selection:
  required:
    - selected_domains: array[string]   # exactly 6
    - ranking_model: string
    - selection_rationale: string
    - fallback_domains: array[string]

phase_2_required_roles:
  source: "reports/expert/expert_index.yaml:selected_domains"
  rule: "must_dispatch_exactly_6_selected_domains"

parallel_dispatch_evidence:
  required: true
  fields:
    - dispatch_window_seconds: integer
    - all_6_dispatched_within_window: boolean
    - overlapping_runtime_pairs: integer

truth_rule:
  strict_parallel_claim_allowed_only_when:
    distinct_real_producers: ">=3"
    all_6_dispatched_within_window: true
```

## Pass

- Every spawn has registry entry
- All context pack fields complete
- Phase 2 dispatch contains exactly 6 selected expert roles
- Registry has timing evidence for dispatch and execution
- Decision gate reviews present for: phase_0, phase_3, phase_5, phase_8, phase_9

## Fail

- Missing registry rows
- Missing context fields
- Missing timing fields for spawned experts
- Less than 6 dispatched experts for phase 2
- Topology claim exceeds recorded producers
