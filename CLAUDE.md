# Technical Informatics Wiki — Schema

This file tells the LLM (Claude Code or any compatible agent) how this wiki is
structured, what conventions to follow, and what to do during ingest, query,
and lint operations. Read this file first in every session.

## Purpose

A personal knowledge base covering the **Technical Informatics** module at
TUHH (Hamburg University of Technology). The source material is the user's
own **handwritten lecture summaries**, photographed/scanned as images in
German (or mixed German/English). The wiki is the English-language,
structured, cross-referenced synthesis of that material — built up
incrementally as new summary pages are ingested.

The user does not write the wiki. The LLM reads, translates, extracts, and
maintains it. The user curates sources, reviews updates, and asks questions.

## Architecture

```
raw/
  summaries/        # immutable photos/scans of handwritten summary pages (images, PDFs)
  assets/           # any other raw images (e.g. lecture slide photos) if added later
wiki/
  index.md          # catalog of every wiki page, organized by category
  log.md            # append-only chronological record of ingests/queries/lints
  topics/           # one page per lecture topic / module chapter
  concepts/         # one page per recurring concept/term that spans topics
  comparisons/       # generated comparison pages, tables, synthesis docs
CLAUDE.md           # this schema file
```

- **raw/** is read-only source of truth. Never edit or delete files here.
  Original filenames should keep a date or topic hint where possible
  (e.g. `raw/summaries/2026-04-10_boolesche_algebra.jpg`).
- **wiki/** is entirely LLM-owned. All pages are in English, in Markdown,
  with YAML frontmatter.

## Page conventions

Every wiki page (topics, concepts, comparisons) starts with frontmatter:

```yaml
---
title: <Human-readable title>
type: topic | concept | comparison
tags: [tag1, tag2]
sources: [raw/summaries/2026-04-10_boolesche_algebra.jpg]
created: 2026-04-10
updated: 2026-04-10
---
```

Body structure:
1. **One-paragraph summary** — plain-English definition/overview.
2. **Details** — the substantive content, translated and cleaned up from the
   handwritten summary, organized with headers as needed.
3. **Diagrams** — where a concept, process, or relationship benefits from a
   visual, embed a Mermaid diagram (flowchart, sequence diagram, concept map,
   state diagram, etc.) in a fenced ```mermaid block. Prefer a diagram over
   prose whenever the original handwritten page contains a drawing, circuit,
   state machine, or process flow.
4. **Related pages** — bullet list of `[[wiki-links]]` (Obsidian-style) to
   other topic/concept pages.
5. **Open questions / gaps** — anything unclear, illegible, or incomplete in
   the handwritten source, flagged for the user.

Keep topic pages matched to the module's own structure (e.g. one page per
lecture or chapter) and split out concepts (e.g. "Karnaugh Map",
"Finite State Machine", "Pipelining") into their own concept pages once they
recur across multiple topics or warrant independent depth.

## index.md format

Organized by section (`## Topics`, `## Concepts`, `## Comparisons`). Each
entry: link, one-line summary, last-updated date.

```markdown
## Topics
- [[topics/boolesche-algebra]] — Boolean algebra basics and laws. (2026-04-10)
```

Update index.md on every ingest — add new pages, refresh one-line summaries
if a page's scope changed.

## log.md format

Append-only, newest entry at the bottom. Each entry starts with:

```
## [YYYY-MM-DD] ingest | <summary title>
- Source: raw/summaries/<file>
- Pages touched: [[topics/...]], [[concepts/...]]
- Notes: <anything noteworthy — contradictions, gaps, translation issues>
```

Use `ingest`, `query`, or `lint` as the type tag so entries stay greppable
(`grep "^## \[" wiki/log.md`).

## Operations

### Ingest (default: one source at a time, user stays involved)
1. Read the image(s) in `raw/summaries/`. Transcribe and translate the
   handwritten German/mixed content into English.
2. Summarize key takeaways back to the user; confirm understanding before
   writing pages, especially where handwriting is ambiguous.
3. Create or update the relevant topic page(s) and any concept pages that
   recur or deserve their own entry.
4. Add Mermaid diagrams for processes, circuits, state machines, or
   relationships drawn in the original notes.
5. Update `wiki/index.md` and append an entry to `wiki/log.md`.
6. Flag anything illegible, ambiguous, or possibly inconsistent with
   existing pages — note it in the page's "Open questions" section and in
   the log.

### Query
1. Read `wiki/index.md` first to find candidate pages.
2. Read the relevant topic/concept pages (and underlying raw images only if
   needed for extra detail).
3. Answer with citations to wiki pages (and raw source where relevant).
4. If the answer is a reusable artifact (comparison table, synthesis, new
   diagram), offer to file it into `wiki/comparisons/` or an existing page,
   and log it.

### Lint (run when asked, or suggest periodically)
Check for:
- Contradictions between pages.
- Orphan pages (no inbound `[[links]]`, missing from index.md).
- Concepts mentioned repeatedly but without their own page.
- Missing cross-references between related topics/concepts.
- Untranslated German fragments left in wiki pages.
- Gaps where a diagram would clarify a process but is missing.
Report findings to the user; apply fixes only after confirming scope for
anything beyond small omissions (e.g. always fix a missing cross-link, ask
before restructuring a page).

## Conventions & style
- All wiki content is in English, even though source material is handwritten
  German notes — translate faithfully, don't paraphrase away technical
  precision.
- Keep original German technical terms in parentheses on first use where
  useful, e.g. "flip-flop (Kippstufe)".
- Prefer Mermaid over prose descriptions of circuits, FSMs, and process
  flows; prefer tables for comparisons of multiple items/attributes.
- Never modify files under `raw/`.
- This schema file is a living document — update it as conventions evolve
  during actual use.
