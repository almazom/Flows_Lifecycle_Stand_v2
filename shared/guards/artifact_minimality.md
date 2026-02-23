# 🛡️ artifact_minimality.md

## What

Keep mandatory artifact set compact and auditable. No bloat, no missing core.

## Biology

```
Nest = structured, minimal, complete
Every chamber serves a purpose
No empty chambers, no duplicate chambers
```

## Contract

```yaml
principle:
  - mandatory_core_must_exist: true
  - optional_artifacts_cannot_replace_core: true
  - no_duplicate_truth_sources: true
  - canonical_source: "shared/guards/artifact_minimality.md"
```

## Mandatory Core Artifact Set (15 items)

```
01. metadata/run_manifest.yaml
02. metadata/input_manifest.yaml
03. reports/preflight/environment_gate_report.yaml
04. reports/preflight/flow_version_lock_report.yaml
05. reports/preflight/mode_executability_report.yaml
06. reports/expert/expert_index.yaml
07. reports/fusion/fusion_report.md
08. reports/fusion/priorities_p0_p1_p2.yaml
09. cards/card_plan.yaml
10. cards/cards_index.yaml
11. ssot/SSOT_KANBAN.json
12. bio/topology_truth_report.yaml
13. bio/spawn_registry.yaml
14. bio/non_stop_watchdog.yaml
15. reports/execution/final_terminal_report.ru.md
```

## Pass

- All 15 core artifacts exist and are non-empty at terminal
- Optional artifacts supplement but do not substitute core
- No alternate core list is allowed in versioned START files

## Fail

- Any core artifact missing at terminal phase
- Core artifact exists but is empty/placeholder
- START declares a different core set than this file
