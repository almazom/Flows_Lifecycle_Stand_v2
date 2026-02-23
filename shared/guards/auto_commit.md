# 🛡️ auto_commit.md

## What

Git commit after every phase AND after every file creation/change. No uncommitted files — ever.

## Artifact

`bio/commit_log.yaml`

## Contract

```yaml
triggers:
  file_created:
    action:
      - git add {file}
      - git commit -m "feat: create {file}"
      - log: bio/commit_log.yaml

  file_updated:
    action:
      - git add {file}
      - git commit -m "fix: update {file}"
      - log: bio/commit_log.yaml

  phase_complete:
    action:
      - check: git status --porcelain
      - if_changes:
          - git add .
          - git commit -m "Phase {N}: {description}"
      - validate: commit_sha_regex ^[0-9a-f]{7,40}$
      - block_if: commit_sha_pending
      - block_if: non_canonical_phase_id
      - log: bio/commit_log.yaml

phase_messages:
  0: "Phase 0: Preflight ✓"
  1: "Phase 1: Bootstrap ✓"
  2: "Phase 2: 6 scouts ✓"
  3: "Phase 3: Fusion ✓"
  4a: "Phase 4a: Card analysis ✓"
  4b: "Phase 4b: Cards ✓"
  5: "Phase 5: FCT Quality ✓"
  6: "Phase 6: SSOT frozen ✓"
  7: "Phase 7: Ready ✓"
  8: "Phase 8: Code ✓"
  9: "Phase 9: COMPLETE ✓"

on_fail: block_phase   # hard block — no phase transition with uncommitted files
```

## GitFlow Branch Strategy

```yaml
branch_per_run:
  pattern: "feature/swarm-review-{YYYYMMDD}"
  create_at: phase_1_bootstrap
  merge_to: main
  merge_at: phase_9_complete

commit_trailer: |
  Co-authored-by: Swarm <swarm@colony>
```

## Pass

- Commit exists for each phase
- Every created/updated file has a commit
- `bio/commit_log.yaml` is non-empty at terminal
- No uncommitted files at any phase boundary
- `git status --porcelain` is empty immediately after each phase commit
- Every phase id in commit log is canonical (`0`,`1`,`2`,`3`,`4a`,`4b`,`5`,`6`,`7`,`8`,`9`)
- No `pending` SHA values at any passed phase

## Fail

- Phase without commit → block_phase
- File created but not committed → block_phase
- Uncommitted at terminal → BLOCKED
- Non-canonical combined phase id (e.g. `0-1`, `4a-4b`) → block_phase
- Any `pending` SHA in passed phase → block_phase
