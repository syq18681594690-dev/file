# DECISIONS

Record meaningful structure, taxonomy, tooling, or maintenance decisions.

## Template

```markdown
## YYYY-MM-DD: Decision title
**Decision**: Chose X
**Reason**: Why this choice fits
**Rejected**: Y (reason)
**Impact**: Files or workflow affected
```

## {{DATE}}: Initialize Markdown Wiki knowledge base

**Decision**: Use `raw/` for source material and `wiki/` for synthesized knowledge pages.
**Reason**: Keeps original sources separate from maintained conclusions.
**Rejected**: Put all notes in one file (reason: harder to search, link, and lint as the wiki grows).
**Impact**: `raw/`, `wiki/`, `wiki/index.md`, `wiki/log.md`
