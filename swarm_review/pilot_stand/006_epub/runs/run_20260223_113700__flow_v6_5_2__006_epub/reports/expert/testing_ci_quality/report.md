# Expert Report: testing_ci_quality

Agent: `019c89a6-788f-7131-85c5-025773744be1`

1. **Unmarked destructive test can run in default CI selection**  
Severity: `P0`  
Evidence: `tests/integration/test_manual_fallback.py:15`, `tests/integration/test_manual_fallback.py:25`, `tests/integration/test_manual_fallback.py:50`, `tests/integration/test_manual_fallback.py:136`, `.github/workflows/ci.yml:24`, `pytest.ini:6`  
Remediation: Mark this test as `manual` (and `integration`) at module level, isolate config mutation to temp files/monkeypatched env vars, and block `.env` writes in automated CI tests.

2. **CI currently excludes the marker-tagged integration/e2e suites**  
Severity: `P1`  
Evidence: `.github/workflows/ci.yml:24`, `pytest.ini:6`, `tests/integration/test_common_handlers.py:25`, `tests/e2e/test_complete_human_translation_journey.py:29`  
Remediation: Add dedicated CI jobs for `-m integration` and a stable `-m "e2e and smoke"` subset; keep current fast job as a separate gate, not the only gate.

3. **E2E marker hygiene is inconsistent, so marker-based CI filtering is unreliable**  
Severity: `P1`  
Evidence: `.github/workflows/ci.yml:24`, `tests/e2e/test_photo_to_book_flow.py:30`, `tests/e2e/test_photo_to_book_flow.py:93`, `tests/e2e/test_translation_pipeline_complete.py:64`  
Remediation: Require `pytestmark = pytest.mark.e2e` (or per-test `@pytest.mark.e2e`) for every executable test under `tests/e2e`, and enforce via a lint/check script in CI.

4. **Duplicate test function name shadows an earlier test definition**  
Severity: `P2`  
Evidence: `tests/e2e/test_user_case_15_docker_find_human_behavior.py:639`, `tests/e2e/test_user_case_15_docker_find_human_behavior.py:1212`  
Remediation: Rename/split the duplicate into uniquely named tests and add static checks (`ruff`/`pyflakes` F811) in CI to catch redefinitions.

5. **Dependency installation is non-deterministic across CI runs**  
Severity: `P1`  
Evidence: `.github/workflows/ci.yml:19`, `.github/workflows/ci.yml:20`, `.github/workflows/ci.yml:21`, `requirements.txt:8`, `requirements.txt:15`, `requirements.txt:25`, `requirements.txt:30`, `requirements.txt:46`  
Remediation: Use a locked dependency set (constraints/lockfile), pin test tooling versions, and remove ad-hoc extra installs (`pip install pytest pytest-asyncio`) from CI.
