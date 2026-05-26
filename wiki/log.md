---
title: Wiki 维护日志
type: log
updated: 2026-05-26
---

# Wiki 维护日志

本文件按时间追加记录 `ingest`、`query` 和 `lint` 操作。

## [2026-05-26] ingest | 后端开发约束

- 来源：用户对话输入。
- 结果：创建并持续补充 [后端开发约定](backend-development-guide.md)，记录 Python 3.12、FastAPI、Uvicorn、PostgreSQL 12、Redis 6.2.5、50 并发目标及 Git 提交规则。

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
- 结果：更新 [后端开发约定](backend-development-guide.md) 与 `AGENTS.md`，明确禁止自动执行 `git push`，只有收到用户明确推送指令时才允许执行。
