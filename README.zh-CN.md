# Facewall

[English](README.md) | 简体中文

[![最新版本](https://img.shields.io/github/v/release/redbson/facewall-releases?label=release)](https://github.com/redbson/facewall-releases/releases/latest) [![平台](https://img.shields.io/badge/platform-macOS%2013%2B%20%C2%B7%20Apple%20silicon-555)](#要求)

Facewall 是一个本地优先、AI-native 的 **macOS 思考墙**。想法刚出现时就从任何 App 里随手丢进去；后台的 AI 把它和你过去的想法连起来，缝进持续生长的 **思考线**，发现你 **改变了主意**，让反复出现的判断浮现为 **长期模式**，并在你重新思考一个问题时 **召回过去的自己**。它通过本机的模型路由器 **OntoRouter** 调用模型，由路由器在背后的服务（本机命令行工具或 API）中挑选并自动切换。没有服务器、不用注册账号：你的想法存在 Mac 上的一个数据库里，只有路由器发往的模型会看到它们。界面有中文和英文，默认跟随 Mac 的系统语言，可在设置里切换。

**⬇ 下载：[macOS](https://github.com/redbson/facewall-releases/releases/download/v0.3.6/Facewall-0.3.6.dmg)** · [全部版本](https://github.com/redbson/facewall-releases/releases) · [更新日志](CHANGELOG.md)

这个仓库放安装包、更新日志和文档；源码是私有的。

## 功能

- **随处捕捉**：全局快捷键（⌥⇧Space）在任何 App 上方弹出一个小浮窗，不抢当前 App 的焦点，回车就放到墙上。也可以从服务菜单（选中文字 → **存入 Facewall**）、菜单栏图标、Dock，以及给快捷指令、Raycast、Alfred 用的 `facewall://` URL scheme 捕捉。引擎没就绪时，捕捉会先存在本机、稍后送达——想法永远不会丢。
- **缝合**：每条线索都在后台缝合：归进一条思考线（新建或已有）、连到相关的过去线索并给出每条连接的理由、更新这条线当前的判断。Facewall 从不按规则瞎猜连接；没有 AI 时线索只是标为「待缝合」，接上模型后自动补缝。
- **观点反转**：新想法和过去的判断矛盾时，缝合会指出来，旧判断失效而不是被删掉，反转在墙上和思考线的历史里都有标记。「不是反转」可以撤销。
- **改了就算数**：把线索移到别的思考线、拆分或合并思考线、把连接标成错的、改写判断、重命名或合并概念。之后的缝合会尊重你的修改；你亲手写的判断永远不会被覆盖——AI 的新说法只作为建议出现。
- **召回**：问一个问题（⌘F），Facewall 找回你自己过去的话，带日期、逐步引用，给出此刻最站得住的判断和它的演化。它会说明自己有多大把握；过去没想过的，直接告诉你，不编造。
- **记忆与遗忘**：跨思考线反复出现的判断会成为长期模式，但要有足够证据（至少 3 条线索、跨 2 条思考线、跨 2 天）才转正——不是你的，可以否决。很久没被想起的线索会自己淡去，被打开或连接时立刻回来；也可以主动让一条线索淡去，或把它唤醒。
- **每日一针**：每天一张卡片——一条旧想法、一条思考线或一个未决问题，配一个提问。可以当场回应、从它发起召回、换一张，或今天跳过。
- **三个视图**：**思考墙**（线索按思考线分组、语义布局、标出反转）、**思考线**（每条线的判断历史和线索）、**记忆**（模式、概念、已淡去和已隐藏的线索）。
- **模型走 OntoRouter**：所有模型调用都按任务名发给本机的 OntoRouter（召回默认 语义分析/高，缝合默认 语义分析/中，自动选好）。背后用哪些服务——Claude Code、Codex 还是某个 API——在 OntoRouter 里设置，不在 Facewall 里。故障按类别区分（路由器没开、配额、认证、配置错误），缝合会自己恢复。
- **本地优先**：一个 SQLite 文件、每日备份、应用内恢复、完整的 JSON 导出导入，没有遥测。App 自带 Python 运行时和嵌入模型，除了调用模型，完全离线。
- **自动更新**：Facewall 会检查 GitHub Releases 上的新版本，校验后安装，见 [自动更新](#自动更新)。

## 要求

- macOS 13 或更新，Apple silicon。没有 Intel 版本。
- 本机运行着 OntoRouter（ontorouter 应用，或 `ontorouter serve`；默认地址 `http://127.0.0.1:4141`），并至少启用了一个服务。
- 别的都不需要：Python 和嵌入模型都在 App 里。

内置嵌入模型以中文为主；英文线索的召回能用，但偏弱。

## 安装

1. 下载 [Facewall-0.3.6.dmg](https://github.com/redbson/facewall-releases/releases/download/v0.3.6/Facewall-0.3.6.dmg)（或在 [Releases](https://github.com/redbson/facewall-releases/releases) 选一个版本），打开后把 `Facewall.app` 拖进「应用程序」。
2. 首次打开：Facewall 没有经过 Apple 公证，macOS 会说无法验证开发者。打开 系统设置 → 隐私与安全性，拉到底部点 **「仍要打开」**，或者在终端执行：

   ```bash
   xattr -dr com.apple.quarantine /Applications/Facewall.app
   ```

3. 之后的版本由 Facewall 自己下载安装（见 [自动更新](#自动更新)），不会再出现这个提示。
4. 打开 Facewall，引擎大约 2 秒就绪。OntoRouter 在运行时，Facewall 会在默认地址找到它并自动选好任务名；**⌘,** › AI 模型 显示路由器状态，可以测试连接。
5. 在任何 App 里按 **⌥⇧Space**，写下一个想法，回车。

要让 Facewall 开机自启，在 设置 › 外观与通用 里打开 **登录时启动**，它会常驻菜单栏，随时可以捕捉。

想先感受一下？在空墙上用 ⌘K 命令面板运行 **载入示例线索**。示例都有标记，不算你的话，一键就能清除。

## 自动更新

- Facewall 启动后不久和之后每 12 小时检查一次 GitHub 上的最新版本。不发送墙上的任何内容；检查可以关掉。
- 有新版本时，**设置 › 更新** 和侧栏底部会提示，并显示更新内容。**下载并安装** 会下载 dmg，核对它的 SHA-256 校验和、包标识、版本号和代码签名，全部一致才暂存新版；**重启并更新** 把它换进去并重新打开 Facewall。下载好但没重启的，下次退出时安装。
- **自动下载更新** 会在后台完成下载和校验，退出时安装。
- 如果 Facewall 是从安装盘、macOS 的隔离位置或一个你没有写入权限的文件夹里运行的，它无法替换自己，会指引你去发布页。
- 从 0.3.2 及更早版本升级，需要手动装一次 0.3.3；之后的版本都在应用内升级。

## 文档

- [使用指南](docs/guide.zh-CN.md)——捕捉、缝合、修正、召回、每日一针、思考线与记忆、设置、快捷键。
- [数据与隐私](docs/privacy.zh-CN.md)——数据在哪、哪些会发给模型、哪些永远不出你的 Mac。
- [排查问题](docs/troubleshooting.zh-CN.md)——首次打开、模型配置、缝合暂停、更新、备份。
- [更新日志](CHANGELOG.md)——每个版本的详细改动（[English](CHANGELOG.en.md)）。每个安装包的校验和在 [checksums/](checksums/)。
- [当前状态与路线图](docs/STATUS.md)——哪些能用、哪些还粗糙、接下来做什么。

## 更新日志

### 0.3.6
- 所有模型调用只走 OntoRouter：去掉了 API 和本机命令行工具的配置，旧版本保存的 key 在升级时删除。

### 0.3.5
- 模型调用可以走本机的 OntoRouter：填任务名，由路由器挑模型并自动切换；联网召回由路由器搜索。
- 手机记录入口（预览）：经中继服务器送到 Mac，端到端加密。

每个版本的详细改动见 [CHANGELOG.md](CHANGELOG.md)（English：[CHANGELOG.en.md](CHANGELOG.en.md)）。

## 反馈

请在本仓库开 [Issue](https://github.com/redbson/facewall-releases/issues)——描述现象即可，不要贴自己的线索原文。

## 声明

Facewall 是独立项目，与 Anthropic、OpenAI、Google 没有隶属关系。Claude、Claude Code、Codex、Gemini 及相关标识是各自所有者的商标，这里只用来指代 Facewall 可以连接的服务。
