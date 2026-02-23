# P1-05: requirements_backlog_traceability_contract

**Priority:** P1-05
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
`swarm_review/v6.5.3/START.md`:380-384

## 🔴 Current Code (ACTUAL — not placeholder)

yaml
**Artifacts:**\n- `reports/execution/requirements_traceability.yaml`

## 🟢 Fixed Code (copy-paste ready)

yaml
**Artifacts:**\n- `reports/execution/requirements_traceability.yaml`\n- `reports/execution/requirements_backlog_traceability.yaml`

## 🧪 Test Code (complete, runnable)

bash
set -euo pipefail
rg -n "requirements_backlog_traceability" swarm_review/v6.5.4/START.md

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
rg -n "requirements_backlog_traceability" swarm_review/v6.5.4/START.md
test -f swarm_review/v6.5.4/START.md
rg -n "requirements_traceability" swarm_review/pilot_stand/006_epub/runs

## 🔄 Rollback

bash
git revert HEAD

## 📝 Commit Message

feat(swarm_review): requirements_backlog_traceability_contract

Card: P1-05

