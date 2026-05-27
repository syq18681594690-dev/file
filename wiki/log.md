---
title: Wiki 维护日志
type: log
updated: 2026-05-27
---

# Wiki 维护日志

本文件按时间追加记录 `ingest`、`query` 和 `lint` 操作。

## [2026-05-26] ingest | 后端开发约束

- 来源：用户对话输入。
- 结果：创建并持续补充 [Python 后端开发规范](python-backend-development-guide.md)，记录 Python 3.12、FastAPI、Uvicorn、PostgreSQL 12、Redis 6.2.5、50 并发目标及 Git 提交规则。

## [2026-05-26] ingest | LLM Wiki 维护模式

- 来源：[Karpathy, LLM Wiki 来源记录](../raw/2026-05-26-karpathy-llm-wiki-source.md)。
- 结果：建立 `raw/`、`wiki/` 与 `AGENTS.md` 三层结构，并使用本索引与日志管理持续积累的开发规范。

## [2026-05-26] ingest | 前端开发经验页面

- 来源：用户对话输入。
- 结果：新增 [前端开发经验](frontend-development-experience.md) 页面，作为后续前端技术选型、实现约定、联调和交付经验的沉淀入口。

## [2026-05-26] ingest | 跨页面功能一致性要求

- 来源：用户对话输入。
- 结果：新增 [跨页面功能一致性约定](cross-page-feature-consistency.md)，并在前端与后端规范中引用统一规则：同一功能跨页面使用时保持一致，特殊差异需告知用户。

## [2026-05-26] ingest | 日常知识积累入口

- 来源：用户对话输入。
- 结果：新增 [日常知识积累](daily-knowledge-notes.md) 页面，用于沉淀尚未归入专项规范的通用知识、工具技巧和问题排查结论。

## [2026-05-26] ingest | Git 推送授权限制

- 来源：用户对话输入。
- 结果：更新 [Python 后端开发规范](python-backend-development-guide.md) 与 `AGENTS.md`，明确禁止自动执行 `git push`，只有收到用户明确推送指令时才允许执行。

## [2026-05-26] ingest | Python 后端规范重命名

- 来源：用户对话输入。
- 结果：将后端主题的实际维护页面重命名为 [Python 后端开发规范](python-backend-development-guide.md)，为后续其他技术栈的后端规范保留独立分类空间，并保留旧 Wiki 路径作为兼容入口。

## [2026-05-26] ingest | Vue 3 前端开发规范

- 来源：用户对话输入（将 “Vu3” 按上下文整理为 “Vue 3”）。
- 结果：新增 [Vue 3 前端开发规范](vue3-frontend-development-guide.md)，记录组件与状态职责、共享功能一致性，以及与 [Python 后端开发规范](python-backend-development-guide.md) 中 FastAPI 接口协作的要求。

## [2026-05-26] ingest | Vue 3 使用 TypeScript

- 来源：用户对话输入（将 `ts` 整理为 `TypeScript`；中断的 `tx` 输入不作为有效规范）。
- 结果：更新 [Vue 3 前端开发规范](vue3-frontend-development-guide.md)，明确 Vue 3 开发使用 TypeScript，并要求 API 类型与 FastAPI 已确认模型保持一致。

## [2026-05-26] ingest | 基于 Python 后端完善 Vue 3 约束

- 来源：用户对话输入。
- 结果：依据 [Python 后端开发规范](python-backend-development-guide.md) 补全 [Vue 3 前端开发规范](vue3-frontend-development-guide.md) 的 API 契约、数据归属、Redis 数据一致性、请求控制、目录职责和联调检查要求。

## [2026-05-26] ingest | 前端后端接口地址配置规则

- 来源：用户对话输入。
- 结果：更新 [Vue 3 前端开发规范](vue3-frontend-development-guide.md)，明确打包运行时使用浏览器当前协议、主机和端口并仅拼接 API 路径，本地调试时允许直接配置 FastAPI 接口地址。

## [2026-05-26] ingest | 修正打包接口端口口径

- 来源：用户对话输入。
- 结果：修正此前“拼接后端端口”的表述，明确打包运行时沿用浏览器当前访问端口，不另行写死或拼接独立后端端口。

## [2026-05-27] ingest | Python 后端使用 SQLAlchemy

- 来源：用户对话输入。
- 结果：更新 [Python 后端开发规范](python-backend-development-guide.md)，明确 PostgreSQL 数据访问使用 `SQLAlchemy`，并保留版本、驱动、同步/异步模式和迁移工具为待确认项。
