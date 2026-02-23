# 🛡️ pr_review_mode.md

## What

Explicit PR review policy for Phase 9.
Default target is `auto` with 3 reviewer agents and quorum 2/3.
Fallback `human` mode is allowed for manual handoff.

## Artifacts

```text
reports/execution/pr_auto_review_report.yaml
reports/execution/reviews/phase_9_pr_review.yaml    # phase 9a review decision
reports/execution/reviews/phase_9_final_review.yaml # always required
```

## Contract

```yaml
pr_review_mode:
  source: shared/config.yaml:pr_review.mode
  allowed_values: [auto, human]

auto_mode:
  reviewers: [security, logic, style]
  quorum:
    min_agents: 3
    pass_threshold: 0.67
  requires:
    - checks_executed
    - no_new_critical_or_high_security_findings
    - tests_and_regression_checks_pass
    - lint_and_style_checks_pass
  output:
    pr_auto_review_report.status: APPROVED | NEEDS_FIX | REJECTED
    phase_9_pr_review.status: pass | fail
    phase_9_pr_review.decision: PR_APPROVED | PR_NEEDS_FIX | PR_REJECTED
  transitions:
    APPROVED: phase_9b_terminal
    NEEDS_FIX: phase_8_workers
    REJECTED: blocked

human_mode:
  requires:
    - explicit_handoff_attestation
  forbids:
    - system_claim_final_pr_review
  output:
    phase_9_pr_review.status: not_applicable_by_policy
    phase_9_pr_review.decision: HUMAN_REVIEW_REQUIRED
```

## Pass

- Mode is explicit and evidence-backed
- `auto` mode includes 3 reviewer roles with quorum 2/3
- `auto` mode produces both PR review artifacts
- Phase 9 final report matches selected mode and decision
- No false claim of final review in human mode

## Fail

- Missing mode or ambiguous policy
- Claiming PR approval without auto checks and quorum
- Claiming final PR review in human mode
