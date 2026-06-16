---
title: "Episode 1: Linear Algebra for ML"
type: episode
domain: [ai]
status: seed
module: "A: Foundations"
episode: 1
# production dashboard: idea, drafting, done, published
code_status: idea
shader_status: idea
script_status: idea
blog_status: idea
video_status: idea
# real artifacts hosted elsewhere. paste URLs or paths on publish
code_repo:
shader_url:
blog_url:
video_url:
created: 2026-06-16
updated: 2026-06-16
tags: [topic/linear-algebra, medium/shader]
---
> See every model as a stack of tensor transforms acting on space, the language the whole field is written in.

## Goal
Stop seeing matrices as grids of numbers and start seeing them as transformations of space, so the rest of the series is geometric intuition rather than symbol pushing.

## Concepts to master
- [[vector]] (point and direction at once)
- [[matrix-as-transform]] (a matrix moves space)
- [[matrix-multiplication]] (composing two transforms)
- [[dot-product]] (projection and similarity, the two-faces concept)
- [[eigenvector]] (directions a transform leaves on their own line)
- [[change-of-basis]] (the same vector seen from another coordinate system)

## What to read
- [[book-mml-deisenroth]] (Mathematics for Machine Learning, chapters 2 to 4)
- [[video-3blue1brown-linear-algebra]] (Essence of Linear Algebra, the intuition to reproduce in HLSL)

## The visual
Medium: #medium/shader. A live matrix acting on a grid mesh, a slider on each entry, so shear, rotate, and scale are felt directly. The determinant shows as a tint on the transformed area, and the eigenvectors draw as rays that stay on their own line while everything else rotates. This becomes the reusable change-of-basis visual for later episodes.

## The build
Matrix multiply, dot product, and transpose by hand, then a power-iteration eigenvector finder, then a small PCA. Ships in the code repo.

## Teaching note
The big unlock is the [[dot-product]] wearing two faces, projection and similarity. Cosine similarity in embeddings and attention scores both rest on it, so bank it here.

## Video hook
> Every neural network is one matrix applied over and over. Here is exactly what that does to space.

## Production
Statuses live in the frontmatter. Board: Maps/episodes.base
- Script brain: [[ep01-script]]
- Blog brain: [[ep01-blog]]
- Code and shader in the separate repo. Fill code_repo and shader_url.
- Published blog and video: fill blog_url and video_url, set statuses to published.
