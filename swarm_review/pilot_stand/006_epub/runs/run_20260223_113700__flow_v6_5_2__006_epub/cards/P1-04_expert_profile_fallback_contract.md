# P1-04: Add Expert Profile Fallback Contract

**Priority:** P1
**Complexity:** 1.5h
**Status:** Backlog

## 👤 User Story (Given/When/Then)
Given some agent profiles can be unavailable in runtime
When phase 2 starts
Then flow must fallback to supported profiles without breaking six-expert dispatch.

## 💼 Business Impact
Prevents run aborts due to profile-specific sandbox issues and keeps non-stop lifecycle intact.

## 📋 Description
Add `agent_profile_fallback` policy to mode executability and spawn registry requirements.

## 🌍 Context
Pilot showed `explorer` profile can fail with sandbox network-namespace error while `default/worker` works.

## ✅ Pre-Implementation Checklist
- [ ] Fallback order defined
- [ ] Attestation field added
- [ ] Strict/non-strict claim wording bounded

## 🔗 Linked Cards
| Card ID | Relationship | Direction |
|---------|-------------|-----------|
| P0-02 | blocked_by | ← this card |
| P1-05 | related | ↔ |

## 🔄 Sync Context
**Depends on state:** mode executability contract exists  
**Produces state:** resilient expert dispatch policy

## 📍 Location
File: `shared/guards/mode_executability.md`  
Lines: `50-55`

## 🔴 Current Code (ACTUAL — not placeholder)
```yaml
preflight_check:
  - detect: available_agents
  - detect: git_access
  - detect: write_permissions
  - resolve: mode (analysis_only | implementation)
  - deny: impossible_claims_upfront
```

## 🟢 Fixed Code (copy-paste ready)
```yaml
preflight_check:
  - detect: available_agents
  - detect: agent_profile_health
  - detect: git_access
  - detect: write_permissions
  - resolve: mode (analysis_only | implementation)
  - resolve: expert_profile_fallback_order [explorer, default, worker]
  - deny: impossible_claims_upfront
```

## 🧪 Test Code (complete, runnable)
```bash
#!/usr/bin/env bash
set -euo pipefail
rg -n "agent_profile_fallback|agent_profile_health" shared/guards/mode_executability.md
```

## ⚠️ Risk Assessment
| Risk | Level | Mitigation |
|------|-------|------------|
| Hidden degradation of expert quality | M | Log fallback and reflect in confidence |
| Incorrect strict_parallel claim | M | Topology guard controls wording |

## ✅ Acceptance Criteria
- [ ] Fallback policy documented
- [ ] Spawn registry captures selected profile per expert
- [ ] Final report reflects fallback usage

## 🧪 Verification (≥3 commands)
```bash
rg -n "fallback" shared/guards/mode_executability.md
rg -n "SUBAGENT" shared/guards/spawn_registry.md
test -f shared/guards/mode_executability.md
```

## 🔄 Rollback
```bash
git revert HEAD
```

## 📝 Commit Message
```
feat(swarm_review): add expert profile fallback contract

Card: P1-04
Fixes: AR-03
```
