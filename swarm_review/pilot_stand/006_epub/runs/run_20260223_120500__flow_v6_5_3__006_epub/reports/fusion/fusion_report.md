# Fusion Report (Phase 3)

Run: `run_20260223_120500__flow_v6_5_3__006_epub`

## Summary
- Raw findings fused: 24
- Deduplicated issues: 10
- P0: 4
- P1: 5
- P2: 1

## P0
1. Step coverage false-pass when required phases are missing.
2. Secret-leak gate pass logic contradicts detected plaintext secrets.
3. Quorum/gate evidence schema is incomplete and non-auditable.
4. Auto-commit pending SHA accepted in pass path.

## P1
1. Gate-review participants lack spawn provenance for phase decisions.
2. Requirement→card→code mapping misses non-implemented backlog items.
3. Multi-source card findings not fully represented in traceability artifact.
4. Card markdown status can drift from SSOT status.
5. Phase-level combined commit labels violate canonical auto-commit phase contract.

## P2
1. Pilot DoD does not explicitly require quorum artifacts.

## Resolution
All raw findings are mapped to deduplicated issue IDs in priorities YAML with source references.
