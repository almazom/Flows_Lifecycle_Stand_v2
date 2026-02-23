# Expert Report: stable_scoring_hard_gates
Agent: `019c89d5-72f3-7b52-8043-7060b47bbc63`

1. scoring template does not enforce full stable gate requirements.  
Evidence: `.../templates/SATISFACTION_SCORE_TEMPLATE.yaml:29`, `shared/guards/pilot_satisfaction.md:22`.  
Remediation: include open_p0/mandatory_artifacts/signed_run_reference fields.

2. hard-gate logic can pass while threshold unmet (`e14` issue).  
Evidence: `.../run_20260223_120500.../satisfaction_score.yaml:18`, `.../topology_truth_report.yaml:1`, `.../gate_review_swarm_matrix.yaml:7`.  
Remediation: derive gate pass from hard threshold checks.

3. registry version-to-evidence mapping inconsistency risk.  
Evidence: `.../STABLE_REGISTRY.md:16`, `.../RUN_INDEX.yaml:30`, `.../run_20260223_124500.../bio/step_coverage_report.yaml:13`.  
Remediation: enforce registry row validation against completed run metadata.
