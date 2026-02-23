# 🐜 SWARM REVIEW v6.5

```
╔═══════════════════════════════════════════════════════════════╗
║                                                               ║
║   6 scouts → masticator → cards → workers → PR              ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
```

## 🚀 Start Here

```
1. Read ../../START.md (root entry)
2. Read ../../AGENTS.md (all agents)
3. Read ../../shared/EXPECTATIONS.md (22 rules)
4. Execute phases 0→9 below
```

---

## 🐜 Colony Lifecycle

```
🔍 SCOUTS x6    Phase 2    → 6 expert reports
🔄 MASTICATOR   Phase 3    → Fusion P0/P1/P2
🏗️ COMB BUILDER Phase 4    → Cards (1-4h each)
👩‍⚕️ NURSES      Phase 5    → 95% confidence
👷 WORKERS x3   Phase 8    → Code + commits
✅ PR           Phase 9    → Complete!
```

---

## 📊 Phase Map

| Phase | Name | Output | Commit |
|-------|------|--------|--------|
| 0 | Preflight | Gates pass | ✓ |
| 1 | Bootstrap | Run manifest | ✓ |
| 2 | Scouts | 6 reports | ✓ |
| 3 | Masticator | P0/P1/P2 | ✓ |
| 4 | Comb Builder | Cards | ✓ |
| 5 | Nurses | 95% quality | ✓ |
| 6 | SSOT | Kanban frozen | ✓ |
| 7 | Readiness | Plan | ✓ |
| 8 | Workers | Code | ✓ |
| 9 | Final | PR | ✓ |

---

## 📁 Run Structure

```
runs/
└── swarm_review_YYYYMMDD_HHMMSS/
    ├── reports/
    │   ├── expert/
    │   │   ├── 01_security.md
    │   │   ├── 02_performance.md
    │   │   ├── 03_maintainability.md
    │   │   ├── 04_simplicity.md
    │   │   ├── 05_testability.md
    │   │   └── 06_api.md
    │   ├── fusion/
    │   │   ├── fusion_report.md
    │   │   └── priorities.yaml
    │   └── quality/
    │       └── card_quality.yaml
    ├── cards/
    │   ├── cards_index.yaml
    │   └── *.md
    ├── ssot/
    │   └── SSOT_KANBAN.yaml
    └── bio/
        ├── stigmergy_signal_ledger.yaml
        ├── quorum_decision_record.yaml
        ├── pheromone_decay.yaml
        └── mutation_record.yaml
```

---

## 🛡️ Guards (from shared/)

| Guard | File |
|-------|------|
| Stigmergy | ../../shared/guards/stigmergy.md |
| Quorum | ../../shared/guards/quorum.md |
| Pheromone | ../../shared/guards/pheromone.md |
| Auto-commit | ../../shared/guards/auto_commit.md |
| Colony Memory | ../../shared/guards/colony_memory.md |

---

## 📴 Template

- ../../shared/templates/MASTER_TEMPLATE.md

---

## 🎭 Castes

| Caste | Phase | Agents |
|-------|-------|--------|
| scout | 2 | 6 parallel |
| masticator | 3 | 1 |
| comb_builder | 4 | 1 |
| nurse | 5 | 1-3 |
| worker | 8 | 3 |

---

## ✅ Terminal Statuses

```yaml
ANALYSIS_READY:
  phases: 0-7 complete
  mode: analysis_only

COMPLETE:
  phases: 0-9 complete
  cards: all implemented
  pr: created

BLOCKED:
  reason: required
```

---

## 📋 Version Info

```yaml
version: 6.5
flow: swarm_review
structure: v2 (shared/)

changes:
  - Uses shared/ resources
  - Version folder structure
  - current → v6.5 symlink

next_patch: 6.5.1
next_minor: 6.6
```

---

**BEGIN: Phase 0 → Preflight**

*swarm_review v6.5*
