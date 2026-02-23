# P0-02: Add Async Blocking Detector Guard

**Priority:** P0
**Complexity:** 3.0h
**Status:** Backlog

## 👤 User Story (Given/When/Then)
Given async-heavy target projects
When scouts analyze code
Then flow should explicitly detect blocking subprocess patterns in async paths.

## 💼 Business Impact
Reduces blind spots for event-loop stalls that can break production bot responsiveness.

## 📋 Description
Add guard+phase check for `subprocess.run` used in async pathways and raise finding severity floor to P0/P1.

## 🌍 Context
Pilot project exposed blocking subprocess issues in summarization and vision async paths.

## ✅ Pre-Implementation Checklist
- [ ] Detection rule defined
- [ ] Evidence format standardized (`file:line`)
- [ ] Rule linked to fusion priority policy

## 🔗 Linked Cards
| Card ID | Relationship | Direction |
|---------|-------------|-----------|
| P0-01 | related | ↔ |
| P1-04 | blocks | → this card |

## 🔄 Sync Context
**Depends on state:** scouts already collect file:line evidence  
**Produces state:** explicit async-blocking detection in guard/contracts

## 📍 Location
File: `swarm_review/v6.5.2/START.md`  
Lines: `191-197`

## 🔴 Current Code (ACTUAL — not placeholder)
```markdown
- Reports must include file:line evidence (no fabricated evidence)
- Dispatch all 6 selected experts within one bounded dispatch window and record timestamp evidence
```

## 🟢 Fixed Code (copy-paste ready)
```markdown
- Reports must include file:line evidence (no fabricated evidence)
- Detect blocking async anti-patterns (`subprocess.run` in async call-paths, sync file I/O in hot async handlers)
- Dispatch all 6 selected experts within one bounded dispatch window and record timestamp evidence
```

## 🧪 Test Code (complete, runnable)
```bash
#!/usr/bin/env bash
set -euo pipefail
rg -n "subprocess\.run|async" pilot_projects/006_epub/core pilot_projects/006_epub/bot | head -n 50
```

## ⚠️ Risk Assessment
| Risk | Level | Mitigation |
|------|-------|------------|
| Over-reporting low-impact sync calls | M | Scope to async call-path context |
| Rule too generic | M | Keep examples in guard |

## ✅ Acceptance Criteria
- [ ] Async blocking rule present in flow contract
- [ ] At least one pilot run detects and prioritizes this class
- [ ] Fusion mapping references the rule

## 🧪 Verification (≥3 commands)
```bash
rg -n "blocking async anti-patterns|subprocess.run" swarm_review/v6.5.3/START.md
rg -n "async" shared/guards/evidence_integrity.md
test -f swarm_review/v6.5.3/START.md
```

## 🔄 Rollback
```bash
git revert HEAD
```

## 📝 Commit Message
```
feat(swarm_review): detect async blocking anti-patterns

Card: P0-02
Fixes: PE-01
```
