# Facewall

[English](README.md) | 简体中文

[![release](https://img.shields.io/github/v/release/redbson/facewall-releases?label=release&color=e8743b)](https://github.com/redbson/facewall-releases/releases/latest) [![platform](https://img.shields.io/badge/platform-macOS%2013%2B%20%C2%B7%20Apple%20Silicon-555)](#安装)

Facewall 是一个本地优先、AI-native 的 **macOS 思考墙**：想法刚出现时随手丢进去，后台的 AI 把它和你过去的想法连起来，
缝进持续生长的 **思考线**，发现你 **改变了主意**，并在你重新思考一个问题时 **召回过去的自己**。它可以用你已有订阅的
**Claude Code**、**Codex** 或 **Gemini CLI** 缝合，也可以接你配置的任何 API——没有服务器，墙上的内容除了模型需要的部分，
不会离开你的 Mac。界面有中文和英文，默认跟随 Mac 的系统语言，可在设置里切换。

⬇️ **下载：** [macOS](https://github.com/redbson/facewall-releases/releases/download/v0.3.3/Facewall-0.3.3.dmg) · [全部版本](https://github.com/redbson/facewall-releases/releases) · [更新日志](CHANGELOG.md)

## 安装

要求 macOS 13 或更新、Apple Silicon。

1. 从 [Releases](https://github.com/redbson/facewall-releases/releases) 下载最新的 `Facewall-<版本>.dmg`，把 **Facewall.app** 拖进「应用程序」。
2. 安装包是 ad-hoc 签名、未公证的，第一次打开会被 macOS 拦下。任选一种办法，只需一次：终端执行

   ```bash
   xattr -dr com.apple.quarantine /Applications/Facewall.app
   ```

   或者被拦下后在 **系统设置 › 隐私与安全性** 里点 **「仍要打开」**。
3. 打开 Facewall，按 **⌘,** 连接模型。本机装了 **Claude Code** 或 **Codex** 时可以一键启用，走你已有的订阅，不需要
   API key；也支持 Gemini CLI（预览）、Anthropic、OpenAI、Azure 和 OpenAI 兼容端点（DeepSeek、Kimi、GLM、Qwen、Ollama 等）。

**更新：** 从 0.3.3 起，Facewall 可以在应用内升级——**设置 › 更新**（或菜单 **Facewall › 检查更新…**）。

## 怎么用

1. **想到就放下。** 在任何 App 里按 **⌥⇧Space**，写下来，回车。一条线索只放一个想法；没想完也没关系——不用整理，
   用自己的话写下你此刻的想法就好。
2. **交给它缝合。** 每条线索都会在后台缝合：归进哪条 **思考线**、连到哪些过去的线索、为什么，以及这条线当前的核心判断。
   选中一条线索，右栏就能看到它的缝合结果。
3. **缝错了就改。** 把线索移到别的思考线、把某条连接标成错的、改写思考线的判断、拆分或合并思考线。之后的缝合会尊重
   你的修正；你亲手写的判断永远优先。
4. **看见自己怎么变。** **思考墙**（⌘1）按思考线收起线索，并标出观点反转；**思考线**（⌘2）里能看到每个判断是怎么
   演化的、在哪里改变过主意。
5. **用召回继续思考。** 按 **⌘F** 问一个问题：Facewall 找回你以前的想法，逐步引用你自己的原话；过去没想过的，它会
   直接告诉你。
6. **每天回来一次。** **每日一针** 每天带回一条旧想法和一个问题。几周之后，跨思考线反复出现的判断会作为长期模式出现在
   **记忆**（⌘3）里——不是你的，就点「这不是我的模式」。

想先感受一下？在空墙上用 ⌘K 命令面板运行「载入示例线索」，看完一键清除。

## 快捷键与入口

| | |
|---|---|
| ⌥⇧Space | 任何 App 里快速捕捉（⇥ 切到召回） |
| ⌘K · ⌘F · ⌘? | 命令面板 · 召回 · 使用帮助 |
| 服务菜单 | 选中文字 → 右键 → 服务 → **存入 Facewall** |
| 菜单栏图标 | 快速捕捉、继续思考、待缝合计数、最近线索 |
| URL scheme | `facewall://capture?text=…` · `facewall://recall?q=…` |

## 数据与隐私

- 所有数据都在本机的一个 SQLite 文件里，没有服务器。**⇧⌘E** 导出完整 JSON，**⌘O** 导入。
- 每天自动备份（保留 7 天），在 设置 › 数据与引擎 里可以恢复到任意一份。
- 只有你配置的模型会看到内容：当前线索、与它最相关的几条过去的线索，以及涉及的思考线判断。
- 检查更新只向 GitHub 询问最新版本号，不带墙上的任何内容（可以关掉）。
- 删除或隐藏的线索不会再出现，也不再发给模型；「让它淡去」保留原文，但不再召回。

## 反馈

请在本仓库开 [Issue](https://github.com/redbson/facewall-releases/issues)——描述现象即可，不要贴自己的线索原文。
