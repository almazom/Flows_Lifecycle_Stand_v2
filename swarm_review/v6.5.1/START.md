# 🐜 SWARM REVIEW v6.5.1

```
╔═══════════════════════════════════════════════════════════════╗
║                                                               ║
║   6 scouts → masticator → card analysis → cards →           ║
║   FCT nurses → SSOT(JSON) → workers → PR                    ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
```

## 🚀 Start Here

```
1. Read ../../START.md          (root entry)
2. Read ../../AGENTS.md         (all agents)
3. Read ../../shared/EXPECTATIONS.md  (22 rules)
4. Read ../../shared/agents/INDEX.md  (spawn library)
5. Execute phases 0→9 below
```

---

## 🐜 Colony Lifecycle

```
🔍 SCOUTS x6       Phase 2    → 6 expert reports (parallel)
🔄 MASTICATOR      Phase 3    → Fusion P0/P1/P2
📐 CARD ARCHITECT  Phase 4a   → card_plan.yaml (before creation!)
🏗️ COMB BUILDER   Phase 4b   → Cards (1-4h each)
👩‍⚕️ FCT NURSES    Phase 5    → 95% FCT confidence
🔒 SSOT FREEZE    Phase 6    → JSON Kanban + 100% gate
👷 WORKERS x3     Phase 8    → Code + commits
✅ PR              Phase 9    → Complete!
```

---

## 📊 Phase Map

| Phase | Name | Output | Auto-Commit | Transition |
|-------|------|--------|-------------|------------|
| 0 | Preflight | Gates pass | ✓ | manual-start |
| 1 | Bootstrap | Run manifest + expert selection + input manifest | ✓ | auto |
| 2 | Scouts x6 | 6 expert reports | ✓ | auto |
| 3 | Masticator | P0/P1/P2 fusion | ✓ | auto |
| 4a | Card Analysis | card_plan.yaml | ✓ | auto |
| 4b | Comb Builder | Cards + index | ✓ | auto |
| 5 | FCT Nurses | 95% FCT quality | ✓ | auto |
| 6 | SSOT Freeze | SSOT_KANBAN.json + 100% gate | ✓ | **auto** |
| 7 | Readiness | Implementation plan | ✓ | **auto** |
| 8 | Workers | Code + commits | ✓ | **auto** |
| 9 | Final | Russian terminal report + PR | ✓ | terminal |

> **Phases 6→7→8→9 are AUTO-TRANSITION. No human gate.**

---

## 📁 Run Structure

```
runs/
└── {FlowName}_{YYYYMMDD}_{HHMMSS}/
    ├── metadata/
    │   ├── run_manifest.yaml
    │   └── input_manifest.yaml
    ├── reports/
    │   ├── preflight/
    │   │   ├── environment_gate_report.yaml
    │   │   ├── flow_version_lock_report.yaml
    │   │   └── mode_executability_report.yaml
    │   ├── expert/
    │   │   ├── expert_index.yaml          ← expert selection rationale
    │   │   ├── security/
    │   │   │   └── report.md
    │   │   ├── performance/
    │   │   │   └── report.md
    │   │   ├── maintainability/
    │   │   │   └── report.md
    │   │   ├── simplicity/
    │   │   │   └── report.md
    │   │   ├── testability/
    │   │   │   └── report.md
    │   │   └── api/
    │   │       └── report.md
    │   ├── fusion/
    │   │   ├── fusion_report.md
    │   │   └── priorities_p0_p1_p2.yaml
    │   ├── quality/
    │   │   └── card_quality_fct.yaml      ← completeness/integrity/quality axes
    │   └── execution/
    │       ├── gate_review_swarm_matrix.yaml
    │       ├── requirements_traceability.yaml
    │       ├── final_terminal_report.ru.md ← MUST BE IN RUSSIAN
    │       └── reviews/
    │           ├── phase_0_preflight_review.yaml
    │           ├── phase_3_fusion_review.yaml
    │           ├── phase_5_quality_review.yaml
    │           ├── phase_8_implementation_review.yaml
    │           └── phase_9_final_review.yaml
    ├── cards/
    │   ├── card_plan.yaml                 ← Phase 4a output
    │   ├── cards_index.yaml
    │   └── {PRIORITY}-{ID}_{title}.md
    ├── ssot/
    │   └── SSOT_KANBAN.json               ← JSON, not YAML
    └── bio/
        ├── stigmergy_signal_ledger.yaml
        ├── quorum_decision_record.yaml
        ├── pheromone_decay.yaml
        ├── mutation_record.yaml
        ├── spawn_registry.yaml
        ├── commit_log.yaml
        ├── non_stop_watchdog.yaml
        ├── step_coverage_report.yaml
        ├── topology_truth_report.yaml
        ├── evidence_integrity_report.yaml
        └── evolution_regression_report.yaml
```

