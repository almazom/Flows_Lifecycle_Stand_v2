# 🤖 AGENTS.md — All AI Agents Read This

```
╔═══════════════════════════════════════════════════════════════╗
║  ALL AI AGENTS READ THIS FILE                                ║
╚═══════════════════════════════════════════════════════════════╝
```

## 📁 How to Navigate

```
1. Read root START.md
2. Read this file (AGENTS.md)
3. Read your agent file (CLAUDE.md, QWEN.md, etc.)
4. Read shared/EXPECTATIONS.md
5. Go to {flow}/current/START.md
6. Execute
```

---

## 🐜 Biological Model

You are part of a **colony** coordinating through:

| Mechanism | File | What |
|-----------|------|------|
| Stigmergy | shared/guards/stigmergy.md | Coordinate via artifacts |
| Quorum | shared/guards/quorum.md | 2/3 consensus |
| Pheromone | shared/guards/pheromone.md | Priority decay |
| Memory | shared/colony_memory/ | Learn between runs |

---

## 🎭 Castes

| Caste | Job | Phase |
|-------|-----|-------|
| scout | Find issues | 2 |
| masticator | Synthesize P0/P1/P2 | 3 |
| comb_builder | Create cards | 4 |
| nurse | Quality 95% | 5 |
| worker | Implement code | 8 |

---

## 📋 Core Rules

```yaml
NEVER_STOP: true       # Continue until terminal
MD_ONLY: true          # No shell scripts
NO_FABRICATION: true   # Don't fake evidence
AUTO_COMMIT: true      # Git after each phase
```

---

## 📂 Shared Resources

```
shared/
├── EXPECTATIONS.md    ← 22 rules (read this!)
├── config.yaml        ← Thresholds
├── guards/            ← Execution contracts
├── templates/         ← Card quality
└── colony_memory/     ← Learning
```

---

## ✅ Quality Standards

- Cards ≥13/15 points
- Confidence ≥95%
- 3-minute comprehension
- No placeholders

---

*AGENTS.md*
