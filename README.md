# Facewall · 版本记录与发布

> 把碎片化思绪缝成一张可操作的私人思考墙。

Facewall 是一个 **本地优先、AI-native 的 macOS 思考墙**：想法刚出现时随手丢进去（**线索**），
后台的认知 Agent 自动归类、连接、缝合成持续生长的 **思考线**，识别你 **观点的反转**，
长期重复的判断浮现为 **模式**，再次思考时 **召回过去的自己**。

核心循环：`线索 → 缝合 → 思考线 → 模式 → 召回`，外加每天一张的 **每日一针**。

这个仓库只放 **更新日志、现状说明和安装包**；源码在私有仓库里维护。

- 📦 **下载**：[Releases](https://github.com/redbson/facewall-releases/releases)
- 📝 **更新日志**：[CHANGELOG.md](CHANGELOG.md)
- 📍 **当前状态与路线图**：[docs/STATUS.md](docs/STATUS.md)

---

## 安装

**要求**：macOS 13 或更新，Apple Silicon（M 系列）。目前只提供简体中文界面，AI 输出也是中文。

1. 从 [Releases](https://github.com/redbson/facewall-releases/releases) 下载最新的 `Facewall-<版本>.dmg`，打开后把 **Facewall.app** 拖进「应用程序」。
2. 安装包是 **ad-hoc 签名、未公证** 的，第一次打开前需要去掉隔离标记（只需一次）：

   ```bash
   xattr -dr com.apple.quarantine /Applications/Facewall.app
   ```

3. 打开 Facewall。引擎约 2 秒就绪，数据保存在 `~/Library/Application Support/Facewall/Data`。
4. 按 **⌘,** 连接 AI：
   - 本机装了 **Claude Code** 或 **Codex** 的话，设置页会直接推荐「一键启用」，走你已有的订阅，不需要 API key；
   - 也可以填 Anthropic / OpenAI / Azure，或任何 OpenAI 兼容端点（DeepSeek、Kimi、GLM、Qwen、Ollama 等预设）。
5. 在任何 App 里按 **⌥⇧Space**，写下一个想法，回车。

App 自带独立的 Python 运行时和中文嵌入模型，除了调用你配置的模型外 **完全离线**；没有服务器，不上传任何数据。

## 日常入口

| 入口 | 怎么用 |
|---|---|
| 快速捕捉浮窗 | 任何 App 里 ⌥⇧Space（不抢焦点）；↩ 放下，⌥↩ 放下并继续，⌘↩ 放下并打开墙，⇥ 切到召回 |
| 服务菜单 | 选中文字 → 右键 → 服务 → **存入 Facewall** |
| 菜单栏图标 | 快速捕捉、继续思考、待缝合计数、最近线索 |
| URL scheme | `facewall://capture?text=…`、`facewall://recall?q=…`、`facewall://trace/<id>` |
| 终端 | `fw 一句想法`、`pbpaste \| fw`、`fw -r 问题`（脚本随源码提供） |

应用内 **⌘K** 命令面板、**⌘F** 召回、**⌘?** 使用帮助。

## 数据与隐私

- 所有数据在本机一个 SQLite 文件里；**⇧⌘E** 导出完整 JSON（原文逐字保留），**⌘O** 导入。
- 每天自动备份（保留 7 天），升级、导入、恢复前也先备份；在 设置 › 数据与引擎 里可以直接恢复到任一份。
- 删除 / 隐藏的线索不会再以任何形式出现（包括由它派生的判断、概念和模式），也不再发给模型。
- 「让它淡去」：原文留在墙上，但不再被召回、推送或连接；随时唤醒。
- 发给模型的内容只有：当前线索与它最相关的几条历史原文、涉及的思考线判断；系统通知默认不显示原文。
- 本机使用统计只记录在数据目录里，不上传。

## 反馈

问题和建议请在本仓库开 [Issue](https://github.com/redbson/facewall-releases/issues)。
请不要在 Issue 里贴自己的线索原文——描述现象即可。
