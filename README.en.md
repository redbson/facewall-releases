# Facewall · Releases and changelog

> Stitch scattered thoughts into a thinking wall you can act on.

Facewall is a **local-first, AI-native thinking wall for macOS**. Drop a thought the moment it appears (a **trace**);
a cognitive agent in the background classifies it, links it to what you thought before, and stitches it into
**threads** that keep growing. It notices when you **change your mind**, lets judgments that keep recurring surface
as **patterns**, and **recalls your past self** when you come back to a question.

The loop: `trace → stitch → thread → pattern → recall`, plus one **Daily Stitch** card a day.

This repository holds only the **changelog, status notes and installers**; the source lives in a private repository.

- 📦 **Download**: [Releases](https://github.com/redbson/facewall-releases/releases)
- 📝 **Changelog**: [CHANGELOG.md](CHANGELOG.md) (Chinese)
- 📍 **Status and roadmap**: [docs/STATUS.md](docs/STATUS.md) (Chinese)
- 中文说明：[README.md](README.md)

---

## Install

**Requirements**: macOS 13 or later, Apple Silicon. The interface follows your system language (English or
Simplified Chinese; selectable in Settings from 0.3.2). The bundled embedding model is Chinese-first; recall over
English traces works but is weaker.

1. Download the latest `Facewall-<version>.dmg` from [Releases](https://github.com/redbson/facewall-releases/releases)
   and drag **Facewall.app** into Applications.
2. The app is **ad-hoc signed and not notarized** (no Apple Developer Program yet), so macOS blocks the first launch.
   Either, once:
   - run in Terminal:

     ```bash
     xattr -dr com.apple.quarantine /Applications/Facewall.app
     ```

   - or, after the block, open **System Settings › Privacy & Security**, scroll down and click **Open Anyway**.
     (Right-click › Open no longer works since macOS 15.)

   Proper signing and notarization are on the roadmap; this step goes away then.
3. Open Facewall. The engine is ready in about two seconds; data lives in `~/Library/Application Support/Facewall/Data`.
4. Press **⌘,** to connect a model:
   - with **Claude Code** or **Codex** installed, Settings offers one-click enable through your existing subscription, no API key;
   - or use Anthropic / OpenAI / Azure, or any OpenAI-compatible endpoint (presets for DeepSeek, Kimi, GLM, Qwen, Ollama…).
5. In any app press **⌥⇧Space**, write a thought, hit Return.

The app ships its own Python runtime and embedding model; apart from calling the model you configured it is
**fully offline**. There is no server and nothing is uploaded.

## Everyday entry points

| Entry | How |
|---|---|
| Quick capture panel | ⌥⇧Space in any app (does not steal focus); ↩ drop, ⌥↩ drop and continue, ⌘↩ drop and open the wall, ⇥ switch to recall |
| Services menu | select text → right-click → Services → **Save to Facewall** |
| Menu bar icon | quick capture, recall, pending count, recent traces |
| URL scheme | `facewall://capture?text=…`, `facewall://recall?q=…`, `facewall://trace/<id>` |
| Terminal | `fw a thought`, `pbpaste \| fw`, `fw -r question` (script ships with the source) |

Inside the app: **⌘K** command palette, **⌘F** recall, **⌘?** help.

## Data and privacy

- Everything is one SQLite file on your Mac; **⇧⌘E** exports complete JSON (verbatim text), **⌘O** imports.
- Daily automatic backups (7 days), plus one before upgrades, imports and restores; restore from any of them in Settings › Data & Engine.
- Deleted or hidden traces never reappear anywhere (including judgments, concepts and patterns derived from them) and are never sent to the model again.
- "Let it fade": the text stays on the wall but is no longer recalled, suggested or linked; wake it any time.
- What reaches the model: the current trace with its few most related past traces and the judgments of the threads involved. System notifications carry no text by default.
- Usage counters stay in the data folder and are never uploaded.

## Feedback

Open an [issue](https://github.com/redbson/facewall-releases/issues). Please describe what happened rather than pasting your own traces.
