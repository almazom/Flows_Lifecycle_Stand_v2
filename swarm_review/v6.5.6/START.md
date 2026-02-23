# 🐜 SWARM REVIEW v6.5.6

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
5. Execute phases 0→9b below
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
🧪 PR REVIEW      Phase 9a   → PR_READY or HUMAN_REVIEW_REQUIRED
✅ TERMINAL        Phase 9b   → Complete!
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
| 9a | PR Review | `phase_9a_pr_review.yaml` | ✓ | **auto** |
| 9b | Final | Russian terminal report + final review | ✓ | terminal |

> **Phases 6→7→8→9a→9b are AUTO-TRANSITION. Human review can be policy-selected, not flow-blocking.**

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
    │   │   ├── mode_executability_report.yaml
    │   │   ├── secret_leak_gate_report.yaml
    │   │   └── ci_test_safety_gate_report.yaml
    │   ├── expert/
    │   │   ├── expert_index.yaml          ← expert selection rationale
    │   │   ├── {domain_1}/
    │   │   │   └── report.md
    │   │   ├── {domain_2}/
    │   │   │   └── report.md
    │   │   ├── {domain_3}/
    │   │   │   └── report.md
    │   │   ├── {domain_4}/
    │   │   │   └── report.md
    │   │   ├── {domain_5}/
    │   │   │   └── report.md
    │   │   └── {domain_6}/
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
    │           ├── phase_9a_pr_review.yaml
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
defaults:
  selected_mode: implementation
  analysis_only_requires_explicit_opt_in: true
  pr_review_mode: human

modes:
  analysis_only:
    terminal: [ANALYSIS_READY, ANALYSIS_READY_WITH_RISKS]
    forbidden_claims: [all_cards_implemented, pr_created, code_committed]
    phase_8: not_applicable_by_mode
    requires: [analysis_only_explicit_opt_in]

  implementation:
    terminal: [COMPLETE, COMPLETE_WITH_LIMITATIONS, BLOCKED]
    requires: [cards_exist, ssot_frozen, workers_available]

pr_review_modes:
  auto:
    requires: [checks_pass, reviewer_quorum_min_3]
    phase_9a_decision: PR_READY
    allows_system_final_review_claim: true

  human:
    requires: [handoff_attestation]
    phase_9a_decision: HUMAN_REVIEW_REQUIRED
    allows_system_final_review_claim: false
