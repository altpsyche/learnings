---
title: eigenvector
aliases: [eigenvectors, eigenvalue, eigenvalues]
type: concept
domain: [math, graphics, ai]
status: seed
created: 2026-06-16
updated: 2026-06-16
tags: [topic/linear-algebra]
---
> A vector that a transform only scales, never rotates. A v = lambda v, where the scale factor lambda is the eigenvalue.

## Intuition
While a transform swings every other vector around, eigenvectors stay pinned to their own line and only get longer or shorter, or flip. They are the grain of a transformation.

## Detail
Solve A v = lambda v through the characteristic polynomial, or numerically by power iteration, which is the Episode 1 build. PCA is the eigenvectors of the covariance matrix, the directions of greatest variance, and that is the build that shows eigenvectors doing real work. A transform is simplest, meaning diagonal, when expressed in the basis of its own eigenvectors (see [[change-of-basis]]).

## Connects to
- [[matrix-as-transform]] (the invariant directions of one)
- [[change-of-basis]] (the eigenbasis diagonalises the transform)

## Sources
- [[book-mml-deisenroth]]
- [[video-3blue1brown-linear-algebra]]

## Recall
- What makes a vector an eigenvector of A? :: A only scales it, A v = lambda v, so it stays on its own line.
- What does PCA have to do with eigenvectors? :: principal components are the eigenvectors of the data's covariance matrix.
