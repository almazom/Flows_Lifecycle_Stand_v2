# Expert Report: performance_concurrency

Agent: `019c89a6-7cc8-7ca0-8c19-53b93c13865f`

1. **Blocking subprocess in async summarization path**
Severity: **P0**  
Evidence: `core/summarizer/providers/gemini_cli_provider.py:87`, `core/summarizer/providers/gemini_cli_provider.py:115`, `core/summarizer/providers/gemini_cli_provider.py:216`, `core/summarizer/chain_manager.py:142`, `bot/handlers/navigation/summary/request.py:623`  
Remediation: Replace `subprocess.run(...)` with `await asyncio.create_subprocess_exec(...)` (or `await asyncio.to_thread(...)` as interim), and keep timeout/cancellation handling in async flow.

2. **Vision analysis blocks event loop via sync CLI subprocess**
Severity: **P0**  
Evidence: `core/vision/gemini_cli_vision_service.py:167`, `core/vision/gemini_cli_vision_service.py:200`, `core/vision/gemini_cli_vision_service.py:59`, `core/vision/ask_gemini_vision_service.py:181`, `core/vision/ask_gemini_vision_service.py:211`, `core/vision/ask_gemini_vision_service.py:83`, `core/vision_book_search_service.py:156`  
Remediation: Make both vision clients fully async (async subprocess APIs) and enforce bounded concurrency (e.g., semaphore) for photo analysis requests.

3. **Synchronous EPUB parsing inside async translation extraction**
Severity: **P1**  
Evidence: `core/translation/content_extractor.py:41`, `core/translation/content_extractor.py:68`, `core/translation/content_extractor.py:69`, `bot/handlers/navigation/chapter/actions.py:245`  
Remediation: Switch to `AsyncEpubProcessor`/`asyncio.to_thread` for chapter extraction so EPUB parsing and boundary extraction do not run on the event loop thread.

4. **Unbounded concurrent Telegram deletions (rate-limit/perf hotspot)**
Severity: **P1**  
Evidence: `bot/handlers/common.py:989`, `bot/handlers/common.py:990`, `bot/handlers/common.py:1010`, `bot/handlers/common.py:1013`, `bot/handlers/common.py:1016`  
Remediation: Add bounded parallelism (e.g., semaphore with small worker pool), batch deletes, and retry/backoff on Telegram flood errors instead of firing all deletions at once.

5. **Blocking MP3 hash/file read in async TTS handler**
Severity: **P2**  
Evidence: `bot/handlers/navigation/chapter/actions.py:538`, `bot/handlers/navigation/chapter/actions.py:663`, `bot/handlers/navigation/chapter/actions.py:664`  
Remediation: Move checksum/file-read work to `asyncio.to_thread` (or use cached metadata/hash) to avoid blocking the loop during cache-hit TTS sends.
