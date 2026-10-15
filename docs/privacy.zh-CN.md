# 数据与隐私

[English](privacy.md) | 简体中文

Facewall 把你的数据放在哪里，哪些内容会离开你的 Mac。

| 什么 | 在哪 |
|---|---|
| 你的墙 | `~/Library/Application Support/Facewall/Data/facewall.db`——所有线索、连接、判断、模式和向量都在这一个 SQLite 文件里。目录可在 设置 › 数据与引擎 里更换。 |
| 备份 | `…/Data/backups/`——最近 7 天每天一份，最近 5 份手动备份，以及每次升级、导入、恢复前各一份。在设置里可以恢复到任意一份。 |
| 模型配置 | `…/Data/llm_config.json`，仅本人可读。key 永远不会回传到界面。 |
| 等待引擎的捕捉 | `~/Library/Application Support/Facewall/outbox.jsonl` |
| 日志 | `~/Library/Logs/Facewall/app.log` 和 `engine.log`（帮助 › 打开日志） |

- 只有这些会发给你配置的模型：正在缝合的线索、与它最相关的几条过去线索、涉及的思考线判断；召回时是你的问题和召回到的线索。OpenAI 和 Azure 的请求会要求服务端不保存。
- 联网搜索默认关闭；打开后也只有你勾选的那次召回会联网，模型用你的问题搜索，不用线索原文。缝合和每日一针从不联网。
- 其余全在本地：命令面板的搜索、嵌入模型、布局、使用统计、更新检查（只向 GitHub 问最新版本号）。
- ⇧⌘E 把全部数据导出为 JSON，原文逐字保留；⌘O 导入。Facewall 写的文件都只有你能读。
- 快速捕捉浮窗、服务菜单和系统通知默认不显示原文；线索删除后，它的通知会被撤回。
