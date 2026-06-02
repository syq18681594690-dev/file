# 知识库

本仓库是一个由代理持续维护的开发规范知识库，用于保存原始资料、整理后的 Wiki 页面、维护日志，以及用于创建类似知识库的 Codex skill 草稿。

## 目录结构

- `raw/`：原始来源记录。已归档的来源资料不应被改写。
- `wiki/`：整理后的 Markdown Wiki 页面。查询或维护时从 `wiki/index.md` 开始。
- `wiki/log.md`：按时间追加的维护记录，用于记录 ingest、query 和 lint 操作。
- `skills/wiki-knowledge-base/`：用于创建类似 Wiki 知识库的 Codex skill 草稿和模板。
- `AGENTS.md`：本仓库的代理维护规则。
- `PROGRESS.md`、`DECISIONS.md`、`CHANGELOG.md`：项目进度、决策记录和变更历史。

## 使用方式

1. 先阅读 `wiki/index.md`，定位相关主题页面。
2. 新增内容前，先阅读对应 Wiki 页面，避免重复或冲突。
3. 长期保留的来源资料或来源记录放入 `raw/`。
4. 更新相关 `wiki/*.md` 页面，并保持 frontmatter 中的 `sources` 信息准确。
5. 在 `wiki/log.md` 追加维护记录。
6. 会话结束前更新 `PROGRESS.md`。

## 来源追踪

Wiki 页面应在 frontmatter 中保留来源信息。来源数量增长后，应建立或维护来源索引，记录原始资料与受影响 Wiki 页面、章节之间的对应关系。原始来源更新时，先通过索引定位需要复核的页面，再进行内容更新。

## 项目定位

这是一个文档与 Wiki 维护仓库，不是可执行应用。阅读和使用当前内容不需要安装运行时依赖。

如果由代理维护本仓库，应优先遵循 `AGENTS.md`。

## 分发注意事项

不要发布本地元数据或凭据。除非明确准备作为发布产物，否则应排除 `.git/`、`.codex/`、`.agents/`、凭据文件和生成的压缩包。
