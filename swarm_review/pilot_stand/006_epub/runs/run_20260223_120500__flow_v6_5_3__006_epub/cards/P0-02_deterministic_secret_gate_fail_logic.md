# P0-02: deterministic_secret_gate_fail_logic

**Priority:** P0-02
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
`shared/guards/evidence_integrity.md`:32-36

## 🔴 Current Code (ACTUAL — not placeholder)

yaml
preflight_secret_gate:\n  required: true\n  block_on_detected_plaintext_secret: true

## 🟢 Fixed Code (copy-paste ready)

yaml
preflight_secret_gate:\n  required: true\n  block_on_detected_plaintext_secret: true\n  fail_if_detected_plaintext_secret_files_non_empty: true

## 🧪 Test Code (complete, runnable)

bash
set -euo pipefail
rg -n "fail_if_detected_plaintext_secret_files_non_empty" shared/guards/evidence_integrity.md

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
rg -n "fail_if_detected_plaintext_secret_files_non_empty" shared/guards/evidence_integrity.md
test -f shared/guards/evidence_integrity.md
rg -n "detected_plaintext_secret_files" swarm_review/pilot_stand/006_epub/runs

## 🔄 Rollback

bash
git revert HEAD

## 📝 Commit Message

feat(swarm_review): deterministic_secret_gate_fail_logic

Card: P0-02

