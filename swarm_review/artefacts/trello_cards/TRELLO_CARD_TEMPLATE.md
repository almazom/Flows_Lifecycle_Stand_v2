# 📋 TRELLO_CARD_TEMPLATE.md

```
╔═══════════════════════════════════════════════════════════════╗
║  Trello/Kanban Card — Standard Format                        ║
║  Every card must be implementable by a middle dev in 1-4h   ║
╚═══════════════════════════════════════════════════════════════╝
```

## Card Header

```
{PRIORITY}-{ID}: {Title}
Priority: P0 | P1 | P2
Complexity: {X}h (must be 1-4h)
Status: Backlog | In Progress | Done
```

---

## Card Body

```markdown
# {PRIORITY}-{ID}: {Title}

**Priority:** P0 | P1 | P2
**Complexity:** {X}h
**Status:** Backlog

---

## 👤 User Story (Given/When/Then)
Given {starting condition}
When {action/change happens}
Then {expected measurable outcome}

## 💼 Business Impact
{Why this change matters for users, delivery, risk, or cost. 1-3 sentences.}

## 📋 Description
{What needs to be done and why — 2-3 sentences max}

## 🌍 Context
{Background a middle developer needs to understand this card in 3 minutes.
Include: what system is affected, what problem this solves, any constraints.}

## ✅ Pre-Implementation Checklist
- [ ] Scope is clear and bounded to 1-4h
- [ ] Dependencies from linked cards are confirmed
- [ ] Affected files and tests are identified

## 🔗 Linked Cards
| Card ID | Relationship | Direction |
|---------|-------------|-----------|
| {ID} | blocks | → this card |
| {ID} | blocked_by | ← this card |
| {ID} | related | ↔ |

## 🔄 Sync Context
**Depends on state:** {What must be true before starting this card}
**Produces state:** {What will be true after completing this card}
**Parallel-safe:** yes | no | conditional ({condition})

## 📍 Location
File: `{path/to/file}`
Lines: `{start}-{end}`

## 🔴 Current Code (ACTUAL — not placeholder)
` ` `{language}
{real code copied from project — never use (...) or TODO}
` ` `

## 🟢 Fixed Code (copy-paste ready)
` ` `{language}
{complete working code — must run as-is}
` ` `

## 🧪 Test Code (complete, runnable)
` ` `{language}
{full test code, no placeholders}
` ` `

## ⚠️ Risk Assessment
| Risk | Level | Mitigation |
|------|-------|------------|
| {risk 1} | H/M/L | {how to mitigate} |
| {risk 2} | H/M/L | {how to mitigate} |

## ✅ Acceptance Criteria
- [ ] {Specific, testable criterion 1}
- [ ] {Specific, testable criterion 2}
- [ ] {Specific, testable criterion 3}

## 🧪 Verification (≥3 commands)
` ` `bash
{command 1 — must be runnable}
{command 2 — must be runnable}
{command 3 — must be runnable}
` ` `

## 🔄 Rollback
` ` `bash
git revert {commit_sha}
# or:
{specific undo steps}
` ` `

## 📝 Commit Message
` ` `
{type}({scope}): {description}

Card: {PRIORITY}-{ID}
Fixes: {finding_id from fusion report}
` ` `
```

---

## 15-Point Quality Scoring

| # | Criterion | Points | Check |
|---|-----------|--------|-------|
| 1 | User story (Given/When/Then) | 1 | Present |
| 2 | Business impact (why it matters) | 1 | Present |
| 3 | File:line exact location | 1 | Present |
| 4 | Current code — ACTUAL code | 2 | No placeholders |
| 5 | Fixed code — copy-paste ready | 2 | Runs as-is |
| 6 | Risk assessment table | 1 | Has mitigation |
| 7 | Pre-impl checklist | 1 | Actionable steps |
| 8 | Tests — complete code | 2 | Runnable |
| 9 | Verification (≥3 commands) | 1 | Runnable |
| 10 | Acceptance criteria | 1 | Checkboxes |
| 11 | Rollback plan | 1 | Working command |
| 12 | Commit message template | 1 | Filled |

**Pass threshold: ≥13/15 (87%)**

## Required Sections for Scoring

All sections below are mandatory for scoring and FCT review:

- `## 👤 User Story (Given/When/Then)`
- `## 💼 Business Impact`
- `## ✅ Pre-Implementation Checklist`
- `## 🧪 Test Code (complete, runnable)`
- `## 🔗 Linked Cards`
- `## 🔄 Sync Context`

---

## FCT Review Axes

Each card is reviewed on 3 dimensions:

| Axis | Question | Target |
|------|----------|--------|
| **Completeness** | Does the card contain all info needed? | 95%+ |
| **Integrity** | Is the card internally consistent (no contradictions)? | 95%+ |
| **Quality** | Can a middle dev understand it in 3 minutes? | 95%+ |

---

## ❌ FORBIDDEN in Cards

```yaml
forbidden:
  - "Consider..."
  - "Maybe..."
  - "If applicable..."
  - "{placeholder}"
  - "TODO"
  - "TBD"
  - "..." to skip code
  - empty sections
  - links to non-existent cards
```

---

## Kanban States

```yaml
states:
  backlog:
    description: "Card created, not yet started"
    next: in_progress

  in_progress:
    description: "Worker actively implementing"
    next: done

  done:
    description: "Implemented, verified, committed"
    final: true
```

---

*swarm_review/artefacts/trello_cards/TRELLO_CARD_TEMPLATE.md*
