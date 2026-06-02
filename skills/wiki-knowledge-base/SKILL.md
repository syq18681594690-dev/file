---
name: wiki-knowledge-base
description: Create and maintain a project-specific Markdown Wiki knowledge base. Use when a user wants to initialize a custom knowledge repository, ingest requirements or source notes into organized wiki pages, answer questions from the wiki, run wiki health checks, or keep index/log/progress/decision records synchronized.
---

# Wiki Knowledge Base

Use this skill to create or maintain a lightweight Markdown knowledge base for a project, team, or long-running topic.

The skill manages structure and workflow only. Do not copy business facts from another project into the new wiki unless the user explicitly provides them as source material.

## Directory Model

Default structure:

```text
raw/
wiki/
wiki/index.md
wiki/log.md
PROGRESS.md
DECISIONS.md
CHANGELOG.md
AGENTS.md
```

Use `raw/` for original source material and `wiki/` for synthesized pages. Treat `wiki/index.md` as the entry point for every query or update.

## Initialize

When the user asks to create a new wiki knowledge base:

1. Confirm or infer the wiki purpose from the user request.
2. Create missing directories and files from `assets/templates/`.
3. Replace placeholders such as `{{PROJECT_NAME}}`, `{{DATE}}`, and `{{TOPIC}}`.
4. Keep generated content minimal. Do not invent frameworks, versions, owners, thresholds, or policies.
5. Add an initial log entry in `wiki/log.md`.
6. Add the first progress entry and next-session entry in `PROGRESS.md`.

## Ingest

When the user provides new source material or requirements:

1. Read `wiki/index.md` first, then the related topic pages.
2. Decide whether the input belongs to an existing page or a new topic.
3. Preserve explicit user facts. Mark unclear items as pending confirmation.
4. Update the existing topic page when possible; avoid duplicate pages.
5. Update `wiki/index.md` when pages are added, renamed, or materially updated.
6. Append `## [YYYY-MM-DD] ingest | Title` to `wiki/log.md`.
7. Update `PROGRESS.md` immediately after completing the subtask.
8. If a structural or maintenance strategy decision was made, append it to `DECISIONS.md`.

## Query

When the user asks a question about the wiki:

1. Start from `wiki/index.md`.
2. Read only the necessary related pages.
3. Answer with links to the local wiki pages used.
4. State missing information plainly instead of guessing.
5. If the answer becomes reusable knowledge, add it to the relevant page or `wiki/daily-knowledge-notes.md`, then append a `query` entry to `wiki/log.md`.

## Lint

When asked to check wiki health, or when the wiki has grown:

1. Check broken relative links.
2. Check orphan pages not listed in `wiki/index.md`.
3. Check duplicate or conflicting rules.
4. Check stale `updated` dates and missing `sources`.
5. Fix deterministic issues directly.
6. Put user-choice conflicts into a pending-confirmation section.
7. Append `## [YYYY-MM-DD] lint | Title` to `wiki/log.md`.

## Page Rules

- Use lowercase kebab-case filenames for wiki pages.
- Prefer one source of truth per rule. Cross-link instead of duplicating long rules.
- Use YAML frontmatter when useful: `title`, `type`, `status`, `updated`, `sources`.
- Use relative links between wiki pages.
- Keep raw source files immutable after archiving.
- Do not run `git commit` or `git push` unless the user explicitly asks.

## Templates

Use these templates when creating files:

- `assets/templates/index.md`
- `assets/templates/log.md`
- `assets/templates/topic-page.md`
- `assets/templates/progress.md`
- `assets/templates/decisions.md`
- `assets/templates/changelog.md`
- `assets/templates/agents.md`
