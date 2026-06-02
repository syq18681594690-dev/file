# Wiki Maintenance Instructions

## Purpose

This directory is a maintained Markdown knowledge base, not necessarily an executable software project.

## Structure

- `raw/`: original source material; do not rewrite archived sources.
- `wiki/`: synthesized knowledge pages, index, and maintenance log.
- `AGENTS.md`: maintenance rules for agents working in this directory.

## Workflow

### Ingest

1. Read `wiki/index.md`.
2. Read related topic pages.
3. Archive or record source material in `raw/` when appropriate.
4. Update or create wiki pages.
5. Update `wiki/index.md`.
6. Append an `ingest` entry to `wiki/log.md`.
7. Update `PROGRESS.md`.

### Query

1. Start from `wiki/index.md`.
2. Read relevant pages.
3. Answer with links to used pages.
4. Add reusable conclusions back to the wiki when appropriate.

### Lint

1. Check broken links.
2. Check orphan pages.
3. Check duplicate or conflicting rules.
4. Check stale dates and missing sources.
5. Fix deterministic issues and list unresolved choices.

## Git

- Do not run `git commit` unless the user explicitly asks.
- Do not run `git push` unless the user explicitly asks to push.
