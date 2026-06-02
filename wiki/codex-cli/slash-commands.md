---
title: Codex CLI Slash Commands
type: reference
status: active
updated: 2026-06-02
sources:
  - OpenAI Codex Manual（2026-06-02 获取）
---

# Codex CLI Slash Commands

返回：[Codex CLI 命令参考](../codex-cli-command-reference.md)

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

## 注意事项

- `/quit` 和 `/exit` 都会退出 CLI，退出前应确认重要修改已经保存或提交。
- `/permissions` 用于调整当前会话权限边界。
- `/approve` 只用于重试最近一次被自动审查拒绝的动作。
- `/clear` 会开启新对话；`Ctrl+L` 只清空终端视图，不重置当前对话。

