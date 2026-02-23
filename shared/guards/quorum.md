# 🛡️ quorum.md

## What

Phase needs 2/3 consensus at 5 mandatory decision points.

## Artifact

`bio/quorum_decision_record.yaml`

## Contract

```yaml
rules:
  min_agents: 3
  pass_threshold: 0.67

process:
  - spawn: ≥3 agents
  - wait: all respond
  - collect: verdicts
  - calculate: agree / total
  - if >= 0.67: pass
  - log: bio/quorum_decision_record.yaml
```

## Mandatory Decision Points (5)

| Point | Phase | Decision Question | Required Review Artifact |
|-------|-------|-------------------|--------------------------|
| preflight_decision | 0 | Is environment ready to run? | `reports/execution/reviews/phase_0_preflight_review.yaml` |
| fusion_decision | 3 | Is P0/P1/P2 prioritization correct? | `reports/execution/reviews/phase_3_fusion_review.yaml` |
| quality_95_validation | 5 | Do cards meet 95% FCT confidence? | `reports/execution/reviews/phase_5_quality_review.yaml` |
| implementation_decision | 8 | Are all cards implemented correctly? | `reports/execution/reviews/phase_8_implementation_review.yaml` |
| final_readiness_decision | 9 | Is the terminal state valid? | `reports/execution/reviews/phase_9_final_review.yaml` |

## Per-Point Required Fields

```yaml
point_id: string
phase_id: string
decision_question: string
input_artifacts: array[string]
spawned_agents: array[string]
agent_outputs: array[string]
consolidated_verdict: string
confidence_percent: integer
classification: strict_parallel | strategy_variations
quorum_met: boolean
status: pass | fail
```

## Pass

- All 5 decision points recorded
- `quorum_met == true` for each
- Review artifact exists for each point

## Fail

- Missing decision point
- Advanced without quorum
- Missing review artifact for any point
