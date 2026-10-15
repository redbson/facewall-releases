# Troubleshooting

English | [简体中文](troubleshooting.zh-CN.md)

The problems you may meet and what to do. Still stuck? Open an [issue](https://github.com/redbson/facewall-releases/issues) and describe what happened (no need to paste your traces).

- **macOS won't open the app**: see step 2 of [Installation](../README.md#installation). The prompt appears only for a manually installed copy; in-app updates don't trigger it.
- **"No AI configured" at the top right**: click it. If `claude`, `codex` or `gemini` is on this Mac but not found, run it once in Terminal and sign in, or enter its path under Settings › AI model.
- **"Stitching paused"**: the status says why — quota used up, signed out, network down, or a misconfigured model — and when it retries. ⇧⌘S retries right away; a misconfigured model takes you to settings.
- **A capture was refused**: the panel (or a notification) says why, usually a text over 20,000 characters, and lets you copy the text back.
- **The engine won't start or stopped answering**: Help › **Restart engine**, then Help › **Open logs** for `engine.log`. A hung engine restarts by itself; two copies of Facewall never open the same data folder.
- **An update failed**: Settings › Updates shows the reason. You can always download the latest dmg from [Releases](https://github.com/redbson/facewall-releases/releases/latest) and install it over the old one; your data, settings and backups are kept.
- **Something looks wrong after an upgrade**: Settings › Data & engine › backups lists the copy made right before it; restoring makes another backup first.