---

## 🔧 Execution Modes

```yaml
modes:
  analysis_only:
    terminal: [ANALYSIS_READY, ANALYSIS_READY_WITH_RISKS]
    forbidden_claims: [all_cards_implemented, pr_created, code_committed]
    phase_8: not_applicable_by_mode

  implementation:
    terminal: [COMPLETE, COMPLETE_WITH_LIMITATIONS, BLOCKED]
    requires: [cards_exist, ssot_frozen, workers_available]
```

---

## 📋 Phase Contracts

### Phase 0 — Preflight (3 gates)

**Intent:** Validate environment, version lock, and execution mode.

**Gates:**
- `environment_gate` — write permissions, target project exists, shared resources available
- `flow_version_lock_gate` — active START = v6.5.1, symlink valid
- `mode_executability_gate` — detect agents, resolve mode, deny impossible claims

**Artifacts:**
- `reports/preflight/environment_gate_report.yaml`
- `reports/preflight/flow_version_lock_report.yaml`
- `reports/preflight/mode_executability_report.yaml`
- `reports/execution/reviews/phase_0_preflight_review.yaml`

**Pass:** All gates pass.
**Fail:** Any gate fails → BLOCKED.

---

### Phase 1 — Bootstrap

**Intent:** Create run folder, select 6 experts based on input, catalogue all input files.

**Steps:**
1. Create run folder: `{FlowName}_{YYYYMMDD}_{HHMMSS}`
2. Create GitFlow branch: `feature/swarm-review-{YYYYMMDD}`
3. **Expert Selection:** Evaluate project input → choose 6 most relevant domains → write `expert_index.yaml` with rationale
4. **Input Manifest:** Catalogue all input files (code, docs, videos) → map to expert domains → write `input_manifest.yaml`
5. Write `run_manifest.yaml`

**Artifacts:**
- `metadata/run_manifest.yaml`
- `metadata/input_manifest.yaml`
- `reports/expert/expert_index.yaml`

**Pass:** All 3 artifacts created, 6 experts selected.

---

### Phase 2 — Scouts x6 (Parallel)

**Intent:** Run 6 expert analyses in parallel as subagents. Each expert in its own folder.

**Rules:**
- Read `../../shared/agents/INDEX.md` before spawning
- Log every spawn to `bio/spawn_registry.yaml`
- Each expert writes to its own subfolder: `reports/expert/{domain}/report.md`
- Reports must include file:line evidence (no fabricated evidence)

**Expert domains:** security, performance, maintainability, simplicity, testability, api

**Artifacts (per expert):**
- `reports/expert/{domain}/report.md`

**Shared:**
- `bio/spawn_registry.yaml`

**Pass:** 6 reports exist, each with file:line evidence.
**Fail:** Any report missing or evidence-free.

---

### Phase 3 — Masticator (Fusion)

**Intent:** Merge 6 expert reports → unified P0/P1/P2 action model.

**Rules:**
- Every finding maps to exactly one of: P0, P1, P2
- Unresolved conflicts must be resolved — no ambiguous items
- Low-priority items go to explicit backlog (not dropped)
- Trigger quorum review: `fusion_decision`

**Artifacts:**
- `reports/fusion/fusion_report.md`
- `reports/fusion/priorities_p0_p1_p2.yaml`
- `reports/execution/reviews/phase_3_fusion_review.yaml`

**Pass:** All findings mapped, no unlabeled items.

---

### Phase 4a — Card Architecture Analysis

**Intent:** Determine HOW MANY cards, WHAT complexity, WHAT structure — BEFORE creating any card.

**Rules:**
- Analyze each fusion item for complexity
- Estimate card count and hours per card
- Identify card dependencies
- If any task > 4h: plan the split before writing cards
- Output a preview/plan that can be reviewed before Phase 4b

**Output (`card_plan.yaml`):**
```yaml
total_tasks: integer
estimated_cards: integer
cards_preview:
  - id: "{PRIORITY}-{sequence}"
    title: string
    priority: P0|P1|P2
    complexity_hours: float   # must be 1..4
    split_from: string | null # if split from a larger task
    depends_on: array[string]
    domain: string
```

**Pass:** All items analyzed, all estimated cards 1-4h, dependency graph complete.

---

### Phase 4b — Comb Builder (Card Creation)

**Intent:** Create cards from card_plan.yaml. Use Trello template.

