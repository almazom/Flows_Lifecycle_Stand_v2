# P1-04: auto_commit_sha_validation

**Priority:** P1-04
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
`shared/guards/auto_commit.md`:18-29

## 🔴 Current Code (ACTUAL — not placeholder)

yaml
phase_complete:\n  action:\n    - check: git status --porcelain

## 🟢 Fixed Code (copy-paste ready)

yaml
phase_complete:\n  action:\n    - check: git status --porcelain\n    - validate: commit_sha_regex ^[0-9a-f]{7,40}$\n    - block_if: commit_sha_pending

## 🧪 Test Code (complete, runnable)

bash
set -euo pipefail
rg -n "commit_sha_regex|commit_sha_pending" shared/guards/auto_commit.md

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
rg -n "commit_sha_regex|commit_sha_pending" shared/guards/auto_commit.md
test -f shared/guards/auto_commit.md
rg -n "pending" swarm_review/pilot_stand/006_epub/runs

## 🔄 Rollback

bash
git revert HEAD

## 📝 Commit Message

feat(swarm_review): auto_commit_sha_validation

Card: P1-04

