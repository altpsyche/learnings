---
title: Vault Guide
type: moc
created: 2026-06-16
updated: 2026-06-16
---
# Vault Guide

How this vault works. The day-to-day procedures live in [[workflows]].

## The idea
A link-first learning second brain. Knowledge lives as small, atomic concept notes in Notes, connected by links and surfaced through Maps of Content (MOCs) in Maps. Folders are few and shallow on purpose. The graph is the structure.

It has to scale across everything I learn: graphics and rendering, tech art, game dev, math, GPU and systems, tooling, and career, not just AI. Concepts that span domains, such as convolution, dot product, rotation, noise, and fields, are one note tagged with several domains and linked from several MOCs.

## Folders
| Folder | Holds |
|---|---|
| 00-Inbox | Files that arrive whole (PDFs, clips, screenshots). Empty it weekly. |
| 01-Meta | This guide, the workflows, and templates. |
| Maps | MOCs (moc-domain.md) and Bases (.base). Entry points. |
| Notes | Atomic concept notes. Flat, no sub-folders. The core graph. |
| Sources | Literature notes: papers, books, courses, videos, blogs. |
| Projects | Active efforts, such as learn-with-me-ai. |
| Journal | Daily notes and weekly reviews. |
| Assets | Images, diagrams, shader snippets, PDFs. Pasted images land here. |
| Home.md | Dashboard and launch page. |

## Capture, two paths
- Text goes into today's daily note in Journal. It is scratch. Promote durable bits into Notes.
- Whole files go into 00-Inbox. Everything there is meant to leave it.

## Naming
- Concepts: lowercase kebab, singular, for example dot-product.md, matrix-as-transform.md, brdf.md.
- MOCs: moc-domain.md.
- Sources: type-author-year-slug.md, for example paper-vaswani-2017-attention.md.
- Daily: YYYY-MM-DD.md.

## Frontmatter (properties)
Shared: title, aliases, type, domain (list), status, created, updated, tags (list).
- type: concept, source, moc, project, episode, script, blog, code, daily, weekly
- domain: ai, graphics, tech-art, gamedev, math, gpu, tools, career
- status: seed (just made), growing (understood and linking), evergreen (could teach it from this note alone)
- Sources add: source_type (paper, book, course, video, blog), author, year, url, rating.
- Projects add: project_status (active, paused, done), start.

Property keys use underscores, not hyphens (source_type, not source-type), because hyphens are read as minus signs by Dataview and Bases and break queries.

## Tags
- Topic hierarchy: #topic/diffusion, #topic/attention, #topic/pbr.
- Visual medium (from the series): #medium/shader, #medium/plot, #medium/code.
- Recall: #flashcard lines (question, then answer after the double colon) for the Spaced Repetition plugin.

## Rules
- No orphans. Every new concept note links to at least one MOC and at least one other note before you leave it.
- Reading feeds the graph. A source note's "Concepts this seeds" list spawns atomic notes.
- Class notes go straight to atomic. Each idea becomes its own concept note as you learn it. The daily note is only a holding pen.
- Episodes are folders of four files (hub, script, blog, code) with a status dashboard hub. Real code, blog, video, and shader live elsewhere, while the vault drafts and links them. See [[workflows]].
- Weekly review (t-weekly): empty the inbox, promote maturity, adopt orphans.
- Atomic notes are born when learned, not pre-stubbed. Do not bulk-create empty notes.

## Plugins to install (Community)
Dataview, Templater, Excalidraw, Obsidian Git, Spaced Repetition. Optional: Homepage, QuickAdd, Recent Files, Iconize, Style Settings. The vault works on core plugins alone. After installing Templater, point its template folder at 01-Meta/templates so the template fields resolve.

## Templates (01-Meta/templates)
t-concept, t-source, t-moc, t-project, t-episode, t-script, t-blog, t-code, t-daily, t-weekly.
