# Expert Report: evidence_integrity
Agent: `019c89ba-6125-72b1-a6e8-6f28b20b3d74`

1. **P0** Secret gate passes while detected plaintext secret exists.  
Evidence: `.../run_20260223_120500.../reports/preflight/secret_leak_gate_report.yaml:1`, `...:3`, `shared/guards/evidence_integrity.md:32`.  
Remediation: deterministic fail on non-empty detected secret files.

2. **P0** Step coverage pass despite missing phases.  
Evidence: `.../bio/step_coverage_report.yaml:23`, `...:25`, `shared/guards/step_coverage.md:21`, `shared/guards/step_coverage.md:64`.  
Remediation: enforce fail when required phases missing.

3. **P1** Quorum evidence fields missing in recorded artifact.  
Evidence: `.../run_20260223_113700.../bio/quorum_decision_record.yaml:2`, `shared/guards/quorum.md:40`.  
Remediation: enforce schema and fail on mismatch.

4. **P1** Auto-commit pending SHA accepted as pass.  
Evidence: `.../run_20260223_120500.../bio/commit_log.yaml:4`, `shared/guards/auto_commit.md:27`, `shared/guards/auto_commit.md:74`.  
Remediation: block phase when SHA is pending.
