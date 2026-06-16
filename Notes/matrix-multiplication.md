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
AB means do B, then do A, as a single transform. This is exactly how you concatenate transforms in a render pipeline. Mechanically, each output number is a [[dot-product]].

## Detail
It is not commutative, so AB is not the same as BA, because order is which transform happens first. It is associative, which is why a chain of transforms can be pre-multiplied once and reused. It is also the atomic operation of deep learning (GEMM), since a forward pass is mostly matrix multiplies. Why it runs fast or slow is its own topic, covered in Episode 5 on GPU compute (future note).

## Connects to
- [[matrix-as-transform]] (each factor is a transform)
- [[dot-product]] (the operation inside every entry)

## Map
- [[moc-math]]

## Sources
- [[book-mml-deisenroth]]
- [[video-3blue1brown-linear-algebra]]

## Recall
#flashcard
- What does the product AB mean as transforms? :: apply B first, then A, as one combined transform.
- What is each entry of a matrix product? :: a dot product of a row of the left matrix and a column of the right.
