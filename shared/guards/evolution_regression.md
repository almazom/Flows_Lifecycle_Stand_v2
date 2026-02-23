# 🛡️ evolution_regression.md

## What

Prevent logic degradation between versions. Locked expectations must survive every upgrade.

## Biology

```
Queen's DNA = immutable
New queen inherits all genes
Mutation = tracked, deliberate, versioned
```

## Artifact

`bio/evolution_regression_report.yaml`

## Locked Expectations (Must Survive)

```yaml
must_preserve:
  - E01: each_run_separate_folder
  - E02: six_experts_parallel
  - E03: fusion_p0_p1_p2
  - E04: cards_1_to_4_hours
  - E05: quality_95_percent
  - E06: ssot_single_source_of_truth
  - E07: non_stop_until_terminal
  - E08: multi_engine_support
  - E09: honest_topology
  - E10: req_cards_code_chain
  - E11: final_report_russian
  - E12: no_fabricated_evidence
  - E13: decision_gate_parallel_review
  - E14: min_3_agents_per_gate
  - E15: stigmergy_coordination
  - E16: quorum_2_of_3
  - E17: mycelial_links
  - E18: role_differentiation
  - E19: mutation_record_on_failure
  - E20: auto_commit_per_phase
  - E21: 15_point_template_scoring
  - E22: dynamic_agent_selection
```

## Contract

```yaml
pre_version_bump:
  - verify: all_locked_expectations_present
  - verify: no_critical_guard_removed
  - verify: no_silent_phase_skip_introduced
  - record: evolution_regression_report.yaml

pass_rule:
  - missing_locked_expectations: []
  - step_coverage_status: pass
  - non_stop_continuity: preserved
  - no_fabricated_claims: true
```

## Pass

- `missing_locked_expectations == []`
- All 22 rules verifiable in new version

## Fail

- Any locked expectation removed without version bump + explicit justification
- Critical guard deleted
