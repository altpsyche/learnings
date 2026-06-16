---
title: "Episode 1 — Linear Algebra for ML"
type: episode
domain: [ai]
status: seed
module: "A: Foundations"
episode: 1
created: 2026-06-16
updated: 2026-06-16
tags: [topic/linear-algebra, medium/shader]
---
> See every model as a stack of tensor transforms acting on space — the language the whole field is written in.

## Goal
Stop seeing matrices as grids of numbers and start seeing them as transformations of space, so the
rest of the series is geometric intuition rather than symbol-pushing.

## Concepts to master
- [[vector]] — point and direction at once
- [[matrix-as-transform]] — a matrix moves space
- [[matrix-multiplication]] — composing two transforms
- [[dot-product]] — projection and similarity (the two-hats concept)
- [[eigenvector]] — directions a transform leaves on their own line
- [[change-of-basis]] — the same vector seen from another coordinate system

## What to read
- [[book-mml-deisenroth]] — *Mathematics for Machine Learning*, ch. 2–4
- [[video-3blue1brown-linear-algebra]] — *Essence of Linear Algebra* (the intuition to reproduce in HLSL)

## The visual  `#medium/shader`
A live matrix acting on a grid mesh, a slider on each entry, so shear/rotate/scale are felt directly.
Determinant shown by tinting the transformed area by how much it grew/shrank; eigenvectors drawn as
rays that visibly stay on their own line while everything else rotates. This becomes the reusable
**change-of-basis** visual for later episodes.

## The build
Matrix multiply, dot product, transpose by hand → a power-iteration eigenvector finder → a small PCA
on a toy dataset, to show eigenvectors doing real work.

## Teaching note
The big unlock is the [[dot-product]] wearing two hats at once (projection + similarity). Dwell there —
cosine similarity in embeddings and attention scores both rest on it. Bank it for later episodes.

## Video hook
> "Every neural network is one matrix applied over and over. Here is exactly what that does to space."
