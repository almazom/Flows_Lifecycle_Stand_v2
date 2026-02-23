# 🛡️ pr_review_mode.md

## What

Explicit PR review policy for Phase 9. Supports two modes:
- `auto` (system performs automated review before terminal report)
- `human` (handoff to user; system does not claim final PR review)

## Artifacts

```text
reports/execution/reviews/phase_9a_pr_review.yaml   # required in auto mode
reports/execution/reviews/phase_9_final_review.yaml # always required
```

## Contract

```yaml
pr_review_mode:
  source: shared/config.yaml:pr_review.mode
  allowed_values: [auto, human]

auto_mode:
  requires:
    - checks_executed
    - reviewer_quorum_min_3
    - pr_ready_status_pass
  output:
    phase_9a_pr_review.status: pass
    phase_9a_pr_review.decision: PR_READY

human_mode:
  requires:
    - explicit_handoff_attestation
  forbids:
    - system_claim_final_pr_review
  output:
    phase_9a_pr_review.status: not_applicable_by_policy
    phase_9a_pr_review.decision: HUMAN_REVIEW_REQUIRED
```

## Pass

- Mode is explicit and evidence-backed
- Phase 9 final report matches selected mode
- No false claim of final review in human mode

## Fail

- Missing mode or ambiguous policy
- Claiming PR-ready without auto checks
- Claiming final PR review in human mode
