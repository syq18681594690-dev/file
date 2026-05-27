---
title: Python 后端开发规范
type: guide
status: active
updated: 2026-05-27
sources:
  - 用户对话输入（2026-05-26）
  - 用户对话输入（2026-05-27）
---

# Python 后端开发规范

## 1. 适用范围

本文档汇总用户明确提出的 Python 后端开发约束，供后续 Python 后端开发、联调和提交代码时遵循。其他语言或运行时的后端规范应另建页面维护。

## 2. 已确定的技术环境

| 项目 | 版本/要求 | 说明 |
| --- | --- | --- |
| Python | `3.12` | 后端代码应在 Python 3.12 环境中开发和验证 |
| Web API 框架 | `FastAPI` | 后端接口使用 FastAPI 开发 |
| 运行服务器 | `Uvicorn` | 后端服务使用 `uvicorn` 命令启动 |
| PostgreSQL | `12` | 数据库功能和 SQL 写法需兼容 PostgreSQL 12 |
| 数据访问/ORM | `SQLAlchemy` | Python 后端通过 SQLAlchemy 访问 PostgreSQL 数据库 |
| Redis | `6.2.5` | 缓存、会话或队列相关功能需兼容 Redis 6.2.5 |
| 并发能力 | 至少 `50` 并发 | 后端接口需支持至少 50 个并发请求 |

## 3. 后端依赖管理

- 后端目录必须放置 Python 依赖文件：`requirements.txt`。
- 新增或移除第三方依赖时，应同步更新 `requirements.txt`。
- 依赖版本应明确记录，避免不同开发环境因版本差异产生运行结果不一致。
- 使用 SQLAlchemy 及 PostgreSQL 驱动时，应将实际选定的依赖及版本记录在 `requirements.txt` 中。
- 安装依赖时，以后端目录中的 `requirements.txt` 为准：

```bash
python3.12 -m pip install -r requirements.txt
```

> 说明：Python 项目通常使用的标准文件名为 `requirements.txt`，而不是 `requirem.txt`。

## 4. 开发注意事项

### 4.1 Python 环境

- 启动服务、执行脚本和运行测试时，确认使用的是 Python `3.12`。
- 后续引入框架或库时，应先确认其支持 Python 3.12。

### 4.2 FastAPI 接口开发

- 后端 HTTP API 使用 FastAPI 实现。
- 引入 FastAPI 及其运行所需依赖时，应将实际使用的依赖版本记录到 `requirements.txt`。
- 接口的数据校验、请求参数和响应模型优先使用 FastAPI 及其配套的数据模型能力定义。

### 4.3 Uvicorn 启动方式

- 后端服务使用 `uvicorn` 命令启动。
- `uvicorn` 及所需运行依赖应记录在后端目录的 `requirements.txt` 中。
- 命令格式如下，其中应用模块路径和参数应按后续实际目录结构确定：

```bash
uvicorn <应用模块>:<FastAPI应用对象> [启动参数]
```

- 生产或压测环境的 `workers`、监听地址、端口等参数，应结合至少 50 并发请求的目标进行验证后确定。

### 4.4 SQLAlchemy 与 PostgreSQL 兼容性

- Python 后端使用 `SQLAlchemy` 访问 PostgreSQL `12` 数据库。
- SQLAlchemy 模型定义、查询构造、事务处理和连接配置必须兼容 PostgreSQL 12。
- 使用 PostgreSQL `12` 支持的 SQL 语法和数据库能力。
- 涉及迁移脚本、字段类型、索引或查询优化时，应在 PostgreSQL 12 环境验证。
- 不默认使用仅在更高 PostgreSQL 版本提供的特性。
- SQLAlchemy 的具体版本、同步或异步访问模式、PostgreSQL 驱动及迁移工具尚未确定，在明确前不擅自固定。

### 4.5 Redis 兼容性

- 使用 Redis `6.2.5` 可用的命令和数据结构能力。
- 引入 Redis 客户端依赖时，在 `requirements.txt` 中固定版本，并验证其与 Redis 6.2.5 的兼容性。

### 4.6 并发与性能要求

- 后端服务最低容量目标为支持至少 `50` 个并发请求。
- 开发接口时避免在请求处理过程中执行不必要的阻塞操作；数据库和 Redis 访问方案需考虑并发请求下的资源占用。
- 涉及 SQLAlchemy 连接池、Redis 连接池、服务进程数或部署配置时，应以满足 50 并发目标为基础进行配置和验证。
- 接口开发完成后，应使用压测验证 50 并发条件下接口可正常响应；具体响应时间和错误率验收阈值待确认。

### 4.7 跨页面功能一致性

- 当多个页面依赖同一业务功能时，后端接口契约、校验逻辑、业务规则和数据口径应保持一致。
- 不为不同页面分别实现互相偏离的同类业务方案；具体要求参见 [跨页面功能一致性约定](cross-page-feature-consistency.md)。
- 确有特殊页面场景需要差异处理时，实施前应告知用户差异原因和影响范围，并记录已确认的例外。

## 5. Git 提交约定

- 日常修改完成后，可以检查变更并运行相应验证，但不擅自提交代码。
- 当用户明确提出“提交 git”或同等含义的提交指令时，执行 `git commit`。
- 执行提交前，应确认待提交文件与本次任务相关，并提供清晰的提交说明。
- 如果当前目录尚未初始化为 Git 仓库，或无法执行 Git 提交，应先说明阻塞原因。
- 后端开发过程中禁止自动执行 `git push`；只有用户明确要求推送远程仓库时，才可执行相应推送操作。

## 6. 待后续确认

以下事项当前未指定，在实际搭建或开发对应功能前需要确定：

- FastAPI 项目目录结构。
- SQLAlchemy 版本、同步/异步访问模式、PostgreSQL 驱动及迁移工具。
- SQLAlchemy 与 Redis 的连接配置管理方式。
- 测试框架、代码格式化和静态检查工具。
- 50 并发压测的响应时间、错误率和测试场景验收标准。
- `uvicorn` 应用模块路径、端口、`workers` 等启动参数及部署环境要求。
