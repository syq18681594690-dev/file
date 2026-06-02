---
title: Codex CLI 命令参考
type: overview
status: active
updated: 2026-06-02
sources:
  - OpenAI Codex Manual（2026-06-02 获取）
  - 本地 `codex --help` 输出（2026-06-02）
---

# Codex CLI 命令参考

## 1. 适用范围

本文档是 Codex CLI 相关资料的主题总览页，记录基础形态、阅读入口和子页面导航。具体命令、参数和示例拆分到子页面维护。

本文依据 2026-06-02 获取的 OpenAI Codex Manual，以及本机 `codex --help`、相关子命令 `--help` 输出整理。Codex CLI 仍可能随版本变化，实际可用参数应以当前机器上的 `codex <command> --help` 为准。

## 2. 基础形态

```bash
codex [OPTIONS] [PROMPT]
codex [OPTIONS] <COMMAND> [ARGS]
```

不带子命令时，`codex` 会进入交互式终端界面（TUI）。

## 3. 子页面

- [全局参数](codex-cli/global-flags.md)：记录 `--cd`、`--model`、`--sandbox`、`--ask-for-approval` 等常用全局参数。
- [顶层命令](codex-cli/top-level-commands.md)：记录 `codex exec`、`codex review`、`codex login`、`codex mcp` 等顶层命令和重点子命令。
- [Slash Commands](codex-cli/slash-commands.md)：记录交互式 CLI 中 `/` 调出的内置命令。
- [常用工作流](codex-cli/common-workflows.md)：记录日常交互、只读分析、脚本总结、审查和恢复会话等组合用法。

## 4. 维护要求

- 总览页只保留主题定位、基础形态和子页面导航。
- 新增或移动 Codex CLI 子页面时，更新本页“子页面”列表。
- 子页面应返回本总览页，并维护自己的 frontmatter 和 `sources`。
- Codex CLI 版本更新后，优先复核本页与各子页面的来源日期和命令可用性。

