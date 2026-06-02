# CHANGELOG

> 格式：feat(scope): 描述 → 新增
>       fix(scope): 描述  → 修复
>       refactor:   描述  → 重构

## 2026-06-02

### 新增
- docs(codex): 增加 Codex CLI 命令、slash commands、全局参数和常用工作流中文参考
- docs(agents): 增加 Wiki 大主题拆分与分层导航维护规则
- docs(readme): 增加中文开源入口说明、目录用途、维护流程和分发注意事项
- docs(wiki): 增加来源索引与联动更新规则
- docs(skill): 增加 `wiki-knowledge-base` skill 草稿及通用 Wiki 模板
- config(git): 忽略本地代理目录和生成的压缩包

### 修复
- docs(agents): 将主题导航收敛到 `wiki/index.md`，`AGENTS.md` 只保留入口说明
- docs(readme): 将 README 标题和正文改为中文
- docs(progress): 更新开源检查、打包、README 和维护状态

### 重构
- docs(codex): 将 Codex CLI 命令参考拆分为主题总览页和子页面
- docs(state): 压缩项目状态文档，合并重复流水与过细中间过程

## 2026-05-29

### 新增
- docs(frontend): 补充列表标题与内容居中展示规范
- docs(frontend): 补充树形数据整行展开收起与展开状态保持规范
- docs(wiki): 沉淀 Wiki 数据量增长后的更新同步防遗漏方法
- docs(skill): 评估并创建 `wiki-knowledge-base` skill 草稿及通用 Wiki 模板

## 2026-05-27

### 新增
- docs(backend): 明确 Python 后端通过 SQLAlchemy 访问 PostgreSQL
- docs(frontend): 增加 Vue 3 与 TypeScript 前端专项规范及 FastAPI 协作要求

## 2026-05-26

### 新增
- docs(wiki): 建立 raw/wiki 结构并增加前端、通用一致性与日常知识入口
- docs(rules): 记录 `git push` 必须由用户明确授权
- docs(notes): 建立后端开发规范与 Codex 笔记维护指令
- docs(frontend): 明确 Vue 3 打包运行与本地调试的后端接口地址规则

### 重构
- docs(wiki): 将后端规范按 Python 技术栈重命名并保留旧路径兼容入口

### 初始化
- 创建项目文档结构（PROGRESS / DECISIONS / CHANGELOG）
