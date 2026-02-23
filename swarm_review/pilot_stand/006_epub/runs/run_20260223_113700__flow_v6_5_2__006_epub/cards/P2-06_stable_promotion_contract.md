# P2-06: Add Stable Promotion Contract

**Priority:** P2
**Complexity:** 1.5h
**Status:** Backlog

## 👤 User Story (Given/When/Then)
Given iterative flow versions
When run results reach threshold
Then stable promotion should be written by contract and traceable in registry.

## 💼 Business Impact
Creates deterministic promotion path to `Stable` and avoids ambiguous version status.

## 📋 Description
Add explicit stable promotion schema in pilot stand and reference it from run index.

## 🌍 Context
Stable criteria exist in markdown but no contract-level schema ties decision to scored evidence.

## ✅ Pre-Implementation Checklist
- [ ] Stable schema fields defined
- [ ] RUN_INDEX includes stable decision fields
- [ ] Registry row format updated

## 🔗 Linked Cards
| Card ID | Relationship | Direction |
|---------|-------------|-----------|
| P1-05 | blocked_by | ← this card |
| P0-01 | related | ↔ |

## 🔄 Sync Context
**Depends on state:** scoring artifacts are available  
**Produces state:** contract-backed stable declaration

## 📍 Location
File: `swarm_review/pilot_stand/006_epub/STABLE_REGISTRY.md`  
Lines: `3-14`

## 🔴 Current Code (ACTUAL — not placeholder)
```markdown
- Satisfaction >=95%
- Confidence >=95%
- No open P0 gaps
- All mandatory artifacts present
```

## 🟢 Fixed Code (copy-paste ready)
```markdown
- Satisfaction >=95%
- Confidence >=95%
- No open P0 gaps
- All mandatory artifacts present
- Signed run_id and flow_version evidence reference is mandatory
```

## 🧪 Test Code (complete, runnable)
```bash
#!/usr/bin/env bash
set -euo pipefail
rg -n "Satisfaction >=95%|Signed run_id" swarm_review/pilot_stand/006_epub/STABLE_REGISTRY.md
```

## ⚠️ Risk Assessment
| Risk | Level | Mitigation |
|------|-------|------------|
| Premature stable declaration | M | Require run evidence reference |
| Registry drift | L | Update with template-driven row |

## ✅ Acceptance Criteria
- [ ] Stable schema line added
- [ ] Registry row references run evidence path
- [ ] RUN_INDEX includes stability decision fields

## 🧪 Verification (≥3 commands)
```bash
rg -n "Stable Registry|Satisfaction >=95%" swarm_review/pilot_stand/006_epub/STABLE_REGISTRY.md
rg -n "runs:" swarm_review/pilot_stand/006_epub/RUN_INDEX.yaml
test -f swarm_review/pilot_stand/006_epub/STABLE_REGISTRY.md
```

## 🔄 Rollback
```bash
git revert HEAD
```

## 📝 Commit Message
```
feat(swarm_review): add stable promotion contract

Card: P2-06
Fixes: MA-04
```
