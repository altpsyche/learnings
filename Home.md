---
title: Home
type: moc
created: 2026-06-16
updated: 2026-06-16
---
# Home

New here? Read the [[vault-guide]] for structure, then [[workflows]] for how to work day to day.

## Maps
- [[moc-ai|AI and ML]]
- [[moc-graphics|Graphics and Rendering]]
- [[moc-tech-art|Technical Art]]
- [[moc-gamedev|Game Dev]]
- [[moc-math|Math and Theory]]
- [[moc-gpu|GPU and Systems]]
- [[moc-tools|Tools and Pipeline]]
- [[moc-career|Career and Meta-Learning]]

## Active projects
```dataview
TABLE project_status, updated FROM "Projects"
WHERE type = "project" AND project_status = "active"
SORT updated DESC
```

## Reading queue (unread or in-progress sources)
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
- [[papers]] (all papers)
- [[concepts]] (all concepts by status)
- [[episodes]] (episode production board)
```
