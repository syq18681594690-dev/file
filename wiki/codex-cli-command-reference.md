---
title: Codex CLI 命令参考
type: reference
status: active
updated: 2026-06-02
sources:
  - OpenAI Codex Manual（2026-06-02 获取）
  - 本地 `codex --help` 输出（2026-06-02）
---

# Codex CLI 命令参考

## 1. 适用范围

本文档记录 Codex CLI 顶层命令、常用全局参数和典型使用场景，方便本地查看和后续维护。

本文依据 2026-06-02 获取的 OpenAI Codex Manual，以及本机 `codex --help`、相关子命令 `--help` 输出整理。Codex CLI 仍可能随版本变化，实际可用参数应以当前机器上的 `codex <command> --help` 为准。

## 2. 基础形态

```bash
codex [OPTIONS] [PROMPT]
codex [OPTIONS] <COMMAND> [ARGS]
```

不带子命令时，`codex` 会进入交互式终端界面（TUI）。

## 3. 常用全局参数

| 参数 | 作用 |
| --- | --- |
| `-C, --cd <DIR>` | 指定 Codex 使用的工作目录。 |
| `-m, --model <MODEL>` | 临时指定模型。 |
| `-p, --profile <NAME>` | 加载 `~/.codex/<name>.config.toml` 配置档。 |
| `-s, --sandbox <MODE>` | 设置沙箱模式：`read-only`、`workspace-write`、`danger-full-access`。 |
| `-a, --ask-for-approval <POLICY>` | 设置审批策略：`untrusted`、`on-request`、`never`。 |
| `--add-dir <DIR>` | 额外允许 Codex 写入的目录。 |
| `-c, --config key=value` | 临时覆盖配置。 |
| `--search` | 启用实时 Web 搜索。 |
| `--image <FILE>` | 给初始 prompt 附加图片。 |
| `--oss` | 使用本地开源模型 provider。 |
| `--dangerously-bypass-approvals-and-sandbox` | 跳过审批和沙箱，高风险，只应在外部隔离环境中使用。 |

## 4. 顶层命令总览

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

## 5. 重点命令说明

### 5.1 `codex`

启动交互式 TUI：

```bash
codex
codex "帮我解释这个项目"
codex -C /path/to/repo
codex --sandbox workspace-write --ask-for-approval on-request
```

适合大多数本地开发任务。交互式界面中可以使用 slash commands，例如 `/status`、`/model`、`/permissions`、`/review`。

### 5.2 `codex exec`

非交互运行 Codex：

```bash
codex exec "总结这个仓库结构"
git diff | codex exec "总结这个 diff 的风险"
```

常用参数：

| 参数 | 作用 |
| --- | --- |
| `--json` | 输出 JSONL，适合脚本解析。 |
| `-o, --output-last-message <FILE>` | 把最后回答写入文件。 |
| `--output-schema <FILE>` | 要求最终输出符合 JSON Schema。 |
| `--ephemeral` | 不持久化 session 文件。 |
| `--skip-git-repo-check` | 允许在非 Git 仓库中运行。 |
| `--ignore-user-config` | 不加载用户配置。 |
| `--ignore-rules` | 不加载 execpolicy 规则。 |

子命令：

| 子命令 | 作用 |
| --- | --- |
| `codex exec resume` | 恢复之前的非交互会话。 |
| `codex exec review` | 在 `exec` 体系下运行代码审查。 |

### 5.3 `codex review`

执行代码审查：

```bash
codex review --uncommitted
codex review --base main
codex review --commit <SHA>
```

常用参数：

| 参数 | 作用 |
| --- | --- |
| `--uncommitted` | 审查 staged、unstaged 和 untracked 变更。 |
| `--base <BRANCH>` | 审查当前分支相对 base 的差异。 |
| `--commit <SHA>` | 审查某个提交引入的变更。 |
| `--title <TITLE>` | 给审查摘要显示标题。 |
| `[PROMPT]` | 自定义审查重点。 |

### 5.4 `codex login`

管理登录：

