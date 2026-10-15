# Changelog

Versions follow `major.minor.patch`; `x.y.z-dev.date` is a **Facewall Dev** preview that installs next to the release build (its own bundle id, data folder, port and hotkeys).

## 0.3.4 · 2026-10-15

### Recall can look on the web
- **Settings › AI model › Web search** (off by default): with it on, the recall panel gains a *Look on the web too* box; for a recall you tick, the model searches the internet itself once before writing (Claude Code, Codex or the Anthropic API — no search service to configure) and lists the sources it used under *From the web*, with links and a line each, kept strictly apart from your own past. Only the question is sent, never trace text; stitching and the Daily Stitch never go online.

### The cognitive kernel takes part in the core loop
- When stitching, the model now sees the kernel's projection of the related concepts and the opposing stances it knows, and uses them to pick concepts and threads and to judge reversals.
- How fast a trace fades listens to the kernel's maturity for its concepts: a trace whose concepts are active or core in the world fades on the "connected" curve (a one-month half-life instead of one week).
- Two new Daily Stitch cards: **tension** (two of your thoughts that pull against each other — which side today?) and **dormant concept** (one that mattered and went quiet).
- World 0 and the built-in graph kernel both serve all three; when World 0 is absent or fails, the built-in kernel answers.

### Other
- With several copies of a local CLI installed (an old `/usr/local/bin/claude` next to a current `~/.local/bin/claude`), the engine now picks the newest, instead of whichever PATH lists first.

## 0.3.3 · 2026-10-15

### In-app updates
- **Settings › Updates**: check for a new version, download it, verify its SHA-256, bundle id and signature, then **Restart & update** in one click; a downloaded update you don't restart for installs the next time you quit Facewall. Facewall checks at launch and every 12 hours (can be turned off) and can download updates in the background. Menu: **Facewall › Check for Updates…**.
- **Version log**: Settings › Updates lists what changed in every version, in English or Chinese to match the interface.
- The sidebar no longer shows the version number; "Update" appears there when a new version is out.
- **Coming from 0.3.2 or earlier, install this version by hand once**; every later version installs from inside the app, and in-app updates don't need the quarantine step.

### Gemini CLI (preview)
- Settings › AI model now offers **Gemini CLI (local)**: with Google's `gemini` command installed and signed in, Facewall stitches and recalls through your own Google account or API key — like Claude Code and Codex, no key to enter in Facewall. Pick Auto / Pro / Flash / Flash-Lite, or pin a specific model.
- It runs read-only, without extensions or MCP servers, and the session log Gemini keeps on your Mac is deleted after every run.
- Marked as a preview: not yet fully tested against a real Gemini model — please open an issue if something goes wrong.

### Cognitive kernel (World 0)
- The bundled World 0 is now 0.5.1.
- Conflict hints in recall no longer treat the topic two traces share as a conflict; only the two opposing stances are flagged.
- When several traces are stitched back to back they now reach World 0 in order; before, a real change of mind could be missed.
- On first launch the cognitive world is rebuilt from your history under the new rules; the old one is kept as a backup.

### Other
- The settings button is now a gear (the old icon looked like a brightness control); "Fix concept" in Memory is now a pencil.
- No database schema change; upgrading from 0.3.x needs no migration.

## 0.3.2 · 2026-10-14

### Chinese and English
- The interface, menus, quick-capture panel, system notifications, Services menu, user guide, command palette and the model's output (judgments, next stitch, recall answers, daily stitch) all come in **简体中文** and **English**. By default Facewall **follows the device language** (Chinese if the system is Chinese, English otherwise); you can fix either one under Settings › General › Language, and the switch applies at once without a restart.
- The language preference is stored both in the app and in the data folder, so background work with no page open — stitching, the daily stitch — uses the same language.
- The `fw` terminal script follows the shell's `LANG`.
- **Existing data isn't retranslated**: older thread judgments and daily-stitch cards keep the language they were written in. The embedding model is still a Chinese model (bge-small-zh), so recall over English traces works but is weaker.
- No database schema change; upgrading from 0.3.x needs no migration.

## 0.3.1 · 2026-10-14

Everything in these two days came out of a full product review (a nine-dimension audit, adversarial verification, independent reproduction), followed by two rounds of hands-on testing on an installed Facewall Dev with real models (Claude Code, Codex).
**No database schema change**; upgrading from 0.3.0 needs no migration.

### Keeping its word
- A core judgment you edited yourself is no longer overwritten by the next stitch. Thread pages mark "your judgment" and can show how it changed; the AI's new judgment is only a suggestion you adopt or ignore.
- After you delete or hide a trace, the patterns, concepts and judgments derived from it no longer appear on any page, export or daily stitch, and are no longer sent to the model.
- The quick-capture outbox no longer gets stuck behind one rejected capture. When the engine refuses one (e.g. too long), the panel says why and lets you copy the text; replays keep the original capture time and never duplicate.
- Quitting the app shuts the engine down cleanly within a second, writes data back to the main database and leaves no orphan process. **Restoring a backup can be done right in Settings** (the current data is backed up first), and the manual-restore instructions were corrected.
- System notifications no longer include the text or summary by default (can be turned on in Settings); deleting a trace withdraws its notifications.
- OpenAI / Azure requests explicitly ask the server not to store them; the database, logs and other files are readable by you only.

