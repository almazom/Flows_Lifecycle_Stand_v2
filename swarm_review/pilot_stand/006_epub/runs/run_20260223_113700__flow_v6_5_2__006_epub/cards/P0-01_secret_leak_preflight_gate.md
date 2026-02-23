# P0-01: Add Secret Leak Preflight Gate

**Priority:** P0
**Complexity:** 2.5h
**Status:** Backlog

## 👤 User Story (Given/When/Then)
Given pilot runs use real repositories with local `.env` files
When preflight starts
Then run must detect plaintext secrets and block unsafe execution/reporting.

## 💼 Business Impact
Prevents accidental token leakage in artifacts and logs, reducing operational and security risk during repeated flow experiments.

## 📋 Description
Extend preflight with `secret_leak_gate` and require explicit redaction signal before continuing.

## 🌍 Context
Current contracts validate evidence integrity but do not explicitly gate plaintext secrets in input repos.

## ✅ Pre-Implementation Checklist
- [ ] Gate path defined in Phase 0 preflight section
- [ ] Redaction/block behavior documented
- [ ] Gate output artifact path added

## 🔗 Linked Cards
| Card ID | Relationship | Direction |
|---------|-------------|-----------|
| P0-02 | related | ↔ |
| P1-03 | blocks | → this card |

## 🔄 Sync Context
**Depends on state:** preflight gates are configurable in `START.md`  
**Produces state:** secret-safe preflight contract and report

## 📍 Location
File: `shared/guards/evidence_integrity.md`  
Lines: `24-33`

## 🔴 Current Code (ACTUAL — not placeholder)
```yaml
hard_rules:
  - no_claim_without_artifact: true
  - no_distinct_producer_claim_without_distinct_engine_session_pairs: true
  - no_simulated_pr_claim_without_pr_url: true
```

## 🟢 Fixed Code (copy-paste ready)
```yaml
hard_rules:
  - no_claim_without_artifact: true
  - no_distinct_producer_claim_without_distinct_engine_session_pairs: true
  - no_simulated_pr_claim_without_pr_url: true
  - no_plaintext_secret_in_run_artifacts: true

preflight_secret_gate:
  required: true
  block_on_detected_plaintext_secret: true
```

## 🧪 Test Code (complete, runnable)
```bash
#!/usr/bin/env bash
set -euo pipefail
rg -n "no_plaintext_secret_in_run_artifacts|preflight_secret_gate" shared/guards/evidence_integrity.md
```

## ⚠️ Risk Assessment
| Risk | Level | Mitigation |
|------|-------|------------|
| False positives on sample tokens | M | Allow whitelist patterns for placeholders |
| Missed secret patterns | M | Add detector list + iterative updates |

## ✅ Acceptance Criteria
- [ ] `secret_leak_gate` documented in guard
- [ ] Preflight artifact includes gate result
- [ ] Blocking behavior is explicit

## 🧪 Verification (≥3 commands)
```bash
rg -n "secret_leak_gate" swarm_review/v6.5.3/START.md
rg -n "no_plaintext_secret_in_run_artifacts" shared/guards/evidence_integrity.md
test -f shared/guards/evidence_integrity.md
```

## 🔄 Rollback
```bash
git revert HEAD
```

## 📝 Commit Message
```
feat(swarm_review): add secret leak preflight gate

Card: P0-01
Fixes: SE-01
```
