# P1-06: ssot_card_status_sync_contract

**Priority:** P1-06
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
`swarm_review/v6.5.3/START.md`:375-379

## 🔴 Current Code (ACTUAL — not placeholder)

yaml
- Update SSOT_KANBAN.json card status as each card completes

## 🟢 Fixed Code (copy-paste ready)

yaml
- Update SSOT_KANBAN.json card status as each card completes\n- Sync generated card markdown status with SSOT at Phase 8 close

## 🧪 Test Code (complete, runnable)

bash
set -euo pipefail
rg -n "Sync generated card markdown status" swarm_review/v6.5.4/START.md

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
rg -n "Sync generated card markdown status" swarm_review/v6.5.4/START.md
test -f swarm_review/v6.5.4/START.md
rg -n "Status: Backlog|"status": "done"" swarm_review/pilot_stand/006_epub/runs/run_20260223_113700__flow_v6_5_2__006_epub/cards swarm_review/pilot_stand/006_epub/runs/run_20260223_113700__flow_v6_5_2__006_epub/ssot/SSOT_KANBAN.json

## 🔄 Rollback

bash
git revert HEAD

## 📝 Commit Message

feat(swarm_review): ssot_card_status_sync_contract

Card: P1-06

