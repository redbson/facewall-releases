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

**Looking on the web too** (off by default): turn on Settings › AI model › Web search, and a *Look on the web too* box appears under the question. Ticked, the model searches the internet itself before answering (Claude Code, Codex or the Anthropic API — no search service to set up) and lists what it used under *From the web*, kept apart from your own past: a web result never appears in your path of thought. Only your question is sent to the search, never your traces.

## The Daily Stitch

When the Stitch page is idle, a card shows one older thought, thread or open question with a question. **Write a reply**, **Recall my past self**, **Another one**, or **Not today**. Examples and faded traces never appear in it.

## Threads and Memory

- **Threads** (⌘2): each thread's traces, its current judgment and how it changed, with reversals and "changed my mind" marked; edit, split, merge, or export one as Markdown (⌘E).
- **Memory** (⌘3): long-term patterns with their evidence (watching until promoted), concepts by maturity, and the faded and hidden traces with **Wake** and **Restore**.
- On the wall: ⌘⌫ deletes the selected trace, or hide it, or let it fade. A deleted or hidden trace never reappears anywhere — including the judgments, concepts and patterns derived from it — and is never sent to the model again.

## Settings (⌘,)

- **AI model**: provider, model, connection test, and the one-click cards for local CLIs. Stitching can use a cheaper model than recall.
- **Appearance & general**: light / dark / follow system with four dark styles; language (English, 简体中文, follow system); launch at login; menu bar and Dock icons; notifications and whether they carry text.
- **Shortcuts**: the two global hotkeys (quick capture, show / hide Facewall) and a reference of everything else.
- **Data & engine**: data folder (show, change), export and import, backups and in-app restore, usage counters, the cognitive kernel, logs, restart engine.
- **Updates**: current version, check / download / install, the two automatic switches, and the version log.

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
