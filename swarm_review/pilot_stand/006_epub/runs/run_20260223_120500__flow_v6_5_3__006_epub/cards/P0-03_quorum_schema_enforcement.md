# P0-03: quorum_schema_enforcement

**Priority:** P0-03
**Complexity:** 2h
**Status:** Backlog

## 👤 User Story (Given/When/Then)
Given run evidence can drift from hard contracts
When phase gates evaluate status
Then gate must fail deterministically on invariant violations.

## 💼 Business Impact
Directly improves stability confidence and prevents false-pass terminal states.

## 📋 Description
Implement contract hardening for this residual gap.

## 🌍 Context
Residual gaps from run #1 prevent stable promotion >=95.

## ✅ Pre-Implementation Checklist
- [ ] Contract section updated
- [ ] Artifact schema updated
- [ ] Verification commands defined

## 🔗 Linked Cards
| Card ID | Relationship | Direction |
|---------|-------------|-----------|
| P0-01 | related | ↔ |
| P1-05 | related | ↔ |

## 🔄 Sync Context
**Depends on state:** run artifacts exist  
**Produces state:** stronger gate determinism

## 📍 Location
File: 
`shared/guards/quorum.md`:39-56

## 🔴 Current Code (ACTUAL — not placeholder)

yaml
required_artifact_fields:\n  quorum_decision_record:\n    - phase_id\n    - decision_question

## 🟢 Fixed Code (copy-paste ready)

yaml
required_artifact_fields:\n  quorum_decision_record:\n    - phase_id\n    - decision_question\n    - input_artifacts\n    - spawned_agents\n    - agent_outputs\n    - consolidated_verdict\n    - confidence_percent\n    - quorum_met

## 🧪 Test Code (complete, runnable)

bash
set -euo pipefail
rg -n "quorum_met|spawned_agents|agent_outputs" shared/guards/quorum.md

## ⚠️ Risk Assessment
| Risk | Level | Mitigation |
|------|-------|------------|
| Over-blocking | M | Explicit override path with evidence |
| Under-detection | M | Add schema checks and tests |

## ✅ Acceptance Criteria
- [ ] Gate fails when invariant fails
- [ ] Evidence schema is complete
- [ ] Final review consumes new fields

## 🧪 Verification (≥3 commands)

bash
rg -n "quorum_met|spawned_agents|agent_outputs" shared/guards/quorum.md
test -f shared/guards/quorum.md
rg -n "quorum_decision_record" swarm_review/pilot_stand/006_epub/runs

## 🔄 Rollback

bash
git revert HEAD

## 📝 Commit Message

feat(swarm_review): quorum_schema_enforcement

Card: P0-03

