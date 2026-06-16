---
title: matrix-as-transform
aliases: [matrix as transformation, linear map]
type: concept
domain: [math, graphics, ai]
status: seed
created: 2026-06-16
updated: 2026-06-16
tags: [topic/linear-algebra]
---
> A matrix is a linear transformation of space: it decides where the basis vectors land, and every other vector follows linearly.

## Intuition
Your model/view/projection matrices already are this. The **columns of the matrix are where the
basis vectors go** — read a matrix by asking "where do î and ĵ land?" and the whole shear/rotate/scale
becomes obvious.

## Detail
- Columns = images of the basis vectors; linearity fills in the rest.
- **Determinant** = the factor by which area/volume scales (negative ⇒ orientation flips). *(future note)*
- **Rank** = the dimensionality of the output space (a squash to a lower dimension loses rank). *(future note)*
- [[eigenvector|Eigenvectors]] are the directions this transform leaves on their own line.

## Connects to
- [[vector]] — what it acts on
- [[matrix-multiplication]] — composing two of these
- [[eigenvector]] — its invariant directions
- [[change-of-basis]] — the same transform in other coordinates

## Sources
- [[book-mml-deisenroth]]
- [[video-3blue1brown-linear-algebra]]

## Recall
- What do the columns of a transformation matrix represent? :: where each basis vector lands after the transform.
- What does the determinant tell you geometrically? :: the factor by which area/volume is scaled (sign = orientation flip).
