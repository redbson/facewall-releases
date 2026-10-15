# Facewall

English | [简体中文](README.zh-CN.md)

[![Latest release](https://img.shields.io/github/v/release/redbson/facewall-releases?label=release)](https://github.com/redbson/facewall-releases/releases/latest) [![Platform](https://img.shields.io/badge/platform-macOS%2013%2B%20%C2%B7%20Apple%20silicon-555)](#requirements)

Facewall is a local-first, AI-native **thinking wall for macOS**. Drop a thought the moment it appears, from any app; an AI in the background links it to what you thought before, stitches it into **threads** that keep growing, notices when you **change your mind**, lets judgments that keep recurring surface as **patterns**, and **recalls your past self** when you come back to a question. It stitches through the **Claude Code**, **Codex** or **Gemini CLI** you are already signed in to, or any API you configure. There is no server and no account: your thoughts live in one database on your Mac, and only the model you chose ever sees them. The interface is in English and Chinese; it follows your Mac's language and can be switched in Settings.

**⬇ Download: [macOS](https://github.com/redbson/facewall-releases/releases/download/v0.3.3/Facewall-0.3.3.dmg)** · [All releases](https://github.com/redbson/facewall-releases/releases) · [Changelog](CHANGELOG.en.md)

This repository holds the installers and the changelog; the source code is private.

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

1. Download [Facewall-0.3.3.dmg](https://github.com/redbson/facewall-releases/releases/download/v0.3.3/Facewall-0.3.3.dmg) (or pick a version on [Releases](https://github.com/redbson/facewall-releases/releases)), open it, and drag `Facewall.app` into Applications.
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

## Usage

### Dropping traces

- **On the wall**: ⌘N or the composer at the bottom; ⌘↩ puts the text on the wall. One thought per trace, half-formed is fine. Up to 20,000 characters.
- **Quick capture panel**, from any app with ⌥⇧Space (changeable under Settings › Shortcuts): ↩ puts it on the wall and closes; ⌥↩ keeps the panel open for the next one; ⌘↩ opens Facewall; ⇧↩ new line; ⇥ switches to recall; Esc closes. With a Pinyin or Zhuyin input method, Return picks a candidate and never submits by mistake.
- **Elsewhere**: select text in any app → right-click → Services → **Save to Facewall** (bind a shortcut under System Settings › Keyboard › Keyboard Shortcuts › Services); the menu bar icon and the Dock icon's menu; `facewall://capture?text=…` to drop a trace silently, `facewall://quick` to open the panel, `facewall://recall?q=…` to recall.
- A system notification tells you when a thought captured outside the window has been stitched; by default it carries no text.

### Reading a stitch

Select a trace and the inspector's **Stitch** page shows: the thread it was filed under, the reversal it found (if any), the past thoughts it was linked to with a reason for each, the thread's judgment after this trace, an emerging pattern if the model flagged one, the AI's full reasoning, and a **Next stitch** question you can answer in place or recall from. The status at the top right shows what the AI is doing (ready, stitching, not configured, paused and why); ⇧⌘S stitches everything pending.

### When the AI gets it wrong

| | |
|---|---|
| **This link is off** | Downweights and deactivates a link; it disappears from the wall and from recall. |
| **Not a reversal** | The earlier judgment the AI retired comes back. |
| **Move…** | Puts the trace on the right thread or starts a new one; later stitches won't move it back. **Split into a new thread** takes a different matter out of a thread; merges ask first and can be undone for 10 minutes. |
| **Edit** (Threads) | Rewrite the title or the judgment. Your judgment is marked and never rewritten; the AI's new wording appears as a suggestion to adopt or ignore. |
| **Not my pattern** (Memory) | Rejects a long-term pattern; it can be restored later. |
| **Rename a concept** (Memory) | Renaming to an existing name merges the two. |

Every correction is a signal: whatever the AI infers, you have the final say.

### Recall

Press ⌘F (or `/` when you aren't typing), write what you want to keep thinking about, press Return. Ask the way you would ask someone who knows you: *What did I go back and forth on about moving to another city?* The result starts with how sure it is, then the most stable judgment right now, how the view changed over time (each step jumps to its trace), open questions, related threads, the recalled words themselves — dated, in your own words — and folded groups for nearest-but-unsure and faded traces. **Keep thinking from here** turns your reply into a new trace.

### The Daily Stitch

When the Stitch page is idle, a card shows one older thought, thread or open question with a question. **Write a reply**, **Recall my past self**, **Another one**, or **Not today**. Examples and faded traces never appear in it.

### Threads and Memory

- **Threads** (⌘2): each thread's traces, its current judgment and how it changed, with reversals and "changed my mind" marked; edit, split, merge, or export one as Markdown (⌘E).
- **Memory** (⌘3): long-term patterns with their evidence (watching until promoted), concepts by maturity, and the faded and hidden traces with **Wake** and **Restore**.
- On the wall: ⌘⌫ deletes the selected trace, or hide it, or let it fade. A deleted or hidden trace never reappears anywhere — including the judgments, concepts and patterns derived from it — and is never sent to the model again.

### Settings (⌘,)

- **AI model**: provider, model, connection test, and the one-click cards for local CLIs. Stitching can use a cheaper model than recall.
- **Appearance & general**: light / dark / follow system with four dark styles; language (English, 简体中文, follow system); launch at login; menu bar and Dock icons; notifications and whether they carry text.
- **Shortcuts**: the two global hotkeys (quick capture, show / hide Facewall) and a reference of everything else.
- **Data & engine**: data folder (show, change), export and import, backups and in-app restore, usage counters, the cognitive kernel, logs, restart engine.
- **Updates**: current version, check / download / install, the two automatic switches, and the version log.

### Shortcuts

| | |
|---|---|
| ⌥⇧Space · ⌥⇧W | Quick capture · show / hide Facewall (global, changeable) |
| ⌘N · ⌘↩ | New trace · put it on the wall |
| ⌘F · `/` | Recall |
| ⌘K | Command palette: commands, threads, and the text of your traces (searched locally) |
| ⌘1 · ⌘2 · ⌘3 | Wall · Threads · Memory |
| ⌥⌘I · ⌃⌘S | Inspector · sidebar |
| ⌘L · ⇧⌘L · ⌘0 | Re-layout · collapse threads · fit the wall |
| ⇧⌘S | Stitch all pending traces |
| ⌘⌫ | Delete the selected trace |
| ⇧⌘E · ⌘E · ⌘O | Export everything · export this thread · import |
| ⌘, · ⌘/ · ⌘? | Settings · shortcuts · user guide |

## Data and privacy

| What | Where |
|---|---|
| Your wall | `~/Library/Application Support/Facewall/Data/facewall.db` — every trace, link, judgment, pattern and vector in one SQLite file. The folder can be moved from Settings › Data & engine. |
| Backups | `…/Data/backups/` — one a day for the last 7 days, the last 5 manual ones, plus one before every upgrade, import and restore. Restore from any of them in Settings. |
| Model configuration | `…/Data/llm_config.json`, readable by you alone. Keys are never sent back to the interface. |
| Captures waiting for the engine | `~/Library/Application Support/Facewall/outbox.jsonl` |
| Logs | `~/Library/Logs/Facewall/app.log` and `engine.log` (Help › Open logs) |

- What reaches the model you configured, and nothing else: the trace being stitched, its few most related past traces, and the judgments of the threads involved; for recall, your question and the recalled traces. OpenAI and Azure requests ask the server not to store them.
- Everything else is local: search in the command palette, the embedding model, the layout, the usage counters, update checks (which only ask GitHub for the latest version number).
- ⇧⌘E exports everything as JSON with the text verbatim; ⌘O imports it. Files Facewall writes are readable by you alone.
- The quick capture panel, the Services menu and system notifications never show text by default; a notification is withdrawn when its trace is deleted.

## Troubleshooting

- **macOS won't open the app**: see step 2 of [Installation](#installation). The prompt appears only for a manually installed copy; in-app updates don't trigger it.
- **"No AI configured" at the top right**: click it. If `claude`, `codex` or `gemini` is on this Mac but not found, run it once in Terminal and sign in, or enter its path under Settings › AI model.
- **"Stitching paused"**: the status says why — quota used up, signed out, network down, or a misconfigured model — and when it retries. ⇧⌘S retries right away; a misconfigured model takes you to settings.
- **A capture was refused**: the panel (or a notification) says why, usually a text over 20,000 characters, and lets you copy the text back.
- **The engine won't start or stopped answering**: Help › **Restart engine**, then Help › **Open logs** for `engine.log`. A hung engine restarts by itself; two copies of Facewall never open the same data folder.
- **An update failed**: Settings › Updates shows the reason. You can always download the latest dmg from [Releases](https://github.com/redbson/facewall-releases/releases/latest) and install it over the old one; your data, settings and backups are kept.
- **Something looks wrong after an upgrade**: Settings › Data & engine › backups lists the copy made right before it; restoring makes another backup first.

## Changelog

### 0.3.3
- In-app updates: check, download, verify and restart from Settings › Updates; a version log in both languages.
- Gemini CLI as a third local provider (preview).
- Bundled World 0 cognitive kernel 0.5.1; conflict hints in recall only flag real reversals.
- The settings button is a gear; the sidebar no longer shows the version number.

### 0.3.2
- English and Chinese interface and model output, following the device language.

### 0.3.1
- Your judgments are never overwritten; deleted traces disappear everywhere; recall says how sure it is and abstains honestly; forgetting and waking; in-app restore of backups; corrections (move, split, merge, reject a pattern).

### 0.3.0
- Heteronto design system, user guide, About panel; automatic model lists; Claude Code / Codex as providers; the Daily Stitch.

See [CHANGELOG.en.md](CHANGELOG.en.md) for every version (Chinese: [CHANGELOG.md](CHANGELOG.md)).

## Feedback

Open an [issue](https://github.com/redbson/facewall-releases/issues). Please describe what happened rather than pasting your own traces.

## Disclaimer

Facewall is an independent project and is not affiliated with Anthropic, OpenAI or Google. Claude, Claude Code, Codex, Gemini and related marks are trademarks of their respective owners and are used only to identify the services Facewall can connect to.
