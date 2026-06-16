---
title: Home
type: moc
created: 2026-06-16
updated: 2026-06-16
---
# 🧠 Home

New here? Read the [[vault-guide]].

## Maps
- 🤖 [[moc-ai|AI / ML]]
- 🎨 [[moc-graphics|Graphics & Rendering]]
- 🪄 [[moc-tech-art|Technical Art]]
- 🎮 [[moc-gamedev|Game Dev]]
- 📐 [[moc-math|Math & Theory]]
- ⚡ [[moc-gpu|GPU & Systems]]
- 🛠️ [[moc-tools|Tools & Pipeline]]
- 🌱 [[moc-career|Career & Meta-Learning]]

## Active projects
```dataview
TABLE project_status, updated FROM "Projects"
WHERE type = "project" AND project_status = "active"
SORT updated DESC
```

## Reading queue (unread / in-progress sources)
```dataview
TABLE source_type AS type, author, status FROM "Sources"
WHERE status != "evergreen"
SORT status ASC
```

## Seeds to grow (oldest first)
```dataview
TABLE domain, updated FROM "Notes"
WHERE status = "seed"
SORT updated ASC
LIMIT 15
```

## Orphans to adopt (link these to something)
```dataview
LIST FROM "Notes"
WHERE length(file.inlinks) = 0 AND length(file.outlinks) = 0
```

## Recently touched
```dataview
TABLE status, file.mtime AS modified FROM "Notes" OR "Sources"
SORT file.mtime DESC
LIMIT 10
```

## Saved collections (Bases)
- [[papers]] — all papers
- [[concepts]] — all concepts by status
