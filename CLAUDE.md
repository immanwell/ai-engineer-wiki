# LLM Wiki

A personal knowledge base maintained by Claude Code for Em.
Based on Andrej Karpathy's LLM Wiki pattern.

## Purpose

This wiki is a structured, interlinked knowledge base for passing the Claude Certified Architect – Foundations exam and building foundational AI engineering knowledge along the way. The exam domains are: `agentic-architecture`, `tool-design-mcp`, `claude-code`, `prompt-engineering`, and`context-reliability`.

Claude maintains the wiki. The human curates sources, asks questions, and guides the analysis.

## Folder structure

```
raw/          -- source documents (immutable -- never modify these)
wiki/         -- markdown pages maintained by Claude
wiki/index.md -- table of contents for the entire wiki
wiki/log.md   -- append-only record of all operations
```

## Ingest workflow

When the user adds a new source to `raw/` and asks you to ingest it:

1. Read the full source document
2. Discuss key takeaways with the user before writing anything
3. Create a summary page in `wiki/` named after the source
4. Create or update concept pages for each major idea or entity
5. Add wiki-links ([[page-name]]) to connect related pages
6. Update `wiki/index.md` with new pages and one-line descriptions
7. Append an entry to `wiki/log.md` with the date, source name, and what changed
8. To read PDFs in the raw/ folder, use the Read tool on the file path.
9. For YouTube URLs, run `summarize "URL" --youtube auto` first and save to `raw/
10. For exam-domain source files (agentic-architecture, tool-design-mcp, claude-code, prompt-engineering, context-reliability), generate Anki cards using Template 1 (Question, Answer, Topic). Save as `ASSETS/[CertName]-[PageName]-TechnicalConcepts-YYYY-MM-DD.csv` using commas as the delimiter. **Do not include a header row** — start directly with the first question. One CSV per source file.

A single source may touch 10-15 wiki pages. That is normal.

## Page format

Every wiki page should follow this structure:

Before creating any wiki page, read `templates/wiki-page.md` and use it as the base structure. Fill in all frontmatter fields — do not leave placeholder values like {{title}}, {{source_file}} in the final file.

## Citation rules

- Every factual claim should reference its source file
- Use the format `[[raw/filename.ext|display text]]` for clickable wiki-links to raw source files
- If two sources disagree, note the contradiction explicitly
- If a claim has no source, mark it as needing verification
- Before writing any wiki page content, cross-check claims against the source — do not introduce information not present in the source; if inferring, label it explicitly as inferred

## Question answering

When the user asks a question:

1. Read `wiki/index.md` first to find relevant pages
2. Read those pages and synthesize an answer
3. Cite specific wiki pages in your response
4. If the answer is not in the wiki, say so clearly
5. If the answer is valuable, offer to save it as a new wiki page

Good answers should be filed back into the wiki so they compound over time.

## Lint

When the user asks you to lint or audit the wiki:

- Check for contradictions between pages
- Find orphan pages (no inbound links from other pages)
- Identify concepts mentioned in pages that lack their own page
- Flag claims that may be outdated based on newer sources
- Check that all pages follow the page format above
- Report findings as a numbered list with suggested fixes

## Rules

- Never modify anything in the `raw/` folder
- Always update `wiki/index.md` and `wiki/log.md` after changes
- Before committing, run a lint pass — check for contradictions between pages, orphaned links, and malformed citations
- Keep page names lowercase with hyphens (e.g. `machine-learning.md`)
- Write in clear, plain language
- When uncertain about how to categorize something, ask the user
- Author tags in frontmatter should be plain usernames without the @ symbol (e.g., `author: dotta` not `author: @steipete`)
- Run `date "+%A, %-d %B %Y, %H:%M"` via Bash tool to get the current datetime before creating any wiki page
- Never move or modify the "Modified" formula
- The {{Date and Time}} should be in the following format: "dddd, Do MMMM YYYY, HH:mm" eg Monday, May 13, 1956, 01:20 reflecting the current day of the week, month, date, year and time the document is created and this is never changed again
- When updating an existing wiki page, never touch the `Created` field or `Modified` formula — edit body content only; the Modified field auto-updates via Obsidian's `dateformat(this.file.mtime, ...)` formula
