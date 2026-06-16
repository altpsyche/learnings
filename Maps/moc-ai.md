---
title: AI and Machine Learning
type: moc
domain: [ai]
created: 2026-06-16
updated: 2026-06-16
---
# AI and Machine Learning

Hub for the machine-learning track. The curriculum and production plan live in the project. The concepts it teaches live as atomic notes in Notes, many shared with graphics and math.

## The project
- [[learn-with-me-ai]] (project hub: status, milestones, log)
- [[series-bible]] (the full 33-episode curriculum, master index)
- [[enrollment-plan]] (courses mapped to the bible)

## Episodes (decomposed as studied)
- [[ep01-linear-algebra]] (Linear Algebra for ML, the worked example and starting point)

## Curated entry points
- [[dot-product]] (projection and similarity, the idea everything later rests on)
- [[matrix-as-transform]] (a matrix moves space)
- [[eigenvector]] (the invariant directions of a transform)

## Sub-maps
<!-- split off moc-transformers, moc-diffusion, etc. when each cluster earns one -->

## All AI notes
```dataview
TABLE status, updated FROM "Notes"
WHERE contains(domain, "ai")
SORT status ASC, file.name ASC
```

## AI sources
```dataview
TABLE source_type AS type, author, year, status FROM "Sources"
WHERE contains(domain, "ai")
SORT status ASC
```
