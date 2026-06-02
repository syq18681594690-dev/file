---
title: Codex CLI 常用工作流
type: guide
status: active
updated: 2026-06-02
sources:
  - OpenAI Codex Manual（2026-06-02 获取）
  - 本地 `codex --help` 输出（2026-06-02）
---

# Codex CLI 常用工作流

返回：[Codex CLI 命令参考](../codex-cli-command-reference.md)

## 日常交互开发

```bash
codex --sandbox workspace-write --ask-for-approval on-request
```

适合常规本地开发。Codex 可在工作区内读写，越界时请求审批。

## 只读分析

```bash
codex --sandbox read-only --ask-for-approval on-request
```

适合代码解释、风险分析、文档阅读等不希望修改文件的任务。

## 脚本总结

```bash
codex exec "总结这个项目"
```

适合 CI、定时任务、管道处理或需要把输出交给其他命令的场景。

## 审查当前改动

```bash
codex review --uncommitted
```

适合提交前审查 staged、unstaged 和 untracked 变更。

## 恢复最近会话

```bash
codex resume --last
```

适合继续之前的交互式 CLI 会话。

## 常用 slash commands

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

## 高风险全权限

```bash
codex --sandbox danger-full-access --ask-for-approval never
```

该组合会显著扩大风险，只建议在隔离容器、CI runner 或完全信任的环境中使用。

