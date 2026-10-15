# Facewall

English | [简体中文](README.zh-CN.md)

[![release](https://img.shields.io/github/v/release/redbson/facewall-releases?label=release&color=e8743b)](https://github.com/redbson/facewall-releases/releases/latest) [![platform](https://img.shields.io/badge/platform-macOS%2013%2B%20%C2%B7%20Apple%20Silicon-555)](#install)

Facewall is a local-first, AI-native **thinking wall for macOS**. Drop a thought the moment it appears; an AI in the
background links it to what you thought before, stitches it into growing **threads**, notices when you **change your
mind**, and **recalls your past self** when you come back to a question. It stitches through **Claude Code**,
**Codex** or **Gemini CLI** on your existing subscription, or any API you configure — there is no server, and nothing
from your wall leaves your Mac except what the model needs. The interface is in English and Chinese; it follows your Mac's language and can be
switched in Settings.

⬇️ **Download:** [macOS](https://github.com/redbson/facewall-releases/releases/download/v0.3.3/Facewall-0.3.3.dmg) · [All releases](https://github.com/redbson/facewall-releases/releases) · [Changelog](CHANGELOG.en.md)

## Install

Requires macOS 13+ on Apple Silicon.

1. Download the latest `Facewall-<version>.dmg` from [Releases](https://github.com/redbson/facewall-releases/releases) and drag **Facewall.app** into Applications.
2. The app is ad-hoc signed and not notarized, so macOS blocks the first launch. Once, either run

   ```bash
   xattr -dr com.apple.quarantine /Applications/Facewall.app
   ```

   or click **Open Anyway** in **System Settings › Privacy & Security** after the block.
3. Open Facewall and press **⌘,** to connect a model. With **Claude Code** or **Codex** installed it offers one-click
   setup on your existing subscription (no API key); Gemini CLI (preview), Anthropic, OpenAI, Azure and
   OpenAI-compatible endpoints (DeepSeek, Kimi, GLM, Qwen, Ollama…) work too.

**Updating:** from 0.3.3 on, Facewall updates itself — **Settings › Updates** (or **Facewall › Check for Updates…**).

## How to use it

1. **Drop thoughts as they come.** Press **⌥⇧Space** in any app, type, hit Return. One thought per trace; half-formed
   is fine — don't organize, just write what you think, in your own words.
2. **Let it stitch.** Each trace is stitched in the background: which **thread** it belongs to, which earlier traces it
   connects to and why, and the thread's current judgment. Select a trace to see its stitch in the right-hand panel.
3. **Correct it when it's wrong.** Move a trace to another thread, mark a link as wrong, rewrite a thread's judgment,
   split or merge threads. Later stitches respect your corrections; your own judgment always wins.
4. **Watch your mind change.** The **Wall** (⌘1) shows traces grouped by thread with reversals marked; **Threads** (⌘2)
   shows how each judgment evolved and where you changed your mind.
5. **Keep thinking with recall.** Press **⌘F** and ask a question: Facewall brings back what you thought before, quotes
   your own words step by step, and says plainly when you never thought about it.
6. **Come back every day.** The **Daily Stitch** brings back one older thought with a question. Over weeks, judgments
   that keep recurring across threads surface in **Memory** (⌘3) as long-term patterns — reject any that aren't you.

Want a feel for it first? Run **Load example traces** from the ⌘K command palette on an empty wall; clear them in one click.

## Shortcuts and entry points

| | |
|---|---|
| ⌥⇧Space | Quick capture from any app (⇥ switches to recall) |
| ⌘K · ⌘F · ⌘? | Command palette · recall · in-app guide |
| Services menu | Select text → right-click → Services → **Save to Facewall** |
| Menu bar icon | Quick capture, recall, pending stitches, recent traces |
| URL scheme | `facewall://capture?text=…` · `facewall://recall?q=…` |

## Data and privacy

- Everything stays on your Mac in one SQLite file; there is no server. **⇧⌘E** exports full JSON, **⌘O** imports.
- Daily backups (kept 7 days); restore any of them in Settings › Data & Engine.
- Only the model you configure sees anything: the current trace, its few most related past traces and the thread judgments involved.
- Update checks only ask GitHub for the latest release; they carry nothing from your wall (can be turned off).
- Deleted or hidden traces never reappear and are never sent to the model again; "let it fade" keeps the text but stops recalling it.

## Feedback

Open an [issue](https://github.com/redbson/facewall-releases/issues) — describe what happened rather than pasting your own traces.
