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
<!-- Domain MOC: replace "ai" with this MOC's domain, in BOTH queries below.
     Sub-MOC (a cluster inside a domain, not one of the eight domains): a sub-MOC is
     not a new domain, so filter by its topic tag instead. Replace both WHERE lines
     with, for example: WHERE contains(file.tags, "#topic/transformers") -->
```dataview
TABLE status, updated FROM "Notes"
WHERE contains(domain, "ai")
SORT status ASC, file.name ASC
```

## Sources in this domain
<!-- Match the WHERE filter above (domain, or the same topic tag). -->
```dataview
TABLE source_type AS type, status, rating FROM "Sources"
WHERE contains(domain, "ai")
SORT status ASC
```

## Sub-maps
- [[ ]]   <!-- created only when a cluster earns one -->
