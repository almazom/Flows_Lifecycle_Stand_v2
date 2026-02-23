# P1-05: Add Pilot Satisfaction Scoring Guard

**Priority:** P1
**Complexity:** 2.5h
**Status:** Backlog

## 👤 User Story (Given/When/Then)
Given we run multiple flow versions on a pilot project
When a run ends
Then satisfaction/confidence scoring must be calculated consistently and auditable.

## 💼 Business Impact
Enables objective progression to stable versions instead of subjective status.

## 📋 Description
Add scoring guard and normalization rules for `E01..E22` plus weighted final satisfaction/confidence.

## 🌍 Context
Current template has score slots but no hard contract for scoring process and evidence linkage.

## ✅ Pre-Implementation Checklist
- [ ] Score formula documented
- [ ] Required evidence links enforced
- [ ] Stable threshold integrated

## 🔗 Linked Cards
| Card ID | Relationship | Direction |
|---------|-------------|-----------|
| P1-03 | blocked_by | ← this card |
| P2-06 | blocks | → this card |

## 🔄 Sync Context
**Depends on state:** run artifacts complete  
**Produces state:** auditable satisfaction and confidence scoring

## 📍 Location
File: `swarm_review/pilot_stand/006_epub/templates/SATISFACTION_SCORE_TEMPLATE.yaml`  
Lines: `5-33`

## 🔴 Current Code (ACTUAL — not placeholder)
```yaml
aggregation:
  expectation_score_percent: 0
  satisfaction_score_percent: 0
  confidence_score_percent: 0
  stable_candidate: false
```

## 🟢 Fixed Code (copy-paste ready)
```yaml
aggregation:
  expectation_score_percent: 0
  satisfaction_score_percent: 0
  confidence_score_percent: 0
  stable_candidate: false
  formula: "mean(E01..E22) with P0 penalty"
  evidence_links_required: true
```

## 🧪 Test Code (complete, runnable)
```bash
#!/usr/bin/env bash
set -euo pipefail
rg -n "formula|evidence_links_required" swarm_review/pilot_stand/006_epub/templates/SATISFACTION_SCORE_TEMPLATE.yaml
```

## ⚠️ Risk Assessment
| Risk | Level | Mitigation |
|------|-------|------------|
| Score manipulation by manual edits | M | Require evidence links + review gate |
| Formula ambiguity | L | Keep formula string explicit |

## ✅ Acceptance Criteria
- [ ] Formula is present and explicit
- [ ] Evidence-link requirement present
- [ ] Run review references scoring artifact

## 🧪 Verification (≥3 commands)
```bash
rg -n "satisfaction_score_percent|formula" swarm_review/pilot_stand/006_epub/templates/SATISFACTION_SCORE_TEMPLATE.yaml
rg -n "stable_candidate" swarm_review/pilot_stand/006_epub/templates/SATISFACTION_SCORE_TEMPLATE.yaml
test -f swarm_review/pilot_stand/006_epub/templates/SATISFACTION_SCORE_TEMPLATE.yaml
```

## 🔄 Rollback
```bash
git revert HEAD
```

## 📝 Commit Message
```
feat(swarm_review): add pilot satisfaction scoring contract

Card: P1-05
Fixes: MA-02
```
