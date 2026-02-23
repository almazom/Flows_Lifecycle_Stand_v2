# Expert Report: producer_counting_model
Agent: `019c89d5-6a67-7bf0-ab78-6c77a183fd65`

1. P0 `mode_executability_report` uses free-form producer capacity.  
Evidence: `.../mode_executability_report.yaml:9`.  
Remediation: derive from unique `(engine,session_id)` pairs in spawn registry.

2. P1 spawn registry lacks `engine_id/engine_session_id/producer_instance_id`.  
Evidence: `shared/guards/spawn_registry.md:28`.  
Remediation: add required fields and reject incomplete rows.

3. P1 producer rule in evidence integrity should require pair list proof.  
Evidence: `shared/guards/evidence_integrity.md:26`.  
Remediation: require `distinct_engine_session_pairs` list and count derivation.
