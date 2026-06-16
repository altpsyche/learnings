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
> Re-expressing the same vector in a different coordinate system — the numbers change, the vector doesn't.

## Intuition
World space vs local/tangent space: the same point on a mesh has different coordinates depending on
which frame you read it in. Change of basis is the translation between frames.

## Detail
- A change-of-basis matrix `P` (its columns are the new basis vectors in old coordinates) and its
  inverse convert components back and forth.
- A transform `A` seen in a new basis becomes `P⁻¹ A P` — and in the basis of its own
  [[eigenvector|eigenvectors]] this is **diagonal**, the simplest possible form.

## Connects to
- [[vector]] — what's being re-expressed
- [[matrix-as-transform]] — transforms also change under a basis change
- [[eigenvector]] — the basis that diagonalises a transform

## Sources
- [[book-mml-deisenroth]]
- [[video-3blue1brown-linear-algebra]]

## Recall
- What changes and what stays the same under a change of basis? :: the component numbers change; the vector itself is unchanged.
