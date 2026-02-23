# P0-01: hard_fail_step_coverage_on_missing_phases

**Priority:** P0-01
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
`shared/guards/step_coverage.md`:21-29

## 🔴 Current Code (ACTUAL — not placeholder)

yaml
rules:\n  no_phase_with_missing_status: true

## 🟢 Fixed Code (copy-paste ready)

yaml
rules:\n  no_phase_with_missing_status: true\n  fail_when_all_required_phases_present_false: true

## 🧪 Test Code (complete, runnable)

bash
set -euo pipefail
rg -n "fail_when_all_required_phases_present_false" shared/guards/step_coverage.md

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
rg -n "fail_when_all_required_phases_present_false" shared/guards/step_coverage.md
test -f shared/guards/step_coverage.md
rg -n "all_required_phases_present" swarm_review/pilot_stand/006_epub/runs

## 🔄 Rollback

bash
git revert HEAD

## 📝 Commit Message

feat(swarm_review): hard_fail_step_coverage_on_missing_phases

Card: P0-01

