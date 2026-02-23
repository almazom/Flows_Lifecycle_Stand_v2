# 🐜 Flows Lifecycle Stand v2

```
╔═══════════════════════════════════════════════════════════════╗
║                                                               ║
║   FLOWS LIFECYCLE STAND v2                                   ║
║                                                               ║
║   Multi-flow • Versioned • Biological                        ║
║                                                               ║
╚═══════════════════════════════════════════════════════════════╝
```

## 🚀 Quick Start

```
1️⃣ Read this file
2️⃣ Go to your flow folder (swarm_review/, feature_sdd/, etc.)
3️⃣ Read {flow}/current/START.md
4️⃣ Execute
```

---

## 📁 Structure

```
Flows_Lifecycle_Stand_v2/
│
├── START.md              ← You are here
├── AGENTS.md             ← All agents read this
├── CLAUDE.md             ← Claude-specific
├── GEMINI.md             ← Gemini-specific
├── COPILOT.md            ← Copilot-specific
├── QWEN.md               ← Qwen-specific
│
├── shared/               ← Common across ALL flows
│   ├── EXPECTATIONS.md
│   ├── config.yaml
│   ├── guards/
│   ├── templates/
│   └── colony_memory/
│
├── swarm_review/         ← Flow 1: 6-agent code review
│   ├── current → v6.5.5/  ← Symlink to latest
│   ├── v6.5/
│   ├── v6.5.1/
│   ├── v6.5.2/
│   ├── v6.5.3/
│   ├── v6.5.4/
│   ├── v6.5.5/
│   ├── v6.5.6/           ← Draft: PR-review policy split (not current)
│   └── pilot_stand/       ← Pilot evolution bench (006_epub)
│
├── feature_sdd/          ← Flow 2: Feature development (FUTURE)
│   └── current → v1.0/
│
└── bug_arc/              ← Flow 3: Bug fixing (FUTURE)
    └── current → v1.0/
```

---

## 🐜 Available Flows

| Flow | Purpose | Current Version |
|------|---------|-----------------|
| **swarm_review** | 6-agent code review, fusion, cards, implementation | v6.5.5 |
| feature_sdd | Feature development (FUTURE) | - |
| bug_arc | Bug analysis & fixing (FUTURE) | - |

---

## 🔄 Versioning

```
Each flow has versions:
  swarm_review/
  ├── current → v6.5.5/    ← Always points to latest
  ├── v6.5.4/              ← Previous patch
  └── v6.5.5/              ← Current patch

Version format: MAJOR.MINOR.PATCH
  MAJOR = Breaking changes
  MINOR = New features
  PATCH = Bug fixes
```

---

## 📦 Shared Resources

All flows use `shared/`:

```
shared/
├── EXPECTATIONS.md       ← 22 locked rules
├── config.yaml           ← Thresholds
├── guards/               ← Execution contracts
├── templates/            ← Card templates
└── colony_memory/        ← Persistent learning
```

---

## 🚀 Start a Flow

```bash
# Go to flow
cd swarm_review/current/

# Read START.md
cat START.md

# Execute
```

---

## 🔧 Adding New Flow

```
1. Create folder: mkdir {flow_name}/
2. Create version: mkdir {flow_name}/v1.0/
3. Create START.md in version folder
4. Create symlink: ln -s v1.0 current
5. Use shared/ resources
```

---

## 🛡️ Harness Engineering (from OpenAI)

Our biological layer implements harness engineering:

| Harness Concept | Our Implementation |
|-----------------|-------------------|
| Guardrails | guards/*.md |
| Test harnesses | Template quality scoring |
| Evaluation | 15-point quality system |
| Iteration | Pheromone decay, colony memory |
| Validation gates | Quorum decisions |

---

**NEXT: Go to `swarm_review/current/START.md`**

*v2 — 2026-02-23*