```bash
codex login
codex login status
printenv OPENAI_API_KEY | codex login --with-api-key
printenv CODEX_ACCESS_TOKEN | codex login --with-access-token
codex login --device-auth
```

用途：

- 通过浏览器完成 ChatGPT 登录。
- 在无头或远程环境使用 device auth。
- 从 stdin 读取 API key 或 Codex access token。
- 查看当前登录状态。

### 5.5 `codex logout`

清除本地凭据：

```bash
codex logout
```

适合共享机器、账号切换或凭据泄露后的清理。

### 5.6 `codex mcp`

管理 MCP server：

```bash
codex mcp list
codex mcp get <name>
codex mcp add ...
codex mcp remove <name>
codex mcp login <name>
codex mcp logout <name>
```

MCP 用于把外部工具、数据源和服务接入 Codex。

### 5.7 `codex plugin`

管理插件：

```bash
codex plugin list
codex plugin add <plugin>
codex plugin remove <plugin>
codex plugin marketplace ...
```

插件可以携带 skills、commands、MCP 配置、hooks 和资源等。

### 5.8 `codex app-server`

启动本地协议服务：

```bash
codex app-server
codex app-server --listen stdio://
codex app-server --listen ws://127.0.0.1:PORT
codex app-server --listen unix://
```

子命令：

| 子命令 | 作用 |
| --- | --- |
| `daemon` | 管理本地 app-server daemon。 |
| `proxy` | 把 stdio 代理到运行中的 app-server。 |
| `generate-ts` | 生成 TypeScript bindings。 |
| `generate-json-schema` | 生成协议 JSON Schema。 |

### 5.9 `codex cloud`

管理 Codex Cloud 任务：

```bash
codex cloud
codex cloud exec --env <ENV_ID> "任务说明"
codex cloud list
codex cloud status <TASK_ID>
codex cloud diff <TASK_ID>
codex cloud apply <TASK_ID>
```

子命令：

| 子命令 | 作用 |
| --- | --- |
| `exec` | 提交云端任务。 |
| `list` | 列出任务。 |
| `status` | 查看任务状态。 |
| `diff` | 查看云端任务生成的 diff。 |
| `apply` | 把云端 diff 应用到本地。 |

### 5.10 `codex apply`

快捷应用 Codex Cloud 任务 diff：

```bash
codex apply <TASK_ID>
```

如果 `git apply` 发生冲突，该命令会失败。

### 5.11 `codex resume`

恢复旧会话：

```bash
codex resume
codex resume --last
codex resume <SESSION_ID>
codex resume <SESSION_ID> "继续完成剩下的测试"
```

常用参数：

| 参数 | 作用 |
| --- | --- |
| `--last` | 恢复最近会话。 |
| `--all` | 显示所有会话，不按当前目录过滤。 |
| `--include-non-interactive` | 包含 `codex exec` 产生的会话。 |

### 5.12 `codex fork`

从旧会话分叉：

```bash
codex fork
codex fork --last
codex fork <SESSION_ID>
```

适合保留原路线，同时另开一个线程尝试其他方案。

### 5.13 `codex archive` / `codex unarchive`

归档和恢复归档会话：

```bash
codex archive <SESSION>
codex unarchive <SESSION>
```

`SESSION` 可以是 session id 或 session name。

### 5.14 `codex completion`

生成 shell 补全：

```bash
codex completion bash
codex completion zsh
codex completion fish
codex completion power-shell
codex completion elvish
```

示例：

```bash
codex completion zsh > "${fpath[1]}/_codex"
```

### 5.15 `codex doctor`

诊断本地环境：

```bash
codex doctor
codex doctor --summary
codex doctor --json
codex doctor --all
```

适合排查登录失败、配置异常、终端问题、Git 问题或 app-server 问题。

### 5.16 `codex sandbox`

直接在 Codex 沙箱里运行命令：

```bash
codex sandbox ls
codex sandbox --permissions-profile <NAME> npm test
```

用于验证某个命令在指定权限 profile 下能否运行。

