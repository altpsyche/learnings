---
title: change-of-basis
aliases: [change of basis, basis change]
type: concept
domain: [math, graphics, ai]
status: seed
created: 2026-06-16
updated: 2026-06-16
tags: [topic/linear-algebra]
---
> Re-expressing the same vector in a different coordinate system. The numbers change, the vector does not.

## Intuition
World space versus local or tangent space. The same point on a mesh has different coordinates depending on which frame you read it in, and change of basis is the translation between frames.

## Detail
A change-of-basis matrix P, whose columns are the new basis vectors written in old coordinates, and its inverse convert components back and forth. A transform A seen in a new basis becomes P inverse times A times P, and in the basis of its own [[eigenvector|eigenvectors]] this is diagonal, the simplest possible form.

## Connects to
- [[vector]] (what is being re-expressed)
- [[matrix-as-transform]] (transforms also change under a basis change)
- [[eigenvector]] (the basis that diagonalises a transform)

## Sources
- [[book-mml-deisenroth]]
- [[video-3blue1brown-linear-algebra]]

## Recall
- What changes and what stays the same under a change of basis? :: the component numbers change, the vector itself does not.
