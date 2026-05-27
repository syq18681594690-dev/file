# DECISIONS

> 记录项目中重要的架构和技术决策，以及做出决策的原因。

## 模板
```
## YYYY-MM-DD：决策标题
**决策**：选择了 X
**原因**：xxx
**否决方案**：Y（原因：xxx）
**影响范围**：src/xxx
```

---

## 2026-05-26：项目初始化
**决策**：使用 PROGRESS / DECISIONS / CHANGELOG 三文件管理项目状态
**原因**：跨会话保持上下文，避免每次向 Claude 重新解释项目背景
**影响范围**：全项目

## 2026-05-26：将目录定位为开发规范笔记库
**决策**：使用 `AGENTS.md` 约束 Codex 将用户输入整理到对应开发规范文档，后端内容集中维护在 `BACKEND_DEVELOPMENT_GUIDE.md`
**原因**：本目录的主要目标是持续维护开发笔记，而非直接承载后端工程实现
**否决方案**：将后端技术约束直接作为本目录的工程实施指令（原因：会把记录需求误解为代码开发任务）
**影响范围**：`AGENTS.md`、`BACKEND_DEVELOPMENT_GUIDE.md`

## 2026-05-26：采用三层 LLM Wiki 结构维护开发规范
**决策**：建立 `raw/` 原始来源层、`wiki/` 知识整理层与 `AGENTS.md` 工作流层，以 `wiki/index.md` 和 `wiki/log.md` 维护导航与操作历史；将后端规范迁移至 `wiki/backend-development-guide.md`，根目录旧路径保留兼容入口
**原因**：让新增输入持续编入可导航、可追溯的规范库，而不是只在聊天中临时归纳
**否决方案**：继续将所有规范放在根目录的单独文件中（原因：缺少来源边界、索引与积累工作流）
**影响范围**：`raw/`、`wiki/`、`AGENTS.md`、后续规范维护流程

## 2026-05-26：跨页面功能一致性使用独立通用规范
**决策**：将前后端共同遵守的多页面功能一致性要求维护在 `wiki/cross-page-feature-consistency.md`，前端与后端主题页分别引用该通用规则
**原因**：同一功能的一致性要求需要单一来源，避免前后端页面分别维护后逐渐产生不同解释
**否决方案**：仅在前端和后端页面分别重复写入规则（原因：重复内容容易出现更新遗漏和规则分叉）
**影响范围**：`wiki/cross-page-feature-consistency.md`、`wiki/frontend-development-experience.md`、`wiki/backend-development-guide.md`

## 2026-05-26：增加日常知识通用入口
**决策**：使用 `wiki/daily-knowledge-notes.md` 积累暂不属于专项规范的开发知识，并在内容成熟为独立主题时拆分页面
**原因**：工具技巧和零散排查结论需要稳定入口，同时避免把不同主题硬塞入前端或后端规范
**否决方案**：将所有日常信息直接追加到现有专项页面（原因：会模糊主题边界并降低检索效率）
**影响范围**：`wiki/daily-knowledge-notes.md`、`wiki/index.md`、后续知识整理流程

## 2026-05-26：Git 推送必须由用户明确授权
**决策**：后端开发及本笔记库维护过程中均禁止自动执行 `git push`，仅在用户明确要求推送时执行
**原因**：远程推送会影响共享仓库状态，应由用户显式控制推送时机与目标
**否决方案**：在完成提交后自动推送远程仓库（原因：可能在用户尚未审核变更或未选择远端时发布内容）
**影响范围**：`AGENTS.md`、`wiki/backend-development-guide.md`、Git 操作流程

## 2026-05-26：后端规范按技术栈命名
**决策**：将现有规范的实际维护页面更名为 `wiki/python-backend-development-guide.md`，标题改为“Python 后端开发规范”；旧 Wiki 路径保留跳转入口
**原因**：现有规范限定 Python、FastAPI 与 Uvicorn，按技术栈命名可为其他语言或运行时的后端规范保留清晰入口
**否决方案**：继续使用泛化的“后端开发约定”名称（原因：后续引入其他后端技术栈时会混淆适用范围）
**影响范围**：`wiki/python-backend-development-guide.md`、`wiki/backend-development-guide.md`、Wiki 导航与交叉链接

## 2026-05-26：前端采用 Vue 3 专项规范
**决策**：将用户提出的 `Vu3` 按上下文规范为 `Vue 3`，新增 `wiki/vue3-frontend-development-guide.md` 并与 Python/FastAPI 后端规范建立协作约定
**原因**：Vue 3 已被指定为前端框架，专项页面可明确组件、状态、接口契约和联调规则，同时保留通用前端经验入口
**否决方案**：仅在通用前端经验页面中零散记录 Vue 3 要求（原因：无法清晰表达特定框架适用范围及后端协作规则）
**影响范围**：`wiki/vue3-frontend-development-guide.md`、`wiki/frontend-development-experience.md`、`wiki/python-backend-development-guide.md`

## 2026-05-26：Vue 3 使用 TypeScript
**决策**：Vue 3 前端开发使用 `TypeScript`，组件边界、共享逻辑和 API 请求响应均以显式类型表达
**原因**：用户明确指定 `ts`，且类型约定有助于前端与 FastAPI 已确认的请求响应结构保持一致
**否决方案**：在 Vue 3 专项规范中继续将 JavaScript 与 TypeScript 都列为待选项（原因：与已明确的用户要求冲突）
**影响范围**：`wiki/vue3-frontend-development-guide.md`、`wiki/frontend-development-experience.md`

## 2026-05-26：Vue 3 接口地址按运行模式解析
**决策**：打包运行时使用浏览器当前访问的协议、主机和端口，仅拼接 API 路径；本地开发调试时支持直接配置 FastAPI 接口地址
**原因**：避免构建产物绑定固定部署主机，同时满足本地联调连接指定后端环境的需要
**否决方案**：在前端页面或构建产物中写死后端接口完整地址或独立后端端口（原因：部署环境变化时不可复用且容易连错服务）
**影响范围**：`wiki/vue3-frontend-development-guide.md`、前端请求层与构建配置

## 2026-05-27：Python 后端使用 SQLAlchemy
**决策**：Python 后端使用 `SQLAlchemy` 访问 PostgreSQL 12
**原因**：用户明确指定数据库访问技术，需统一模型映射、会话与查询实现边界
**否决方案**：继续保留 ORM 或数据库访问方案未确定状态（原因：与用户已明确的技术选择冲突）
**影响范围**：`wiki/python-backend-development-guide.md`、后端依赖与数据访问实现
