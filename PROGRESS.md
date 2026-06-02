# PROGRESS

## 项目：zhaobiao

## 当前阶段
开发规范 Wiki 维护与状态文档压缩

## 已完成
- [x] 建立 Codex 开发规范 Wiki：`raw/` 原始资料层、`wiki/` 知识整理层、`AGENTS.md` 维护规则层，以及 `wiki/index.md` 和 `wiki/log.md` 工作流入口（2026-05-26）
- [x] 沉淀 Python/FastAPI 后端规范：Uvicorn、PostgreSQL 12、Redis、并发要求、SQLAlchemy 数据访问与 Git 推送授权规则（2026-05-26 至 2026-05-27）
- [x] 沉淀 Vue 3 + TypeScript 前端规范：组件、状态、接口契约、本地联调地址、打包接口地址、列表居中和树形展开状态保持规则（2026-05-26 至 2026-05-29）
- [x] 建立跨页面功能一致性、通用前端经验和日常知识积累入口，并记录 Wiki 数据量增长后的同步防遗漏方法（2026-05-26 至 2026-05-29）
- [x] 创建 `skills/wiki-knowledge-base/` skill 草稿及通用模板，评估将 Wiki 知识库维护流程抽象为 Codex skill（2026-05-29 至 2026-06-02）
- [x] 增加来源索引与联动更新规则，明确文章、书籍、原始文件与页面 frontmatter、`wiki/log.md` 的追溯关系（2026-06-02）
- [x] 完成开源准备：打包分发包、检查敏感信息风险、创建中文 `README.md`、增加本地文件忽略规则（2026-06-02）
- [x] 新增 Codex CLI 命令参考，并按分层导航规则拆分为总览页和 `wiki/codex-cli/` 子页面（2026-06-02）
- [x] 将 `AGENTS.md` 当前导航收敛为入口说明，主题清单统一维护在 `wiki/index.md`，并写入 Wiki 大主题拆分与分层导航规则（2026-06-02）
- [x] 压缩 `PROGRESS.md`、`DECISIONS.md`、`CHANGELOG.md`，保留仍影响后续维护的状态、决策和用户可感知变更摘要（2026-06-02）

## 进行中
- [ ] `wiki-knowledge-base` skill 草稿完善
  - 已完成：基础结构、通用模板、维护状态记录
  - 未完成：如用户确认方向，将来源索引规则和 Wiki 分层导航规则同步补充进 skill 模板

## 待开始
- [ ] 后续 Codex CLI 内容更新时，从 `wiki/codex-cli-command-reference.md` 入口进入对应子页面维护

## 下次会话从这里开始
- 文件：`skills/wiki-knowledge-base/SKILL.md`
- 位置：第 31 行 `Initialize` 流程
- 待完成：如用户确认方向，将来源索引规则和 Wiki 分层导航规则同步补充进 `wiki-knowledge-base` skill 模板；后续 Codex CLI 内容更新时从 `wiki/codex-cli-command-reference.md` 入口进入对应子页面
