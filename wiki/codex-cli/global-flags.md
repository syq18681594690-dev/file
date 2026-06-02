---
title: Codex CLI 全局参数
type: reference
status: active
updated: 2026-06-02
sources:
  - OpenAI Codex Manual（2026-06-02 获取）
  - 本地 `codex --help` 输出（2026-06-02）
---

# Codex CLI 全局参数

返回：[Codex CLI 命令参考](../codex-cli-command-reference.md)

## 常用全局参数

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

## 安全提示

- 日常开发优先使用 `--sandbox workspace-write --ask-for-approval on-request`。
- 只读分析优先使用 `--sandbox read-only --ask-for-approval on-request`。
- `danger-full-access` 和 `never` 会显著扩大风险，只应在隔离容器、CI runner 或完全信任的环境中使用。