```

---

## 📋 Phase Contracts

### Phase 0 — Preflight (5 gates)

**Intent:** Validate environment, version lock, and execution mode.

**Gates:**
- `environment_gate` — write permissions, target project exists, shared resources available
- `flow_version_lock_gate` — active START = v6.5.5, symlink valid
- `mode_executability_gate` — detect agents, resolve mode, deny impossible claims
- `secret_leak_gate` — detect plaintext secrets in input/project paths and run artifacts
- `ci_test_safety_gate` — detect destructive/manual tests leaking into default CI recommendations

**Artifacts:**
- `reports/preflight/environment_gate_report.yaml`
- `reports/preflight/flow_version_lock_report.yaml`
- `reports/preflight/mode_executability_report.yaml`
- `reports/preflight/secret_leak_gate_report.yaml`
- `reports/preflight/ci_test_safety_gate_report.yaml`
- `reports/execution/reviews/phase_0_preflight_review.yaml`

**Pass:** All gates pass.
**Fail:** Any gate fails → BLOCKED.

---

### Phase 1 — Bootstrap

**Intent:** Create run folder, select 6 experts based on input, catalogue all input files.

**Steps:**
1. Create run folder: `{FlowName}_{YYYYMMDD}_{HHMMSS}`
2. Create GitFlow branch: `feature/swarm-review-{YYYYMMDD}`
3. **Input Manifest:** Catalogue all input files (code, docs, videos) → write `input_manifest.yaml`
4. **Dynamic Expert Selection:** Rank candidate domains by input coverage and risk → choose top 6 domains → write `expert_index.yaml` with score + rationale + fallback domains
5. If candidate domains `< 6`: fill remaining slots from fallback library and mark as synthetic coverage in `expert_index.yaml`
6. Write `run_manifest.yaml` with selected mode (`implementation` default) and explicit `analysis_only_explicit_opt_in` boolean

**Artifacts:**
- `metadata/run_manifest.yaml`
- `metadata/input_manifest.yaml`
- `reports/expert/expert_index.yaml`

**Pass:** All 3 artifacts created, exactly 6 experts selected, mode policy resolved.

---

### Phase 2 — Scouts x6 (Parallel)

**Intent:** Run 6 expert analyses in parallel as subagents. Each expert in its own folder.

**Rules:**
- Read `../../shared/agents/INDEX.md` before spawning
- Log every spawn to `bio/spawn_registry.yaml`
- Each expert writes to its own subfolder: `reports/expert/{domain}/report.md`
- Reports must include file:line evidence (no fabricated evidence)
- Reports must explicitly detect async blocking anti-patterns (`subprocess.run` in async call-paths, sync I/O in hot async handlers)
- If preferred profile is unavailable, fallback using `mode_executability` profile policy and attest fallback in spawn registry
- Dispatch all 6 selected experts within one bounded dispatch window and record timestamp evidence

**Expert domains:** selected in Phase 1 (`reports/expert/expert_index.yaml`)

**Artifacts (per expert):**
- `reports/expert/{domain}/report.md`

**Shared:**
- `bio/spawn_registry.yaml`

**Pass:** 6 reports exist, each with file:line evidence, and parallel dispatch evidence is present in spawn registry.
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
- Template resolution order:
  1. `../../03_swarm_review/artefacts/trello_cards/TRELLO_CARD_TEMPLATE.md` (preferred)
  2. `../../swarm_review/artefacts/trello_cards/TRELLO_CARD_TEMPLATE.md` (fallback)
  3. If neither exists → fail preflight
- Every card ≥13/15 quality points
- Each card must include required scoring sections: user story, business impact, pre-implementation checklist, test code, linked cards, sync context
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
  "version": "6.5.5",
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
- Default mode is `implementation`; execute cards non-stop, card by card
- If `mode == analysis_only`: allowed only when `analysis_only_explicit_opt_in == true`; produce non-implementation attestation only
- Every file change → immediate commit (auto_commit guard)
- Update SSOT_KANBAN.json card status as each card completes
- Sync generated card markdown `Status` field with SSOT state at phase-8 close
- Trigger quorum review: `implementation_decision`
- Maintain traceability: requirements → cards → code

**Artifacts:**
- `reports/execution/requirements_traceability.yaml`
- `reports/execution/requirements_backlog_traceability.yaml`
- `reports/execution/reviews/phase_8_implementation_review.yaml`

**Transition:** `auto → Phase 9a`

---

### Phase 9a — PR Review Policy Gate

**Intent:** Resolve PR review policy before terminal claim.

**Rules:**
- Read `pr_review_mode` (`auto` or `human`) from `shared/config.yaml`
- If `pr_review_mode == auto`:
  - run automated checks
  - run reviewer quorum (>=3 agents) on implementation diff
  - emit `phase_9a_pr_review.yaml` with `decision: PR_READY` only when pass
- If `pr_review_mode == human`:
  - emit `phase_9a_pr_review.yaml` with `decision: HUMAN_REVIEW_REQUIRED`
  - system must not claim final PR review/merge

**Artifact:**
- `reports/execution/reviews/phase_9a_pr_review.yaml`

**Transition:** `auto → Phase 9b`

---

### Phase 9b — Final Verification + Terminal

**Intent:** Verify gates and emit terminal report with policy-consistent PR claim.

**Required checks:**
- `evolution_regression_gate == pass`
- `non_stop_continuity_gate == pass`
- `step_coverage_gate == pass`
- `evidence_integrity_gate == pass`
- `card_quality_95_gate == pass`
- `decision_gate_parallel_review_gate == pass`
- `flow_version_lock_gate == pass`
- `stable_promotion_gate == pass`

**PR claim policy:**
- If `phase_9a_pr_review.decision == PR_READY`: allowed terminal claim `pr_reviewed_by_system: true`
- If `phase_9a_pr_review.decision == HUMAN_REVIEW_REQUIRED`: terminal must attest `pr_reviewed_by_system: false`

**Stable promotion gate criteria:**
- `satisfaction_score_percent >= 95`
- `confidence_score_percent >= 95`
- `open_p0_gaps == 0`
- `mandatory_artifacts_complete == true`
- `signed_run_reference` present in registry/index

**Trigger quorum:** `final_readiness_decision`

**Artifacts:**
- `reports/execution/final_terminal_report.ru.md` ← **IN RUSSIAN**
- `reports/execution/reviews/phase_9a_pr_review.yaml`
- `reports/execution/reviews/phase_9_final_review.yaml`
- `reports/execution/gate_review_swarm_matrix.yaml`

**Pass:** All checks pass, report in Russian, and PR status is honestly attested by selected policy.

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
| CI Test Safety | ../../shared/guards/ci_test_safety.md | Safe CI/test recommendations |
| Req Backlog Traceability | ../../shared/guards/requirements_backlog_traceability.md | No unmapped findings |
| Spawn Registry | ../../shared/guards/spawn_registry.md | Subagent tracking |
| Non-Stop Watchdog | ../../shared/guards/non_stop_watchdog.md | Auto-continue |
| Step Coverage | ../../shared/guards/step_coverage.md | All phases tracked |
| Mode Executability | ../../shared/guards/mode_executability.md | Mode contract |
| Final Gate Matrix | ../../shared/guards/final_gate_matrix.md | Deterministic final gate evidence |
| Pilot Satisfaction | ../../shared/guards/pilot_satisfaction.md | Stable scoring contract |
| Evolution Regression | ../../shared/guards/evolution_regression.md | No logic degradation |
| Artifact Minimality | ../../shared/guards/artifact_minimality.md | Core artifact set |
| Flow Version Lock | ../../shared/guards/flow_version_lock.md | Version validation |
| Portable Standalone | ../../shared/guards/portable_standalone.md | No external links or absolute paths |
| PR Review Mode | ../../shared/guards/pr_review_mode.md | Auto/human PR-review policy contract |

---

## 📋 Mandatory Core Artifact Set (18 items)

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
12. bio/topology_truth_report.yaml
13. bio/spawn_registry.yaml
14. bio/non_stop_watchdog.yaml
15. reports/execution/final_terminal_report.ru.md
16. reports/execution/reviews/phase_9a_pr_review.yaml
17. reports/execution/gate_review_swarm_matrix.yaml
18. reports/execution/reviews/phase_9_final_review.yaml
```

