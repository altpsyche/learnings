---
title: Vault Guide
type: moc
created: 2026-06-16
updated: 2026-06-16
---
# Vault Guide

How this vault works. Read once, then mostly forget — the templates enforce most of it.

## The idea
A link-first **learning second brain**. Knowledge lives as small, atomic **concept notes** in
`Notes/`, connected by links and surfaced through **Maps of Content** (MOCs) in `Maps/`. Folders
are few and dumb on purpose; the *graph* is the structure.

It must scale across everything I learn — graphics/rendering, tech art, game dev, math,
GPU/systems, tooling, career — not just AI. Concepts that span domains (convolution, dot product,
rotation, noise, fields) are **one note tagged with multiple domains**, linked from multiple MOCs.

## Folders
| Folder | Holds |
|---|---|
| `00-Inbox/` | Files that arrive whole (PDFs, clips, screenshots). Empty it weekly. |
| `01-Meta/` | This guide + `templates/`. |
| `Maps/` | MOCs (`moc-<domain>.md`) + Bases (`.base`). Entry points. |
| `Notes/` | Atomic concept notes. **Flat, no sub-folders.** The core graph. |
| `Sources/` | Literature notes: papers, books, courses, videos, blogs. |
| `Projects/` | Active efforts, e.g. `learn-with-me-ai/`. |
| `Journal/` | Daily notes + weekly reviews. |
| `Assets/` | Images, diagrams, shader snippets, pdfs (pasted images auto-land here). |
| `Home.md` | Dashboard / launch page. |

## Capture, two paths
- **Text** → today's **daily note** (`Journal/`). It's scratch; promote durable bits into `Notes/`.
- **Whole files** → `00-Inbox/`. Everything there is meant to leave it.

## Naming
- Concepts: lowercase kebab, singular — `dot-product.md`, `matrix-as-transform.md`, `brdf.md`.
- MOCs: `moc-<domain>.md`.
- Sources: `<type>-<author>-<year>-<slug>.md` — `paper-vaswani-2017-attention.md`.
- Daily: `YYYY-MM-DD.md`.

## Frontmatter (properties)
Shared: `title, aliases, type, domain[], status, created, updated, tags[]`.
- `type`: concept | source | moc | project | episode | daily | weekly
- `domain`: ai, graphics, tech-art, gamedev, math, gpu, tools, career
- `status`: **seed** (just made) → **growing** (understood, linking) → **evergreen** (could teach it from this note alone)
- Sources add: `source_type` (paper/book/course/video/blog), `author`, `year`, `url`, `rating`.
- Projects add: `project_status` (active/paused/done), `start`.

> Property keys use **underscores, not hyphens** (`source_type`, not `source-type`) — hyphens are
> read as minus signs by Dataview and Bases and break queries.

## Tags
- Topic hierarchy: `#topic/diffusion`, `#topic/attention`, `#topic/pbr`.
- Visual medium (from the series): `#medium/shader`, `#medium/plot`, `#medium/code`.
- Recall: `#flashcard` lines (or `q :: a`) for the Spaced Repetition plugin.

## Workflow / rules
- **No orphans:** every new concept note links to ≥1 MOC and ≥1 other note before you leave it.
- **Reading feeds the graph:** a source note's "Concepts this seeds" spawns atomic notes.
- **Weekly review** (`t-weekly`): empty the inbox, promote maturity, adopt orphans.
- **Atomic notes are born when learned**, not pre-stubbed. Don't bulk-create empty notes.

## Plugins to install (Community)
Dataview, Templater, Excalidraw, Obsidian Git, Spaced Repetition; optional: Homepage, QuickAdd,
Recent Files, Iconize, Style Settings. The vault works on core plugins alone — these just make the
dashboards and capture richer. After installing **Templater**, point its template folder at
`01-Meta/templates` so the `<% %>` fields resolve.

## Templates (`01-Meta/templates/`)
`t-concept` · `t-source` · `t-moc` · `t-project` · `t-episode` · `t-daily` · `t-weekly`.