**Rules:**
- Template: `../../swarm_review/artefacts/trello_cards/TRELLO_CARD_TEMPLATE.md`
- Every card ≥13/15 quality points
- Each card must have: title, context, `## 🔗 Linked Cards`, `## 🔄 Sync Context`
- 3-minute comprehension test: a middle developer must understand the card in 3 minutes

**Artifacts:**
- `cards/cards_index.yaml`
- `cards/{PRIORITY}-{ID}_{title}.md` (one per card)

**Pass:** All cards from card_plan.yaml created, all score ≥13/15.

---

### Phase 5 — FCT Nurses (Quality Loop)

**Intent:** Validate cards against 3 FCT dimensions. Iterate until 95% confidence.

**FCT Dimensions:**
| Axis | Question | Target |
|------|----------|--------|
| Completeness | Does the card contain all required information? | ≥95% |
| Integrity | Is the card internally consistent? | ≥95% |
| Quality | Can a middle dev understand it in 3 minutes? | ≥95% |

**Rules:**
- Iterate card reviews until all 3 axes ≥95%
- Trigger quorum review: `quality_95_validation`

**Output (`card_quality_fct.yaml`):**
```yaml
completeness_score: integer   # 0-100
integrity_score: integer      # 0-100
quality_score: integer        # 0-100
comprehension_3min_pass_rate: integer
template_compliance_percent: integer
confidence_percent: integer   # must reach 95
status: pass | fail
```

**Artifacts:**
- `reports/quality/card_quality_fct.yaml`
- `reports/execution/reviews/phase_5_quality_review.yaml`

**Pass:** All 3 FCT axes ≥95%, `confidence_percent ≥95`.

---

### Phase 6 — SSOT Freeze + 100% Release Gate

**Intent:** Lock the Kanban in JSON. Require explicit 100% sign-off from ≥2 nurse agents before workers start.

**Rules:**
- SSOT file is **JSON** (not YAML): `ssot/SSOT_KANBAN.json`
- Kanban states: `backlog`, `in_progress`, `done`
- 100% release gate: ≥2 nurse agents must explicitly sign off
- After freeze → auto-transition to Phase 7 (no human gate)

**SSOT_KANBAN.json schema:**
```json
{
  "version": "6.5.1",
  "flow": "swarm_review",
  "run_id": "string",
  "frozen_at": "ISO8601",
  "release_gate": {
    "confidence_percent": 100,
    "signed_by": ["nurse_agent_1", "nurse_agent_2"],
    "status": "pass"
  },
  "cards": [
    {
      "id": "string",
      "title": "string",
      "priority": "P0|P1|P2",
      "complexity_hours": "float",
      "status": "backlog|in_progress|done",
      "linked_cards": ["string"],
      "assigned_worker": "string|null"
    }
  ]
}
```

**Transition:** `auto → Phase 7`

---

### Phase 7 — Readiness

**Intent:** Create implementation plan from SSOT_KANBAN.json.

**Rules:**
- Read SSOT_KANBAN.json (single source of truth)
- Resolve worker assignments (from config.yaml modes)
- Confirm dependency order
- Auto-transition to Phase 8

**Artifact:** `reports/execution/implementation_readiness.yaml`

**Transition:** `auto → Phase 8`

---

### Phase 8 — Workers (Mode-Aware)

**Intent:** Implement all cards non-stop. Auto-commit every file change.

**Rules:**
- If `mode == analysis_only`: produce non-implementation attestation only
- If `mode == implementation`: execute cards non-stop, card by card
- Every file change → immediate commit (auto_commit guard)
- Update SSOT_KANBAN.json card status as each card completes
- Trigger quorum review: `implementation_decision`
- Maintain traceability: requirements → cards → code

**Artifacts:**
- `reports/execution/requirements_traceability.yaml`
- `reports/execution/reviews/phase_8_implementation_review.yaml`

**Transition:** `auto → Phase 9`

---

### Phase 9 — Final Verification + Terminal

**Intent:** Verify everything, emit Russian report, create PR.

**Required checks:**
- `evolution_regression_gate == pass`
- `non_stop_continuity_gate == pass`
- `step_coverage_gate == pass`
- `evidence_integrity_gate == pass`
- `card_quality_95_gate == pass`
- `decision_gate_parallel_review_gate == pass`
- `flow_version_lock_gate == pass`

**Trigger quorum:** `final_readiness_decision`

**Artifacts:**
- `reports/execution/final_terminal_report.ru.md` ← **IN RUSSIAN**
- `reports/execution/reviews/phase_9_final_review.yaml`
- `reports/execution/gate_review_swarm_matrix.yaml`

