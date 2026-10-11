# skills

林昊的 agent skills 个人仓：自创 skill 与高频使用件的收敛管理。

## 结构

- `skills/`：自创 skill（唯一事实源在本仓，迭代经 PR/commit 管理）
- `curated/`：高频使用的第三方 skill（标注来源与版本，仅作个人精选镜像，不回上游）
- 团队共享 skill 在 [dev-skills 仓](https://dev.msh.team/engineering/playground/dev-skills)（内部 GitLab），本仓不复制

## 收录

### skills/（自创）

| skill | 一句话 | 版本 |
|---|---|---|
| [frontend-design](skills/frontend-design) | 前端设计功底与两触点对齐流程（不定死风格；环节地图+实例驱动元迭代） | v1.0（2026-09-30） |
| [workwiki](skills/workwiki) | 工作知识库的读取与维护（归档碎片、恢复上下文、沉淀 SOP） | — |

### curated/（高频第三方，标注来源）

来自 [mattpocock/skills](https://github.com/mattpocock/skills)（Matt Pocock 工程 skill 集），镜像日期 2026-09-30：

| skill | 用途 |
|---|---|
| code-review | 按 Standards+Spec 双轴 review 分支/PR |
| diagnosing-bugs | 疑难 bug 与性能回归的诊断循环 |
| domain-modeling（未收，见 dev-skills） | — |
| grilling | 对计划/决策/想法做压力提问 |
| handoff | 交接文档生成 |
| prototype | 一次性原型回答设计问题 |
| research | 基于高信源调研并落 Markdown |
| tdd（未收） | — |
| writing-for-agents | 写给 agent 消费的文档（skill/AGENTS.md 写作规范） |

## 管理约定

1. **一 skill 一家**：本仓 `skills/` 的改动只在本仓进行；`curated/` 只镜像不改内容，需要改就移入 `skills/` 并改标注为自创 fork。
2. **实例驱动迭代**：skill 用出问题，先定位环节/规则再补反例（带日期+场景+原话），规则只增不删、失效标 superseded；版本与变更记各 skill 的 CHANGELOG。
3. **新增 skill**：自创进 `skills/`，第三方精选进 `curated/` 并补来源行；同步更新本 README 索引。

## 部署

各使用环境按需同步：`/root/.agents/skills/`（nika pod）、Mac 本地技能目录。同步方式：clone 本仓后拷贝对应目录，或以 git sparse-checkout 按需拉取。
