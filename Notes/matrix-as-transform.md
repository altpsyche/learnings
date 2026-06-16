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
> A matrix is a linear transformation of space. It decides where the basis vectors land, and every other vector follows linearly.

## Intuition
Your model, view, and projection matrices already are this. The columns of the matrix are where the basis vectors go, so read a matrix by asking where i-hat and j-hat land, and the whole shear, rotate, and scale becomes obvious.

## Detail
Columns are the images of the basis vectors, and linearity fills in the rest. The determinant is the factor by which area or volume scales, and a negative determinant flips orientation (future note). The rank is the dimensionality of the output space, and squashing to a lower dimension loses rank (future note). The [[eigenvector|eigenvectors]] are the directions this transform leaves on their own line.

## Connects to
- [[vector]] (what it acts on)
- [[matrix-multiplication]] (composing two of these)
- [[eigenvector]] (its invariant directions)
- [[change-of-basis]] (the same transform in other coordinates)

## Sources
- [[book-mml-deisenroth]]
- [[video-3blue1brown-linear-algebra]]

## Recall
- What do the columns of a transformation matrix represent? :: where each basis vector lands after the transform.
- What does the determinant tell you geometrically? :: the factor by which area or volume is scaled, and its sign tells you whether orientation flips.
