---
title: Codex CLI 顶层命令
type: reference
status: active
updated: 2026-06-02
sources:
  - OpenAI Codex Manual（2026-06-02 获取）
  - 本地 `codex --help` 输出（2026-06-02）
---

# Codex CLI 顶层命令

返回：[Codex CLI 命令参考](../codex-cli-command-reference.md)

## 命令总览

| 命令 | 作用 |
| --- | --- |
| `codex` | 启动交互式 CLI。适合日常开发、改代码、问问题、审查 diff。 |
| `codex exec` / `codex e` | 非交互模式运行 Codex。适合脚本、CI、管道处理和自动总结。 |
| `codex review` | 非交互式代码审查。可审查未提交变更、某个 commit 或相对 base branch 的差异。 |
| `codex login` | 登录 Codex。支持 ChatGPT 登录、device auth、API key 和 access token。 |
| `codex logout` | 删除本地保存的登录凭据。 |
| `codex mcp` | 管理 MCP server，例如 `list`、`get`、`add`、`remove`、`login`、`logout`。 |
| `codex plugin` | 管理 Codex 插件，例如安装、列出、删除插件，或管理 plugin marketplace。 |
| `codex mcp-server` | 把 Codex 本身作为 MCP server 通过 stdio 暴露给其他 agent 或工具。 |
| `codex app-server` | 启动本地 app-server，用于 IDE、App、协议开发或调试。实验性。 |
| `codex remote-control` | 确保本地 app-server daemon 以 remote-control 支持运行。实验性。 |
| `codex completion` | 生成 shell 自动补全脚本。 |
| `codex update` | 更新 Codex CLI 到最新版，取决于安装方式是否支持自更新。 |
| `codex doctor` | 生成诊断报告，检查安装、配置、认证、运行时、Git、终端、app-server 和会话等问题。 |
| `codex sandbox` | 在 Codex 提供的沙箱里运行任意命令，用于测试权限边界。 |
| `codex debug` | 调试工具集合，例如查看模型 catalog、测试 app-server 消息流。 |
| `codex apply` / `codex a` | 把 Codex Cloud 任务生成的最新 diff 应用到本地工作区。 |
| `codex resume` | 恢复之前的交互式会话。 |
| `codex archive` | 归档一个保存的会话。 |
| `codex unarchive` | 取消归档一个会话。 |
| `codex fork` | 从旧会话 fork 出一个新线程，保留原 transcript。 |
| `codex cloud` | 在终端里查看、提交、应用 Codex Cloud 任务。实验性。 |
| `codex exec-server` | 运行独立 exec-server 服务。实验性。 |
| `codex features` | 查看、启用、禁用 feature flags。 |
| `codex help` | 查看帮助。可配合子命令，例如 `codex help exec`。 |

## 重点命令

### `codex exec`

```bash
codex exec "总结这个仓库结构"
git diff | codex exec "总结这个 diff 的风险"
```

常用参数包括 `--json`、`--output-last-message <FILE>`、`--output-schema <FILE>`、`--ephemeral`、`--skip-git-repo-check`、`--ignore-user-config` 和 `--ignore-rules`。

### `codex review`

```bash
codex review --uncommitted
codex review --base main
codex review --commit <SHA>
```

用于审查未提交变更、相对 base branch 的差异，或某个提交引入的变更。

### `codex login`

```bash
codex login
codex login status
printenv OPENAI_API_KEY | codex login --with-api-key
printenv CODEX_ACCESS_TOKEN | codex login --with-access-token
codex login --device-auth
```

用于 ChatGPT 登录、无头环境 device auth、stdin 读取 API key 或 access token，以及查看登录状态。

### `codex mcp`

```bash
codex mcp list
codex mcp get <name>
codex mcp add ...
codex mcp remove <name>
codex mcp login <name>
codex mcp logout <name>
```

MCP 用于把外部工具、数据源和服务接入 Codex。

### `codex plugin`

```bash
codex plugin list
codex plugin add <plugin>
codex plugin remove <plugin>
codex plugin marketplace ...
```

插件可以携带 skills、commands、MCP 配置、hooks 和资源等。

### `codex cloud`

```bash
codex cloud
codex cloud exec --env <ENV_ID> "任务说明"
codex cloud list
codex cloud status <TASK_ID>
codex cloud diff <TASK_ID>
codex cloud apply <TASK_ID>
```

用于查看、提交、跟踪和应用 Codex Cloud 任务。

