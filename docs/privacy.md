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

- Model requests send selected context to the configured endpoint. A stitch can include the current trace, related traces and thread judgments. Recall can include your question and matching traces. With OntoRouter selected, the router determines which model receives the request. A direct API receives it from Facewall.
- Recall web search is optional and uses OntoRouter. It sends your question as the search query for recalls you choose to search.
- The optional read-only MCP connection returns readable notes and thinking threads to the connected agent. Hidden, deleted, explicitly forgotten and example notes are excluded. The agent may include returned content in its own model requests.
- Command-palette search, embeddings, layout and usage counters run locally. Update checks request release information from GitHub.
- ⇧⌘E exports everything as JSON with the text verbatim; ⌘O imports it. Files Facewall writes are readable by you alone.
- The quick capture panel, the Services menu and system notifications never show text by default; a notification is withdrawn when its trace is deleted.
