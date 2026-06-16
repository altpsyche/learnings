---
title: <% tp.file.title %>
type: moc
domain: []
created: <% tp.date.now("YYYY-MM-DD") %>
updated: <% tp.date.now("YYYY-MM-DD") %>
---
## Overview
<!-- What this domain covers and where to start. -->

## Curated entry points
- [[ ]]

## All notes in this domain
<!-- Replace "ai" with this MOC's domain tag. -->
```dataview
TABLE status, updated FROM "Notes"
WHERE contains(domain, "ai")
SORT status ASC, file.name ASC
```

## Sources in this domain
```dataview
TABLE source_type AS type, status, rating FROM "Sources"
WHERE contains(domain, "ai")
SORT status ASC
```

## Sub-maps
- [[ ]]   <!-- created only when a cluster earns one -->
