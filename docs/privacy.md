# Data and privacy

English | [简体中文](privacy.zh-CN.md)

Where Facewall keeps your data and what leaves your Mac.

| What | Where |
|---|---|
| Your wall | `~/Library/Application Support/Facewall/Data/facewall.db` — every trace, link, judgment, pattern and vector in one SQLite file. The folder can be moved from Settings › Data & engine. |
| Backups | `…/Data/backups/` — one a day for the last 7 days, the last 5 manual ones, plus one before every upgrade, import and restore. Restore from any of them in Settings. |
| Model configuration | `…/Data/llm_config.json`, readable by you alone. Keys are never sent back to the interface. |
| Captures waiting for the engine | `~/Library/Application Support/Facewall/outbox.jsonl` |
| Logs | `~/Library/Logs/Facewall/app.log` and `engine.log` (Help › Open logs) |

- What reaches the model you configured, and nothing else: the trace being stitched, its few most related past traces, and the judgments of the threads involved; for recall, your question and the recalled traces. OpenAI and Azure requests ask the server not to store them.
- Web search is off unless you turn it on, and then only a recall you ticked goes online: the model searches with your question, never with trace text. Stitching and the Daily Stitch never go online.
- Everything else is local: search in the command palette, the embedding model, the layout, the usage counters, update checks (which only ask GitHub for the latest version number).
- ⇧⌘E exports everything as JSON with the text verbatim; ⌘O imports it. Files Facewall writes are readable by you alone.
- The quick capture panel, the Services menu and system notifications never show text by default; a notification is withdrawn when its trace is deleted.
