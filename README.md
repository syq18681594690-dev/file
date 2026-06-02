# Zhaobiao Wiki

This repository is a maintained development-standards Wiki. It stores original inputs, synthesized knowledge pages, maintenance logs, and a draft Codex skill for creating similar Wiki knowledge bases.

## Contents

- `raw/`: original source records. Archived source material should not be rewritten.
- `wiki/`: maintained Markdown Wiki pages. Start from `wiki/index.md`.
- `wiki/log.md`: append-only maintenance history for ingest, query, and lint work.
- `skills/wiki-knowledge-base/`: draft Codex skill and templates for creating a similar Wiki structure.
- `AGENTS.md`: project-specific maintenance rules for agents working in this repository.
- `PROGRESS.md`, `DECISIONS.md`, `CHANGELOG.md`: project state, decisions, and change history.

## How To Use

1. Read `wiki/index.md` to find the relevant topic page.
2. Read the linked Wiki page before adding new content.
3. Put long-term source material or source records in `raw/`.
4. Update the related `wiki/*.md` page and keep its `sources` metadata accurate.
5. Append a maintenance entry to `wiki/log.md`.
6. Update `PROGRESS.md` before ending a maintenance session.

## Source Tracking

Wiki pages should keep a source trail in their frontmatter. For larger source collections, add or maintain a source index that maps raw files to affected Wiki pages and sections. When a raw source changes, use that mapping to identify which Wiki pages need review.

## Opening This Project

This is a documentation and Wiki maintenance repository, not an executable application. There are no runtime dependencies required to read or use the current content.

For agent-based maintenance, follow `AGENTS.md` first.

## Distribution Notes

Do not publish local metadata or credentials. In particular, exclude `.git/`, `.codex/`, `.agents/`, credential files, and generated archive files unless they are intentionally prepared for release.
