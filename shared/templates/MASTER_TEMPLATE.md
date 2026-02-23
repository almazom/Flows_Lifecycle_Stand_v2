# 📴 MASTER_TEMPLATE.md

## 15-Point Card Quality

| Criterion | Points | Check |
|-----------|--------|-------|
| User story | 1 | Given/When/Then |
| Business impact | 1 | Why matters |
| File:line | 1 | Exact location |
| Current code | 2 | ACTUAL code |
| Fixed code | 2 | Copy-paste ready |
| Risk | 1 | Table |
| Pre-impl | 1 | Checklist |
| Tests | 2 | Complete code |
| Verify (3+) | 1 | Commands |
| Acceptance | 1 | Criteria |
| Rollback | 1 | Plan |
| Commit | 1 | Template |

**Pass: ≥13/15**

---

## Card Structure

```markdown
# {PRIORITY}-{ID}: {Title}

## 👤 User Story (Given/When/Then)
Given {condition}
When {action}
Then {outcome}

## 💼 Business Impact
{why this card matters}

## ✅ Pre-Implementation Checklist
- [ ] Scope is bounded to 1-4h
- [ ] Dependencies confirmed
- [ ] Affected files/tests identified

## 📍 Location
File: {path}:{line}

## 🔴 Current Code
` `{lang}
{actual code from project}
` `

## 🟢 Fixed Code
` `{lang}
{copy-paste ready code}
` `

## 🧪 Test Code
` `{lang}
{complete runnable tests}
` `

## 🔗 Linked Cards
| Card ID | Relationship | Direction |
|---------|-------------|-----------|
| {ID} | blocks | → this card |
| {ID} | related | ↔ |

## 🔄 Sync Context
**Depends on:** {what must be true before starting}
**Produces:** {what will be true after completing}

## ⚠️ Risk
| Risk | Level | Mitigation |
|------|-------|------------|
| {risk} | H/M/L | {how} |

## ✅ Acceptance
- [ ] {criterion 1}
- [ ] {criterion 2}
- [ ] {criterion 3}

## 🧪 Verify
` `bash
{command 1}
{command 2}
{command 3}
` `

## 🔄 Rollback
` `bash
git revert {sha}
` `

## 📝 Commit
` `
{type}({scope}): {desc}
Card: {ID}
` `
```

---

## ❌ FORBIDDEN

- "Consider..."
- "Maybe..."
- TODO, TBD, {...}
- "..." to skip code
- missing required sections for scoring