---

## ✅ Terminal Statuses

```yaml
DEFAULT_POLICY:
  selected_mode: implementation
  analysis_only_requires_explicit_opt_in: true
  pr_review_mode: human

ANALYSIS_READY:
  phases: 0-7 complete
  mode: analysis_only
  phase_8: not_applicable_by_mode
  allowed_only_when:
    - analysis_only_explicit_opt_in: true

COMPLETE:
  phases: 0-9b complete
  cards: all done
  pr_review_mode: auto
  pr_ready: true

COMPLETE_WITH_LIMITATIONS:
  phases: 0-9b complete
  cards: all done
  pr_review_mode: human
  pr_ready: human_review_required
  requires: explicit_handoff_attested

BLOCKED:
  reason: required (explicit, never null)
```

---

## 📋 Version Info

```yaml
version: 6.5.6
flow: swarm_review
based_on: v6.5.5
structure: v2 (shared/)

changes_from_6_5_5:
  - hard-24: phase 9 split into PR policy gate (9a) and terminal gate (9b) with auto/human modes
  - hard-25: new guard `pr_review_mode.md` added and connected in guard table
  - hard-26: shared config gains explicit `pr_review.mode` policy contract

next_patch: 6.5.7
next_minor: 6.6
```

---

**BEGIN: Phase 0 → Preflight**

*swarm_review v6.5.6*
