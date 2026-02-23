# Expert Report: maintainability_doc_debt

Agent: `019c89a6-7e9d-7793-95a8-bb08cedac2c1`

## Maintainability / Documentation Debt Report (`pilot_projects/006_epub`)

1. **Bulk upload state is restart-unsafe (operability debt)**  
Severity: **P1**  
Evidence: `pilot_projects/006_epub/bot/handlers/bulk_upload.py:72`, `pilot_projects/006_epub/bot/handlers/bulk_upload.py:73`, `pilot_projects/006_epub/bot/handlers/bulk_upload.py:75`, `pilot_projects/006_epub/bot/handlers/bulk_upload.py:235`  
Remediation: Persist bulk session/job state (Redis or DB), add batch/job IDs, and implement resume/recovery on process restart.

2. **Critical upload scenarios are left as xfail TODO placeholders**  
Severity: **P1**  
Evidence: `pilot_projects/006_epub/tests/integration/test_upload.py:329`, `pilot_projects/006_epub/tests/integration/test_upload.py:333`, `pilot_projects/006_epub/tests/integration/test_upload.py:369`  
Remediation: Implement non-EPUB validation and duplicate-upload behavior tests, then remove `xfail` placeholders to restore regression protection.

3. **Docs index references a stale/nonexistent filename**  
Severity: **P2**  
Evidence: `pilot_projects/006_epub/docs/_INDEX.md:13`, `pilot_projects/006_epub/docs/00-overview/user_stories.md:1`  
Remediation: Update `_INDEX.md` to `user_stories.md` and add automated markdown link/path validation in CI.

4. **Project identity is inconsistent across active docs (005 vs 006)**  
Severity: **P2**  
Evidence: `pilot_projects/006_epub/README.md:1`, `pilot_projects/006_epub/docs/03-operations/deployment/docker_management.md:3`, `pilot_projects/006_epub/docs/03-operations/deployment/docker_management.md:10`, `pilot_projects/006_epub/docs/flow_pilot/GITFLOW_PILOT.md:5`  
Remediation: Define one canonical project identifier and normalize README/operations docs to that identifier (including container/service naming examples).

5. **Keyboard layer is a monolith with deferred TODO/deprecation markers (readability debt)**  
Severity: **P2**  
Evidence: `pilot_projects/006_epub/README.md:69`, `pilot_projects/006_epub/bot/keyboards.py:567`, `pilot_projects/006_epub/bot/keyboards.py:1442`, `pilot_projects/006_epub/bot/keyboards.py:1921`  
Remediation: Split `bot/keyboards.py` by domain (TOC, summary nav, settings, progress), remove deprecated args, and track remaining TODOs as issue-backed tasks.
