---
title: dot-product
aliases: [dot product, inner product, scalar product]
type: concept
domain: [math, graphics, ai]
status: seed
created: 2026-06-16
updated: 2026-06-16
tags: [topic/linear-algebra]
---
> The sum of componentwise products of two vectors. It equals the product of their lengths times the cosine of the angle between them, and it has two faces: geometric projection and similarity.

## Intuition
First face, projection: how much of a lies along b. You use this every time you write N dot L for Lambert lighting. Second face, similarity: a score for how aligned two vectors point. It is large when they agree, zero when perpendicular, negative when opposed.

## Detail
a dot b = a1*b1 + a2*b2 + ... = |a| |b| cos(angle). A value of zero means the vectors are orthogonal. Normalise out the lengths and you get cosine similarity, which is just the angle. Every entry of a matrix product is a dot product, so it is the atom inside [[matrix-multiplication]].

This same score returns later as cosine similarity in embeddings (Episode 13) and as the attention score (Episode 14). The two-faces idea is the biggest unlock of [[ep01-linear-algebra]].

## Connects to
- [[vector]] (its operands)
- [[matrix-multiplication]] (built out of dot products)

## Sources
- [[book-mml-deisenroth]]
- [[video-3blue1brown-linear-algebra]]

## Recall
- What are the dot product's two interpretations? :: geometric projection of one vector onto another, and a similarity score.
- When is a dot b zero? :: when the vectors are orthogonal.
