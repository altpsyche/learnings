---
title: matrix-multiplication
aliases: [matrix multiply, matmul, GEMM]
type: concept
domain: [math, graphics, ai]
status: seed
created: 2026-06-16
updated: 2026-06-16
tags: [topic/linear-algebra]
---
> Composing two linear transforms into one. Entry (i, j) of the product is the dot product of row i of the first matrix with column j of the second.

## Intuition
`AB` means "do B, then do A" as a single transform — exactly how you concatenate transforms in a
render pipeline. Mechanically, each output number is a [[dot-product]].

## Detail
- **Not commutative** (`AB ≠ BA`) — order is "which transform first".
- **Associative**, which is why a chain of transforms can be pre-multiplied once and reused.
- It is the **atomic operation of deep learning** (GEMM): a forward pass is mostly matmuls. Why it's
  fast or slow is its own story — Episode 5, GPU compute. *(future note)*

## Connects to
- [[matrix-as-transform]] — each factor is a transform
- [[dot-product]] — the operation inside every entry

## Sources
- [[book-mml-deisenroth]]
- [[video-3blue1brown-linear-algebra]]

## Recall
- What does the product AB mean as transforms? :: apply B first, then A, as one combined transform.
- What is each entry of a matrix product? :: a dot product of a row of the left matrix and a column of the right.
