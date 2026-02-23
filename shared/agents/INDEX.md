# 🤖 agents/INDEX.md — Subagent Library

```
╔═══════════════════════════════════════════════════════════════╗
║  READ THIS FILE BEFORE SPAWNING ANY SUBAGENT                 ║
╚═══════════════════════════════════════════════════════════════╝
```

## Available Agents

| Agent | Binary | Best For |
|-------|--------|----------|
| Kimi | `kimi` | Long context, large file analysis |
| Qwen | `qwen` | Fast coding, structured output |
| Codex | `codex` | Code execution, implementation |
| Gemini | `gemini` | Multimodal, video/image input |
| Pi | `pi` | Reasoning, planning |
| GLM5 | `glm5` | General, Chinese-language support |

## Selection Protocol

```
1️⃣ READ this INDEX.md
2️⃣ CHECK availability: which kimi / which qwen / which codex
3️⃣ SELECT based on caste (see table below)
4️⃣ SPAWN with full context pack
5️⃣ LOG to bio/spawn_registry.yaml
```

## Caste → Preferred Agent

| Caste | Preferred | Fallback |
|-------|-----------|----------|
| scout | kimi, gemini | qwen, codex |
| masticator | kimi | qwen |
| comb_builder | qwen, codex | gemini |
| nurse | kimi, qwen | codex |
| worker | codex, qwen | pi |

## Context Pack Template

```yaml
SUBAGENT: true
TASK_ID: "{flow}_{phase}_{role}_{timestamp}"
PHASE: "{phase_number}"
BIO_CASTE: "scout|masticator|comb_builder|nurse|worker"
ROLE: "{specific role, e.g. security}"
GOAL: "{exact goal — one sentence}"
INPUT_ARTIFACTS:
  - "{path/to/input1}"
  - "{path/to/input2}"
CONSTRAINTS: "non-stop | md-only | no-fabrication | no-placeholders"
OUTPUT_ARTIFACTS:
  - "{path/to/expected/output}"
OUTPUT: "summary | changed_files | risks"
```

## Topology Rules

```yaml
strict_parallel:
  requires_distinct_real_producers: ">=3"
  if_below_3: classify_as strategy_variations

strategy_variations:
  allowed: true
  must_attest: "strategy_variations (not strict_parallel)"
  forbidden_wording:
    - "three-way quorum passed"
    - "3 distinct producers confirmed"
```

## Quorum Decision Points (5 mandatory)

Spawn ≥3 agents at each of these gates:

| Point | Phase | Question |
|-------|-------|----------|
| preflight_decision | 0 | Is environment ready? |
| fusion_decision | 3 | Is P0/P1/P2 prioritization correct? |
| quality_95_validation | 5 | Do cards meet 95% confidence? |
| implementation_decision | 8 | Are all cards implemented? |
| final_readiness_decision | 9 | Is terminal state valid? |

## Input Types Supported

| Type | Agent | Notes |
|------|-------|-------|
| Code files | any | Primary use case |
| Markdown docs | any | Full support |
| YAML/JSON | any | Full support |
| Video files | gemini | Multimodal only |
| Large files (>100KB) | kimi, gemini | Long-context models |

## Fallback Policy

```yaml
tier_1: [kimi, qwen, codex]
tier_2: [gemini, pi, glm5]

if_less_than_3_available:
  - use: strategy_variations
  - never_claim: strict_parallel
  - attest: "strategy_variations due to limited agent availability"
```

---

*shared/agents/INDEX.md*
