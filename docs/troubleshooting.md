# Troubleshooting

English | [简体中文](troubleshooting.zh-CN.md)

The problems you may meet and what to do. Still stuck? Open an [issue](https://github.com/redbson/facewall-releases/issues) and describe what happened (no need to paste your traces).

- **macOS won't open the app**: see step 2 of [Installation](../README.md#installation). The prompt appears only for a manually installed copy; in-app updates don't trigger it.
- **"Stitching paused" because OntoRouter isn't running**: open the ontorouter app or run `ontorouter serve`; stitching resumes by itself. If the router listens somewhere other than `http://127.0.0.1:4141`, enter its address under Settings › AI model. A 401 means the router has a key set: enter it there too.
- **"Stitching paused"**: the status says why — router not running, quota used up, signed out, or a misconfigured task name — and when it retries. ⇧⌘S retries right away; a misconfigured model takes you to settings.
- **A capture was refused**: the panel (or a notification) says why, usually a text over 20,000 characters, and lets you copy the text back.
- **The engine won't start or stopped answering**: Help › **Restart engine**, then Help › **Open logs** for `engine.log`. A hung engine restarts by itself; two copies of Facewall never open the same data folder.
- **An update failed**: Settings › Updates shows the reason. You can always download the latest dmg from [Releases](https://github.com/redbson/facewall-releases/releases/latest) and install it over the old one; your data, settings and backups are kept.
- **Something looks wrong after an upgrade**: Settings › Data & engine › backups lists the copy made right before it; restoring makes another backup first.
