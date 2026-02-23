# Expert Report: gate_spawn_provenance
Agent: `019c89d5-6c78-7bd1-a583-930d1099b051`

1. P0 gate reviewers missing spawn provenance for phases 0/3/5/8/9.  
Evidence: `shared/agents/INDEX.md:75`, `shared/guards/spawn_registry.md:21`, `.../run_20260223_120500.../bio/spawn_registry.yaml:15`, `.../bio/quorum_decision_record.yaml:3`.  
Remediation: require spawn rows per gate reviewer.

2. P1 reviewer aliases not joinable to spawn `agent_id`.  
Evidence: `.../phase_5_quality_review.yaml:3`, `.../bio/spawn_registry.yaml:23`.  
Remediation: include `spawn_ref`/`agent_id` in review files.

3. P1 quorum cannot prove each spawned reviewer responded.  
Evidence: `shared/guards/quorum.md:20`, `.../bio/quorum_decision_record.yaml:6`.  
Remediation: require one output artifact per reviewer.
