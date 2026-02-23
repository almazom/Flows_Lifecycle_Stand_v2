# 🛡️ evidence_integrity.md

## What

Block fabricated evidence and topology fiction. No claim without artifact.

## Biology

```
No pheromone trail = no food here
Fake trail = colony dies
```

## Artifacts

```
bio/topology_truth_report.yaml
bio/evidence_integrity_report.yaml
```

## Contract

```yaml
hard_rules:
  - no_claim_without_artifact: true
  - no_distinct_producer_claim_without_distinct_engine_session_pairs: true
  - no_simulated_pr_claim_without_pr_url: true
  - no_plaintext_secret_in_run_artifacts: true

preflight_secret_gate:
  required: true
  block_on_detected_plaintext_secret: true

topology_rules:
  strict_parallel_min_distinct_producers: 3
  phase2_six_expert_dispatch_required: true
  phase2_dispatch_source: "bio/spawn_registry.yaml"
  if_distinct_producers_below_3:
    classification: strategy_variations
    strict_parallel_claim_allowed: false
  forbidden_terms_when_not_strict_parallel:
    - "three-way quorum passed"
    - "3 distinct producers verified"
    - "parallel execution confirmed"

on_violation:
  action: set_terminal_status → BLOCKED
  reason: fabricated_evidence
```

## Required Artifact Fields

```yaml
topology_truth_report:
  - actual_distinct_producers: integer
  - classification: strict_parallel | strategy_variations
  - fabricated_claims_found: boolean
  - strict_parallel_claim_allowed: boolean
  - phase2_six_expert_dispatch_verified: boolean
  - phase2_dispatch_window_seconds: integer

evidence_integrity_report:
  - no_claim_without_artifact: boolean
  - no_fake_parallel_claim: boolean
  - no_fake_pr_claim: boolean
  - no_fake_six_expert_dispatch_claim: boolean
  - status: pass | fail
```

## Pass

- All claims have referenced artifacts
- `fabricated_claims_found == false`
- `phase2_six_expert_dispatch_verified == true` for strict_parallel phase-2 claims
- `status == pass`

## Fail

- Any claim without artifact → BLOCKED
- Fake parallel with < 3 producers → BLOCKED
- Claiming six parallel expert dispatch without spawn evidence → BLOCKED
