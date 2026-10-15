# Facewall

English | [简体中文](README.zh-CN.md)

[![Latest release](https://img.shields.io/github/v/release/redbson/facewall-releases?label=release)](https://github.com/redbson/facewall-releases/releases/latest) [![Platform](https://img.shields.io/badge/platform-macOS%2013%2B%20%C2%B7%20Apple%20silicon-555)](#requirements)

Facewall is a local-first, AI-native **thinking wall for macOS**. Drop a thought the moment it appears, from any app; an AI in the background links it to what you thought before, stitches it into **threads** that keep growing, notices when you **change your mind**, lets judgments that keep recurring surface as **patterns**, and **recalls your past self** when you come back to a question. It stitches through the **Claude Code**, **Codex** or **Gemini CLI** you are already signed in to, or any API you configure. There is no server and no account: your thoughts live in one database on your Mac, and only the model you chose ever sees them. The interface is in English and Chinese; it follows your Mac's language and can be switched in Settings.

**⬇ Download: [macOS](https://github.com/redbson/facewall-releases/releases/download/v0.3.4/Facewall-0.3.4.dmg)** · [All releases](https://github.com/redbson/facewall-releases/releases) · [Changelog](CHANGELOG.en.md)

This repository holds the installers, the changelog and the documentation; the source code is private.

## Features

- **Capture from anywhere**: a global hotkey (⌥⇧Space) opens a small floating panel over any app without stealing its focus; Return puts the thought on the wall. Also from the Services menu (select text → **Save to Facewall**), the menu bar icon, the Dock, and a `facewall://` URL scheme for Shortcuts, Raycast or Alfred. If the engine isn't ready, captures wait locally and are delivered later — a thought is never lost.
- **Stitching**: every trace is stitched in the background: filed under a thread (new or existing), linked to related past traces with a reason for each link, and the thread's current judgment is updated. Facewall never guesses links by rule; without an AI, traces simply wait as "pending" and are stitched once a model is connected.
- **Reversals**: when a new thought contradicts an earlier judgment, the stitch says so, the old judgment is retired rather than deleted, and the reversal is marked on the wall and in the thread's history. "Not a reversal" undoes it.
- **Corrections that stick**: move a trace to another thread, split or merge threads, mark a link as off, rewrite a judgment, rename or merge a concept. Later stitches respect what you changed, and a judgment you wrote yourself is never overwritten — the AI's new wording is only offered as a suggestion.
- **Recall**: ask a question (⌘F) and Facewall brings back your own past words, dated and quoted step by step, with the judgment that holds up best right now and how it changed. It says how sure it is, and when nothing in your past relates, it says so instead of making something up.
- **Memory and forgetting**: judgments that recur across threads become long-term patterns, only once there is enough evidence (at least three traces, across two threads and two days) — reject any that aren't you. Traces nothing has recalled for a long time fade on their own and come back the moment they are opened or linked; you can also let a trace fade on purpose, or wake it.
- **The Daily Stitch**: one card a day — an older thought, a thread or an open question, with a question to answer. Reply in place, recall from it, pick another, or skip today.
- **Three views**: the **Wall** (traces grouped by thread, semantic layout, reversals marked), **Threads** (each thread's judgment history and traces), and **Memory** (patterns, concepts, faded and hidden traces).
- **Your model, your choice**: one-click setup with the Claude Code, Codex or Gemini CLI on this Mac, on your existing subscription and with no API key; or Anthropic, OpenAI, Azure OpenAI and any OpenAI-compatible endpoint (presets for DeepSeek, Kimi, GLM, Qwen and Ollama). Failures are told apart (quota, signed out, network, misconfigured) and stitching resumes by itself.
- **Local by design**: one SQLite file, daily backups, in-app restore, full JSON export and import, no telemetry. The app ships its own Python runtime and embedding model; apart from the model call it is fully offline.
- **Automatic updates**: Facewall checks GitHub Releases for a new version and installs it after verifying it, see [Automatic updates](#automatic-updates).

## Requirements

- macOS 13 or later, Apple silicon. There is no Intel build.
- A model to stitch with — one of:
  - [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (`claude`), [Codex CLI](https://github.com/openai/codex) (`codex`) or [Gemini CLI](https://github.com/google-gemini/gemini-cli) (`gemini`, preview), installed and signed in. Facewall runs them on your subscription; no API key is needed.
  - or an API key for Anthropic, OpenAI, Azure OpenAI, or any OpenAI-compatible endpoint, including a local Ollama.
- Nothing else: Python and the embedding model are inside the app.

The bundled embedding model is Chinese-first; recall over English traces works but is weaker.

## Installation

1. Download [Facewall-0.3.4.dmg](https://github.com/redbson/facewall-releases/releases/download/v0.3.4/Facewall-0.3.4.dmg) (or pick a version on [Releases](https://github.com/redbson/facewall-releases/releases)), open it, and drag `Facewall.app` into Applications.
2. First launch: Facewall is not notarized by Apple, so macOS says it cannot verify the developer. Open System Settings → Privacy & Security and click **Open Anyway** near the bottom, or run:

   ```bash
   xattr -dr com.apple.quarantine /Applications/Facewall.app
   ```

3. Later versions are downloaded and installed by Facewall itself (see [Automatic updates](#automatic-updates)), so you won't see this prompt again.
4. Open Facewall. The engine is ready in about two seconds. Press **⌘,** to connect a model: with Claude Code, Codex or Gemini CLI on this Mac an **Enable** card is waiting at the top of AI settings; otherwise pick a service and enter a key.
5. Press **⌥⇧Space** in any app, write a thought, press Return.

To start Facewall when you log in, turn on **Launch at login** under Settings › Appearance & general. Facewall then lives in the menu bar, ready to capture.

Want a feel for it first? Run **Load example traces** from the ⌘K command palette on an empty wall. Examples are marked as such, never count as your words, and go away with one click.

## Automatic updates

- Facewall checks the latest GitHub release shortly after it starts and every 12 hours after that. Nothing from your wall is sent; the check can be turned off.
- When there is a newer version, **Settings › Updates** and the bottom of the sidebar say so, with the release notes. **Download & install** fetches the dmg and checks its SHA-256 checksum, bundle identifier, version and code signature. Only if all of them match does it stage the new app; **Restart & update** then swaps it in and reopens Facewall. A downloaded update you don't restart for is installed the next time you quit.
- **Download updates automatically** does the download and verification in the background; the update installs when you quit.
- If Facewall runs from the disk image, from macOS's quarantine location or from a folder you can't write to, it can't replace itself and points you to the releases page instead.
- Coming from 0.3.2 or earlier, install 0.3.3 by hand once; every later version installs from inside the app.

## Documentation

- [User guide](docs/guide.md) — capturing, stitching, corrections, recall, the Daily Stitch, threads and memory, settings, shortcuts.
- [Data and privacy](docs/privacy.md) — where your data lives, what reaches the model, what never leaves your Mac.
- [Troubleshooting](docs/troubleshooting.md) — first launch, model setup, paused stitching, updates, backups.
- [Changelog](CHANGELOG.en.md) — every version in detail ([中文](CHANGELOG.md)). Checksums of every installer are in [checksums/](checksums/).
- [Status and roadmap](docs/STATUS.md) (Chinese) — what works, what is known to be rough, what comes next.

## Changelog

### 0.3.4
- Recall can look on the web (opt-in): the model searches by itself and lists its sources apart from your own past.
- The cognitive kernel now takes part in stitching, forgetting and the Daily Stitch (tension and dormant-concept cards); World 0 and the built-in kernel both serve it.
- Several copies of a local CLI: the newest wins.

### 0.3.3
- In-app updates: check, download, verify and restart from Settings › Updates; a version log in both languages.
- Gemini CLI as a third local provider (preview).
- Bundled World 0 cognitive kernel 0.5.1; conflict hints in recall only flag real reversals.
- The settings button is a gear; the sidebar no longer shows the version number.

See [CHANGELOG.en.md](CHANGELOG.en.md) for every version (Chinese: [CHANGELOG.md](CHANGELOG.md)).

## Feedback

Open an [issue](https://github.com/redbson/facewall-releases/issues). Please describe what happened rather than pasting your own traces.

## Disclaimer

Facewall is an independent project and is not affiliated with Anthropic, OpenAI or Google. Claude, Claude Code, Codex, Gemini and related marks are trademarks of their respective owners and are used only to identify the services Facewall can connect to.
