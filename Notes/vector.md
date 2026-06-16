---
title: vector
aliases: [vectors]
type: concept
domain: [math, graphics, ai]
status: seed
created: 2026-06-16
updated: 2026-06-16
tags: [topic/linear-algebra]
---
> An element of a vector space. It is at once a point in space and a direction or displacement, and it only becomes a list of numbers once a basis is fixed.

## Intuition
As a graphics programmer you already hold both readings. The triple (x, y, z) is a vertex position and also a movement. Same triple, two meanings, and which one matters depends on context, not on the numbers.

## Detail
Addition is tip to tail. Scalar multiplication stretches or flips. The list-of-numbers view is the coordinates in a chosen basis, so changing the basis changes the numbers while the vector stays the same (see [[change-of-basis]]). Length comes from a norm, and direction is the vector normalised.

## Connects to
- [[dot-product]] (combine two vectors into a scalar)
- [[matrix-as-transform]] (what maps vectors to vectors)
- [[change-of-basis]] (why the components are not the vector)

## Sources
- [[book-mml-deisenroth]]
- [[video-3blue1brown-linear-algebra]]

## Recall
- Why is a vector not the same thing as its list of components? :: the components are coordinates in a chosen basis. The vector itself is basis independent.