### 5.17 `codex features`

管理功能开关：

```bash
codex features list
codex features enable <feature>
codex features disable <feature>
```

相关变更会持久写入 `$CODEX_HOME/config.toml`。

### 5.18 `codex update`

更新 Codex CLI：

```bash
codex update
```

是否成功取决于当前安装方式是否支持自更新。

### 5.19 `codex debug`

调试工具：

```bash
codex debug models
codex debug models --bundled
codex debug app-server send-message-v2 "hello"
```

用途：

- `debug models`：打印 Codex 看到的模型 catalog。
- `--bundled`：只看当前 binary 内置 catalog，不刷新远程。
- `debug app-server send-message-v2`：用内置测试客户端向 app-server 发一条 V2 消息。

### 5.20 `codex mcp-server`

让 Codex 作为 MCP server 运行：

```bash
codex mcp-server
```

适合另一个 agent 或 MCP client 调用 Codex。

### 5.21 `codex remote-control`

确保本地 app-server daemon 以 remote-control 模式运行。该命令主要用于远程控制、移动端或 SSH 远程工作流，不是普通日常开发命令。

### 5.22 `codex exec-server`

运行实验性独立服务，用于程序化或服务化执行 Codex。普通使用一般不需要。

## 6. CLI 内置 slash commands

在交互式 Codex CLI 中，输入 `/` 可以打开 slash command 弹窗。任务正在运行时，也可以输入 slash command 后按 `Tab` 排队到下一轮执行。

