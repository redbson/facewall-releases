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

- 模型请求把相关上下文发往选定的端点。缝合时可能包含当前线索、相关历史线索和思考线判断。召回时可能包含你的问题和匹配的线索。选用 OntoRouter 时由路由器决定使用哪个模型。选用直连 API 时由 Facewall 向该端点发请求。
- 召回的联网搜索由 OntoRouter 提供，默认关闭。勾选联网参考时，路由器用你的问题作为搜索词。
- 可选的只读 MCP 连接会把可读取的线索和思考线返回给连接的代理。结果排除隐藏、删除、主动遗忘和示例线索。代理可能把返回的内容带入自己的模型请求。
- 命令面板搜索、嵌入模型、布局和使用统计在本地运行。更新检查向 GitHub 请求发布信息。
- ⇧⌘E 把全部数据导出为 JSON，原文逐字保留；⌘O 导入。Facewall 写的文件都只有你能读。
- 快速捕捉浮窗、服务菜单和系统通知默认不显示原文；线索删除后，它的通知会被撤回。
