# Expert Report: gate_review_integrity
Agent: `019c89ba-7a18-73d2-94e6-2bf57bd54741`

1. **P0** Quorum artifact missing required evidence fields.  
Evidence: `shared/guards/quorum.md:39`, `.../run_20260223_113700.../bio/quorum_decision_record.yaml:1`.  
Remediation: strict schema + block if missing.

2. **P1** Gate reviews claim 3 reviewers without spawn provenance for gate phases.  
Evidence: `shared/agents/INDEX.md:75`, `.../run_20260223_113700.../bio/spawn_registry.yaml:18`, `.../phase_5_quality_review.yaml:3`.  
Remediation: require spawn entries for gate-review participants.

3. **P1** Parallel-review gate passes while producer threshold is below 3.  
Evidence: `shared/EXPECTATIONS.md:51`, `.../topology_truth_report.yaml:1`, `.../satisfaction_score.yaml:18`, `.../gate_review_swarm_matrix.yaml:7`.  
Remediation: derive gate pass from hard threshold checks.

4. **P2** Evidence-integrity report lacks claim-to-artifact mapping.  
Evidence: `shared/guards/evidence_integrity.md:72`, `.../bio/evidence_integrity_report.yaml:1`.  
Remediation: add claims[] with refs[] and verification result.