### More reliable stitching
- Failures of the local Claude Code / Codex are told apart by kind (quota, not signed in, network, timeout, configuration); after the circuit breaker trips it recovers per kind, and configuration errors are no longer blamed on a trace.
- The backlog is stitched in time order with dates, so reversals no longer point the wrong way; model output is validated before it's written; "not a reversal" restores the old judgment it had replaced.
- Stitching resumes automatically after wake and when the network returns; a hung engine restarts by itself; two engines can't open the same data folder.

### Value you can see
- The daily stitch stays at the top of the stitch page (folded into one line when you're busy); "Today's stitch" can be brought up any time.
- Every trace's stitch result can be revisited: which thread it went into, which earlier words it connected to and why, reversals found, the next stitch; a list of recent stitches; clicking a system notification jumps straight to that trace.
- The semantic layout no longer jumps around with every new trace; a new trace outside the view is panned into sight.
- Reversals are visible in the wall's default view; judgment changes have a timeline.

### Closing the correction loop
- A trace can be "moved to" another thread or a new one, and later stitches respect your choice; threads can be split; merges are confirmed first and can be undone within 10 minutes; hidden traces can be restored.
- A long-term pattern can be rejected with "this isn't my pattern" and restored later; patterns flagged by the model are only "under observation" until they reach the bar (≥3 traces, across 2 threads, across 2 days).

### Recall and forgetting (new)
- Recall judges how sure it is — confident / indirectly related / unrelated — and when nothing is related it says plainly "you haven't thought about this before" instead of stretching; each step of the evolution path quotes the original words and can be opened.
- **Forgetting**: every trace has a salience that decays over time (after World 0's decay model: one-week half-life when isolated, one month when connected, three months when pinned or recalled often, never reaching zero). Traces not thought of for a long time fold into "faded memories" and become active again when opened, connected or answered; you can also "let it fade" on purpose — the text stays on the wall but is no longer recalled, surfaced or connected — and "wake" it any time.
- Recall started from a trace no longer treats that trace as its own past.

### First run
- When a local Claude Code / Codex is found, it's recommended with one-click enabling (even when the environment has a paid API key; "keep current settings" is available); with nothing configured, Facewall no longer falls back to Azure.
- Example traces are labelled "example", can be cleared in one click, and stay out of the daily stitch and pattern evidence.
- The main composer's draft survives view switches and reloads and grows with its content; ⌘K defaults to local search (nothing leaves the machine), dropping a trace takes ⌘↩ and can be undone; Enter handling under input methods is unified; startup no longer flashes an empty wall.

### Engineering
- 265 backend, 63 frontend and 72 Swift automated tests; packaging runs all three suites on the app's bundled runtime and verifies the signature; dependencies are locked.
- The port no longer drifts; the web cache no longer keeps snapshots of the wall; times are shown in the local time zone.

## 0.3.0 · 2026-10-12

- User guide (⌘?), About panel and the HETERONTO credit.
- The interface moved to the Heteronto design system: light / dark / follow system and several dark styles; the wall folds traces by thread, with sources marked segment by segment; thread pages show "changed my mind"; the daily stitch quotes whole clauses.
- AI settings: available models are fetched automatically and picked from a list; Claude Code models can "follow the latest" or be pinned to a version.
- Trust and scale: derived content cleaned up after deletes, a migration framework and daily backups, a promotion bar for patterns, World 0 integration fixes; replaying 10,000 traces went from 25 minutes to 16 seconds.
- Claude Code / Codex as model providers (uses your local subscription, no API key needed); the daily stitch; local usage statistics; `run.py eval` quality evaluation.

## 0.2.0 · 2026-10-02

- **Facewall becomes a macOS app**: lives in the menu bar, a global-hotkey capture panel (⌥⇧Space), "Save to Facewall" in the Services menu, a `facewall://` URL scheme, the `fw` terminal command; captures go to an outbox and are never lost.
- Engine: Chroma removed, vectors stored in SQLite; a stitch queue with a circuit breaker; an SSE event stream; local token / Host / Origin guards; the Chinese embedding model bge-small-zh.
- Wall-first layout, a command registry, focused subgraphs, editable threads and concepts, data import.
- World 0 as an upgradable cognitive-kernel component.

## 0.1.0 · 2026-06 – 2026-09

The browser dev-mode MVP: an asynchronous stitch pipeline, a weekly growth digest, data export, automatic model lists and presets for compatible endpoints, Azure OpenAI by default.
