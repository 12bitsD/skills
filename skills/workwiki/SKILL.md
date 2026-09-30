---
name: workwiki
description: "读取和维护用户的 Work Wiki：归档工作碎片、恢复项目上下文、结合已存知识分析指令与 gap、沉淀工具 SOP。用户提到 workwiki、工作知识库或要求将本次工作记入 wiki 时使用；知识根目录固定，不随当前项目改变。"
---

# Work Wiki

固定知识根目录：`/Users/user/Desktop/workwiki`。从任意工作目录使用此根目录的绝对路径，勿在当前项目创建另一个 wiki。

1. 每轮首次访问 wiki 前，先执行 `python3 /Users/user/Desktop/workwiki/scripts/before-read.py --sync`，成功后读取 `/Users/user/Desktop/workwiki/AGENTS.md` 和 `/Users/user/Desktop/workwiki/INDEX.md`；若本轮 hook 已成功同步可省略。同步失败则暂停读取并报告原因。如果根目录无法访问，说明路径与限制，不把失败当作空知识库。
2. 按当前请求走相应分支：
   - **查询 / 恢复 / 分析**：按名称、别名和关键词用 `rg -n -F --` 检索 `projects/`、`playbooks/`；需要证据才搜 `inbox/`。读取命中内容及来源，结合状态和时间回答，并链接所用文件。分析指令时先用已存上下文补事实缺口，再指出仍需用户决定的事项。
   - **记录 / 写回**：读取 `/Users/user/Desktop/workwiki/FORMAT.md`，按照其中的模板和来源约定保存本次相关碎片并整合项目知识。以 AGENTS.md 的规则决定自动写回或提出待确认决策。只归档当前授权任务相关内容。
   - **SOP**：检索已有流程；新建或改动操作规则按 AGENTS.md 的确认边界处理。执行 SOP 仍受当前请求和工具权限约束。
   - **定时跟进**：按 AGENTS.md 的日程规则调用当前环境实际提供的 Codex 能力；缺少能力时如实说明未创建。
3. 写入结束按协议验证来源、链接和导航；简短报告结果。没有新增知识的查询无需写入。

本 skill 仅在调用时工作，不会后台监听其他对话；将其他窗口的信息纳入 wiki 需要在那个窗口调用它或提供材料。本机文件对远程或云端会话不一定可见；权限受限时说明需要访问上述根目录。