**Pass:** All checks pass, report in Russian, PR created (or COMPLETE_WITH_LIMITATIONS attested).

---

## 🛡️ Guards

| Guard | File | Covers |
|-------|------|--------|
| Stigmergy | ../../shared/guards/stigmergy.md | Artifact coordination |
| Quorum | ../../shared/guards/quorum.md | 2/3 consensus + 5 gates |
| Pheromone | ../../shared/guards/pheromone.md | Priority decay |
| Auto-commit | ../../shared/guards/auto_commit.md | File + phase commits |
| Colony Memory | ../../shared/guards/colony_memory.md | Learn between runs |
| Evidence Integrity | ../../shared/guards/evidence_integrity.md | No fake claims |
| Spawn Registry | ../../shared/guards/spawn_registry.md | Subagent tracking |
| Non-Stop Watchdog | ../../shared/guards/non_stop_watchdog.md | Auto-continue |
| Step Coverage | ../../shared/guards/step_coverage.md | All phases tracked |
| Mode Executability | ../../shared/guards/mode_executability.md | Mode contract |
| Evolution Regression | ../../shared/guards/evolution_regression.md | No logic degradation |
| Artifact Minimality | ../../shared/guards/artifact_minimality.md | Core artifact set |
| Flow Version Lock | ../../shared/guards/flow_version_lock.md | Version validation |

---

## 📋 Mandatory Core Artifact Set (15 items)

At terminal phase, ALL of these must exist and be non-empty:

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
12. bio/spawn_registry.yaml
13. bio/step_coverage_report.yaml
14. reports/execution/gate_review_swarm_matrix.yaml
15. reports/execution/final_terminal_report.ru.md
```

---

## ✅ Terminal Statuses

```yaml
ANALYSIS_READY:
  phases: 0-7 complete
  mode: analysis_only
  phase_8: not_applicable_by_mode

COMPLETE:
  phases: 0-9 complete
  cards: all done
  pr: created

COMPLETE_WITH_LIMITATIONS:
  phases: 0-9 complete
  cards: all done
  pr: not_created (infra missing)
  requires: explicit_limitations_attested

BLOCKED:
  reason: required (explicit, never null)
```

---

## 📋 Version Info

```yaml
version: 6.5.1
flow: swarm_review
based_on: v6.5
structure: v2 (shared/)

changes_from_6_5:
  # Meta-expectation fixes
  - gap-01: SSOT is now JSON (SSOT_KANBAN.json)
  - gap-02: auto_commit now triggers on file_created|file_updated
  - gap-03: expert reports in per-expert subfolders
  - gap-04: Phase 4 split into 4a (analysis) and 4b (creation)
  - gap-05: Phase 1 includes dynamic expert selection
  - gap-06: Phase 1 includes input_manifest.yaml for video/large files
  - gap-07: Phase 6 adds 100% release gate (nurses sign-off)
  - gap-08: MASTER_TEMPLATE adds Linked Cards + Sync Context
  - gap-09: Phase 5 renamed FCT Nurses with 3 quality axes
  - gap-10: artefacts/trello_cards/TRELLO_CARD_TEMPLATE.md created
  - gap-11: card_plan.yaml is Phase 4a output (preview before creation)
  - gap-12: GitFlow branch strategy in auto_commit
  - gap-13: auto_commit on_fail changed to block_phase
  - gap-14: Phase 6→7→8→9 explicit auto-transitions
  - gap-15: ExpertName as subfolder in run structure
  # Evolution regression fixes (restored from v4.5.stable)
  - evol-01: shared/agents/INDEX.md created
  - evol-02: spawn_registry guard created
  - evol-03: evidence_integrity guard created
  - evol-04: quorum.md now has 5 named decision points + review artifacts
  - evol-05: non_stop_watchdog guard created
  - evol-06: step_coverage guard created
  - evol-07: mode_executability guard created
  - evol-08: evolution_regression guard created
  - evol-09: artifact_minimality guard (15-item core set)
  - evol-10: requirements_traceability.yaml in mandatory artifacts
  - evol-11: SSOT_KANBAN.json schema defined in Phase 6
  - evol-12: COMPLETE_WITH_LIMITATIONS terminal status restored
  - evol-13: final_terminal_report.ru.md linked to explicit path
  - evol-14: flow_version_lock guard created
  - evol-15: bio/commit_log.yaml in auto_commit guard
  - evol-16: language.final_report: ru in config.yaml

next_patch: 6.5.2
next_minor: 6.6
```

---

**BEGIN: Phase 0 → Preflight**

*swarm_review v6.5.1*
