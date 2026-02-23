# Expert Report: security_config_surface

Agent: `019c89a6-7a4b-7762-8528-9eff48e3e214`

## Security Config Surface Report (5 Findings)

1. **Plaintext bot credential present in runtime env file**
Severity: **P0**  
Evidence: `.env:3`; `config.py:157`; `docker-compose.yml:13`  
Remediation: Rotate the Telegram token immediately, remove real credentials from `.env`, load secrets from a secret manager/runtime env injection, and keep only placeholders in local templates.

2. **Whitelist bypass is enabled in default configuration path**
Severity: **P1**  
Evidence: `.env.example:7`; `.env.example:14`; `.env:7`; `.env:14`; `bot/filters.py:35`; `bot/filters.py:37`  
Remediation: Set `DISABLE_WHITELIST=false` in defaults, require explicit secure override for local-only debugging, and add startup hard-fail when whitelist is disabled outside tightly controlled dev runs.

3. **User-controlled query is passed to CLI without explicit option boundary**
Severity: **P1**  
Evidence: `bot/handlers/common.py:328`; `bot/handlers/common.py:341`; `core/find_epub_cli.py:87`; `core/find_epub_cli.py:226`  
Remediation: Add strict query validation and pass `--` before positional query (if supported by `find_epub`) to prevent option-style argument injection.

4. **PATH-based command execution with unqualified binary name**
Severity: **P2**  
Evidence: `core/vision/ask_gemini_vision_service.py:22`; `core/vision/ask_gemini_vision_service.py:67`; `core/ai_toc_extractor.py:290`  
Remediation: Use pinned absolute executable paths, verify file ownership/permissions (and ideally checksum/signature) at startup, and run with a minimal trusted `PATH`.

5. **Sensitive values are written/printed by operational scripts**
Severity: **P1**  
Evidence: `scripts/development/debugging/clean_env_deepseek_diagnosis.sh:40`; `scripts/development/debugging/clean_env_deepseek_diagnosis.sh:117`; `docker-entrypoint.sh:90`; `docker-entrypoint.sh:92`  
Remediation: Remove plaintext secret logging and backup of full keys, redact sensitive fields by default, and ensure any diagnostics output is masked and access-restricted.