| 命令 | 作用 | 适用场景 |
| --- | --- | --- |
| `/permissions` | 调整 Codex 不询问即可执行的权限范围。 | 会话中临时放宽或收紧审批要求，例如切换 Auto 或 Read Only。 |
| `/ide` | 引入 IDE 当前打开文件、选区和上下文。 | 不想重新描述 IDE 中正在看的文件时使用。 |
| `/keymap` | 重映射 TUI 快捷键。 | 查看并持久化自定义快捷键到 `config.toml`。 |
| `/vim` | 切换输入框 Vim 模式。 | 在 Vim normal/insert 行为和默认编辑模式之间切换。 |
| `/sandbox-add-read-dir` | 给沙箱额外目录读取权限，仅 Windows。 | 命令需要读取当前可读根之外的绝对路径时使用。 |
| `/agent` | 切换当前 agent thread。 | 查看或继续 spawned subagent 的工作线程。 |
| `/apps` | 浏览 apps/connectors 并插入到 prompt。 | 需要把某个 app 作为 `$app-slug` 附加给 Codex 使用。 |
| `/plugins` | 浏览已安装和可发现插件。 | 查看插件工具、安装建议插件或管理插件可用性。 |
| `/hooks` | 查看和管理生命周期 hooks。 | 检查 hook 配置、信任新 hook 或禁用非托管 hook。 |
| `/clear` | 清空终端并开启新对话。 | 想在同一 CLI 会话中重置可见 UI 和对话上下文。 |
| `/compact` | 总结当前可见对话以节省 token。 | 长对话后保留关键上下文，降低上下文占用。 |
| `/copy` | 复制 Codex 最新完成的输出。 | 快速复制最近的回答或计划，也可使用 `Ctrl+O`。 |
| `/diff` | 显示 Git diff，包括未跟踪文件。 | 提交或测试前查看 Codex 改了什么。 |
| `/exit` | 退出 CLI，等同 `/quit`。 | 结束当前 CLI 会话。 |
| `/experimental` | 切换实验性功能。 | 启用 subagents、Apps、Smart Approvals 等可选功能。 |
| `/approve` | 批准一次最近被 auto review 拒绝的重试。 | 自动审查拒绝某个动作后，确认要重试一次。 |
| `/memories` | 配置 memory 使用和生成。 | 在 TUI 中开启、关闭或调整 memory 行为。 |
| `/skills` | 浏览和使用 skills。 | 为特定任务选择本地 skill，让后续请求遵循该 skill。 |
| `/feedback` | 向 Codex 维护方发送日志和反馈。 | 报告问题或向支持提供诊断信息。 |
| `/init` | 在当前目录生成 `AGENTS.md` 脚手架。 | 为仓库或子目录沉淀持久代理指令。 |
| `/logout` | 登出 Codex。 | 在共享机器上清理本地凭据。 |
| `/mcp` | 列出已配置 MCP tools。 | 检查当前会话能调用哪些外部工具；可用 verbose 查看服务器细节。 |
| `/mention` | 将文件或目录附加到对话。 | 明确指向希望 Codex 下一步读取的文件或文件夹。 |
| `/model` | 选择当前模型和可用 reasoning effort。 | 在普通模型和更强推理模型之间切换。 |
| `/fast` | 切换 Fast service tier。 | 当前模型支持 Fast tier 时，开启、关闭或查看状态。 |
| `/plan` | 切换到计划模式，并可附带 prompt。 | 实施前先让 Codex 提出计划。任务运行中暂不可用。 |
| `/goal` | 设置、查看、暂停、恢复或清除任务目标。 | 长任务中给 Codex 一个持续追踪的目标。 |
| `/personality` | 选择沟通风格。 | 调整回复风格，例如更简洁或更协作。 |
| `/ps` | 查看实验性后台终端和近期输出。 | 检查当前会话启动的长运行后台命令。 |
| `/stop` | 停止所有后台终端。 | 取消当前会话启动的后台终端工作。 |
| `/fork` | 从当前对话 fork 新线程。 | 想探索另一条路线但保留当前 transcript。 |
| `/side` / `/btw` | 开启临时旁路对话。 | 问一个聚焦追问，同时不打断主线程 transcript。 |
| `/raw` | 切换 raw scrollback 模式。 | 查看长输出时，让终端选择和复制更少受格式影响。 |
| `/resume` | 从会话列表恢复旧对话。 | 继续之前的 CLI 会话。 |
| `/new` | 在同一 CLI 会话中开始新对话。 | 想重置聊天上下文但不退出 CLI。 |
| `/quit` | 退出 CLI。 | 结束当前 CLI 会话。 |
| `/review` | 请求 Codex 审查当前工作树。 | 完成修改后或需要第二视角审查本地变更时使用。 |
| `/status` | 显示会话配置和 token 使用。 | 确认当前模型、审批策略、可写根目录和剩余上下文。 |
| `/debug-config` | 打印配置层和 requirements 诊断。 | 排查配置优先级、托管策略和网络约束。 |
| `/statusline` | 交互式配置 TUI 底部状态栏字段。 | 选择并排序 model、context、limits、git、tokens、session 等状态项。 |
| `/title` | 配置终端窗口或标签页标题字段。 | 调整标题中显示的 project、status、thread、branch、model、task progress 等内容。 |
| `/theme` | 选择语法高亮主题。 | 预览并持久化终端语法高亮主题。 |

注意事项：

- `/quit` 和 `/exit` 都会退出 CLI，退出前应确认重要修改已经保存或提交。
- `/permissions` 用于调整当前会话权限边界。
- `/approve` 只用于重试最近一次被自动审查拒绝的动作。
- `/clear` 会开启新对话；`Ctrl+L` 只清空终端视图，不重置当前对话。

常用 slash command 示例：

```text
/status
/permissions
/model
/plan 为这个迁移任务制定计划
/goal 完成迁移并保持测试通过
/review
/diff
/compact
/resume
```

## 7. 推荐日常组合

日常交互开发：

```bash
codex --sandbox workspace-write --ask-for-approval on-request
```

只读分析：

```bash
codex --sandbox read-only --ask-for-approval on-request
```

脚本总结：

```bash
codex exec "总结这个项目"
```

审查当前改动：

```bash
codex review --uncommitted
```

恢复最近会话：

```bash
codex resume --last
```

高风险全权限：

```bash
codex --sandbox danger-full-access --ask-for-approval never
```

高风险全权限只建议在隔离容器、CI runner 或完全信任的环境中使用。
