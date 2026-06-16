---
type: weekly
created: <% tp.date.now("YYYY-MM-DD") %>
tags: [review]
---
# Week of <% tp.date.now("YYYY-MM-DD") %>

## Inbox — clear it
<!-- Every item in 00-Inbox/ filed into Sources / Notes / Assets or deleted. -->
- [ ] 00-Inbox empty

## Promote maturity
<!-- seed -> growing -> evergreen. -->
```dataview
TABLE status, domain, updated FROM "Notes"
WHERE status = "seed"
SORT updated ASC
```

## Adopt orphans
```dataview
LIST FROM "Notes"
WHERE length(file.inlinks) = 0 AND length(file.outlinks) = 0
```

## Wins this week
- 

## Focus next week
- 
