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
> The sum of componentwise products of two vectors, equal to |a||b|cosθ — a single number that wears two hats: geometric projection and similarity.

## Intuition
**Hat 1, projection:** how much of `a` lies along `b`. You use this every time you write `N·L`
for Lambert lighting. **Hat 2, similarity:** a score for how aligned two vectors point — bigger when
they agree, zero when perpendicular, negative when opposed.

## Detail
`a·b = Σ aᵢbᵢ = |a||b|cosθ`.
- `= 0` ⇔ orthogonal.
- Normalise out the magnitudes and you get **cosine similarity**, just the angle.
- Every entry of a matrix product is a dot product — it's the atom inside [[matrix-multiplication]].

Forward pointer (don't make a note yet): this exact score returns as **cosine similarity** in
embeddings (Ep 13) and as the **attention** score (Ep 14). The two-hats idea is the single biggest
unlock of [[ep01-linear-algebra]].

## Connects to
- [[vector]] — its operands
- [[matrix-multiplication]] — built out of dot products

## Sources
- [[book-mml-deisenroth]]
- [[video-3blue1brown-linear-algebra]]

## Recall
- What are the dot product's two interpretations? :: geometric projection of one vector onto another, and a similarity score (|a||b|cosθ).
- When is a·b zero? :: when the vectors are orthogonal.
