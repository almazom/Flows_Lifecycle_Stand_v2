# P1-03: Add CI Manual-Test Safety Gate

**Priority:** P1
**Complexity:** 2.0h
**Status:** Backlog

## 👤 User Story (Given/When/Then)
Given CI and test findings can include destructive/manual paths
When fusion creates implementation priorities
Then flow should add a dedicated gate to prevent unsafe CI recommendations.

## 💼 Business Impact
Avoids introducing harmful CI changes and improves reliability of recommendations.

## 📋 Description
Introduce `ci_test_safety_gate` with checks for `manual` markers, destructive fixtures, and mutable env writes.

## 🌍 Context
Pilot findings show unsafe tests can be selected by default CI command patterns.

## ✅ Pre-Implementation Checklist
- [ ] Gate defined in preflight/quality
- [ ] Required signals listed
- [ ] Artifact file path specified

## 🔗 Linked Cards
| Card ID | Relationship | Direction |
|---------|-------------|-----------|
| P1-05 | related | ↔ |
| P0-01 | blocked_by | ← this card |

## 🔄 Sync Context
**Depends on state:** fusion already labels test/CI findings  
**Produces state:** guardrail for safe CI-related recommendations

## 📍 Location
File: `swarm_review/v6.5.2/START.md`  
Lines: `150-159`

## 🔴 Current Code (ACTUAL — not placeholder)
```markdown
**Gates:**
- `environment_gate` — write permissions, target project exists, shared resources available
- `flow_version_lock_gate` — active START = v6.5.2, symlink valid
- `mode_executability_gate` — detect agents, resolve mode, deny impossible claims
```

## 🟢 Fixed Code (copy-paste ready)
```markdown
**Gates:**
- `environment_gate` — write permissions, target project exists, shared resources available
- `flow_version_lock_gate` — active START = v6.5.3, symlink valid
- `mode_executability_gate` — detect agents, resolve mode, deny impossible claims
- `ci_test_safety_gate` — detect destructive/manual test leakage into default CI recommendations
```

## 🧪 Test Code (complete, runnable)
```bash
#!/usr/bin/env bash
set -euo pipefail
rg -n "xfail|manual|destructive|.env" /home/pets/zoo/006_epub/tests /home/pets/zoo/006_epub/.github/workflows
```

## ⚠️ Risk Assessment
| Risk | Level | Mitigation |
|------|-------|------------|
| Gate complexity creep | L | Keep focused on CI safety signals |
| False blocks | M | Add clear override protocol |

## ✅ Acceptance Criteria
- [ ] Gate appears in phase-0 contract
- [ ] Output artifact produced in preflight
- [ ] At least one finding is reclassified through gate logic

## 🧪 Verification (≥3 commands)
```bash
rg -n "ci_test_safety_gate" swarm_review/v6.5.3/START.md
test -f swarm_review/v6.5.3/START.md
rg -n "manual" /home/pets/zoo/006_epub/tests/integration/test_manual_fallback.py
```

## 🔄 Rollback
```bash
git revert HEAD
```

## 📝 Commit Message
```
feat(swarm_review): add ci manual-test safety gate

Card: P1-03
Fixes: TS-01
```
