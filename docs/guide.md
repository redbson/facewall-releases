# Facewall user guide

English | [简体中文](guide.zh-CN.md)

How to use Facewall day to day: capturing, reading a stitch, correcting the AI, recall, the Daily Stitch, threads and memory, settings and shortcuts. For installation see the [README](../README.md).

## Dropping traces

- **On the wall**: ⌘N or the composer at the bottom; ⌘↩ puts the text on the wall. One thought per trace, half-formed is fine. Up to 20,000 characters.
- **Quick capture panel**, from any app with ⌥⇧Space (changeable under Settings › Shortcuts): ↩ puts it on the wall and closes; ⌥↩ keeps the panel open for the next one; ⌘↩ opens Facewall; ⇧↩ new line; ⇥ switches to recall; Esc closes. With a Pinyin or Zhuyin input method, Return picks a candidate and never submits by mistake.
- **Elsewhere**: select text in any app → right-click → Services → **Save to Facewall** (bind a shortcut under System Settings › Keyboard › Keyboard Shortcuts › Services); the menu bar icon and the Dock icon's menu; `facewall://capture?text=…` to drop a trace silently, `facewall://quick` to open the panel, `facewall://recall?q=…` to recall.
- A system notification tells you when a thought captured outside the window has been stitched; by default it carries no text.

## Reading a stitch

Select a trace and the inspector's **Stitch** page shows: the thread it was filed under, the reversal it found (if any), the past thoughts it was linked to with a reason for each, the thread's judgment after this trace, an emerging pattern if the model flagged one, the AI's full reasoning, and a **Next stitch** question you can answer in place or recall from. The status at the top right shows what the AI is doing (ready, stitching, not configured, paused and why); ⇧⌘S stitches everything pending.

## When the AI gets it wrong

| | |
|---|---|
| **This link is off** | Downweights and deactivates a link; it disappears from the wall and from recall. |
| **Not a reversal** | The earlier judgment the AI retired comes back. |
| **Move…** | Puts the trace on the right thread or starts a new one; later stitches won't move it back. **Split into a new thread** takes a different matter out of a thread; merges ask first and can be undone for 10 minutes. |
| **Edit** (Threads) | Rewrite the title or the judgment. Your judgment is marked and never rewritten; the AI's new wording appears as a suggestion to adopt or ignore. |
| **Not my pattern** (Memory) | Rejects a long-term pattern; it can be restored later. |
| **Rename a concept** (Memory) | Renaming to an existing name merges the two. |

Every correction is a signal: whatever the AI infers, you have the final say.

## Recall

Press ⌘F (or `/` when you aren't typing), write what you want to keep thinking about, press Return. Ask the way you would ask someone who knows you: *What did I go back and forth on about moving to another city?* The result starts with how sure it is, then the most stable judgment right now, how the view changed over time (each step jumps to its trace), open questions, related threads, the recalled words themselves — dated, in your own words — and folded groups for nearest-but-unsure and faded traces. **Keep thinking from here** turns your reply into a new trace.

When **OntoRouter** is selected, turn on **Settings › AI model › Web search** to show a **Look on the web too** checkbox under your question. If you tick it, OntoRouter uses the question as the search query. The answer lists any sources it uses under **From the web**.

## Capturing from your phone

Facewall has no server, so the phone reaches your Mac through a **relay server** (preview: the relay has to be self-hosted and its package is not public yet). On the Mac open **Settings › Mobile**, enter the relay address and its invite code, click **Pair a phone** and scan the QR code with the phone camera; add the page to the home screen. The phone page is one box: write, tap, done — offline it queues and sends later. Every capture is encrypted on the phone with a key that travels only inside the QR code; the relay stores ciphertext, the Mac decrypts it, puts it on the wall as a `mobile` trace dated when you wrote it, and has the relay delete it. With the Mac off, captures wait on the relay for up to 30 days. **Unpair** revokes the phone; pairing again makes a new key.

## The Daily Stitch

When the Stitch page is idle, a card shows one older thought, thread or open question with a question. **Write a reply**, **Recall my past self**, **Another one**, or **Not today**. Examples and faded traces never appear in it.

## Threads and Memory

- **Threads** (⌘2): each thread's traces, its current judgment and how it changed, with reversals and "changed my mind" marked; edit, split, merge, or export one as Markdown (⌘E).
- **Memory** (⌘3): long-term patterns with their evidence (watching until promoted), concepts by maturity, and the faded and hidden traces with **Wake** and **Restore**.
- On the wall: ⌘⌫ deletes the selected trace, or hide it, or let it fade. A deleted or hidden trace never reappears anywhere — including the judgments, concepts and patterns derived from it — and is never sent to the model again.

## Settings (⌘,)

- **AI model.** Choose a provider and set models for recall and stitching. [AI model setup](#ai-model)
- **MCP.** Connect a local agent to readable Facewall notes. [Recall from an agent](#recall-from-an-agent)
- **Appearance & general**: light / dark / follow system with four dark styles; language (English, 简体中文, follow system); launch at login; menu bar and Dock icons; notifications and whether they carry text.
- **Shortcuts**: the two global hotkeys (quick capture, show / hide Facewall) and a reference of everything else.
- **Data & engine**: data folder (show, change), export and import, backups and in-app restore, usage counters, the cognitive kernel, logs, restart engine.
- **Updates**: current version, check / download / install, the two automatic switches, and the version log.

### AI model

1. Choose **OntoRouter**, **OpenAI**, **DeepSeek**, **Anthropic**, **Google Gemini**, **Azure OpenAI** or **OpenAI-compatible** in the provider menu. OntoRouter defaults to `http://127.0.0.1:4141`. Enter the API key for your selected service when required. For a compatible server, enter its full base URL, for example `http://localhost:11434/v1` for Ollama.
2. Use **Fetch models** to see available choices or enter the model ID. Use the deployment name for Azure OpenAI. OntoRouter can pick task names automatically when left blank.
3. Choose a main model for recall. Stitching and the Daily Stitch use the optional stitch model when one is set.
4. Select **Test connection** to validate the draft settings, then **Save** to activate them. Each provider keeps its own profile for when you switch back.

### Recall from an agent

Open **Settings › MCP**, choose a detected Codex, Claude Code, Qoder CLI or Gemini CLI client, and connect Facewall. The recall skill can be installed or removed separately. Start a new agent session after changing its setup.

Ask for evidence from your notes, for example, “Find what I wrote about automatic archiving. Cite the original notes and dates.” The read-only server can work while the app is closed. [Data and privacy](privacy.md)

## Shortcuts

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
