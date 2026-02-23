# Expert Report: quorum_parallelism
Agent: `019c89ba-5f71-7fe2-87f8-9ce9a63039b1`

1. **P0** Phase-2 parallel evidence missing in current run.  
Evidence: `swarm_review/v6.5.3/START.md:193`, `swarm_review/v6.5.3/START.md:214`, `.../run_20260223_120500.../reports/expert/expert_index.yaml:3`, `.../bio/spawn_registry.yaml:12`, `.../bio/spawn_registry.yaml:15`.  
Remediation: hard-fail transition until 6 dispatches + window evidence + 6 reports exist.

2. **P1** Step coverage pass with missing required phases.  
Evidence: `shared/guards/step_coverage.md:58`, `.../run_20260223_120500.../bio/step_coverage_report.yaml:23`, `.../bio/step_coverage_report.yaml:25`, `shared/guards/quorum.md:27`.  
Remediation: compute pass from invariants only.

3. **P1** Quorum decision artifact too shallow for 2/3 audit.  
Evidence: `shared/guards/quorum.md:39`, `shared/guards/quorum.md:55`, `.../run_20260223_113700.../bio/quorum_decision_record.yaml:2`.  
Remediation: require spawned_agents, outputs, agreement ratio, confidence.

4. **P2** Pilot DoD under-specifies quorum strength.  
Evidence: `docs/flow_pilot/GITFLOW_PILOT.md:5`, `shared/guards/quorum.md:15`, `shared/config.yaml:19`.  
Remediation: add >=3-reviewer + quorum artifact requirement in pilot DoD.
