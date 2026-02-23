# 006_epub Pilot Stand

## Scope

This project is used as a pilot workload to evolve `swarm_review` versions.

- Target project path: `/home/pets/zoo/006_epub`
- Target repo: `https://github.com/almazom/006_epub`
- Goal: improve flow quality, not project feature delivery.

## Run Cycle

1. Select flow version (`v6.5.2`, `v6.5.3`, ...).
2. Start run with unique `run_id`.
3. Collect run artifacts in `runs/{run_id}/`.
4. Fill run review from `templates/RUN_REVIEW_TEMPLATE.md`.
5. Score satisfaction and confidence.
6. Decide:
   - If score <95%: open gaps and create next patch version.
   - If score >=95% and no critical gaps: mark version as `Stable`.

## Required Evidence Per Run

- Expectations snapshot used in this run.
- Actual artifacts list (what was produced).
- Gap register (missing vs expected).
- Error/ignore list.
- Satisfaction score (0-100).
- Confidence score (0-100).
- Stable decision record.

