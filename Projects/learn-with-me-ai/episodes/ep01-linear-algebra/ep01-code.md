---
title: "Ep01 code and shader notes"
type: code
domain: [ai]
status: seed
episode: 1
created: 2026-06-16
updated: 2026-06-16
tags: [topic/linear-algebra, medium/shader]
---
> Code and shader brain for [[ep01-linear-algebra]]. From-scratch build plan and the HLSL for the live matrix visual. Shipping code lives in the separate repo. This is the thinking and the snippets.

## From-scratch build
Language: Python with NumPy for arrays only, avoiding the linear-algebra calls that hide the idea.
- matmul(A, B): triple loop, each output entry a [[dot-product]] of a row and a column.
- dot(a, b) and transpose(A) by hand, to ground [[matrix-multiplication]].
- power_iteration(A): repeated multiply and normalise to find the dominant [[eigenvector]].
- pca(X): center the data, form the covariance, take the top eigenvectors, project. This is where eigenvectors do real work.
Each function returns the real numbers that drive the shader: the matrix entries and the computed eigenvectors.

## Shader and HLSL notes
Medium: #medium/shader. Builds on the Part 0 grid-mesh and matrix primitive.
- Render a 2D grid mesh, then apply a 2x2 matrix M whose entries are sliders (uniforms).
- Determinant: tint the transformed cells by the sign and size of det(M), so area scaling and orientation flips are visible.
- Eigenvectors: draw as rays that stay on their own line. Compute them on the CPU with power_iteration and pass them in as uniforms, so the visual reads real values rather than faking them.
- Uniforms: the matrix entries, time, pointer, and the precomputed eigenvectors and eigenvalues.

## Snippets
Apply the live matrix to a grid position:
```hlsl
// M is the live 2x2 transform, p is the grid position
float2 transformed = mul(M, p);
```
Tint by determinant sign:
```hlsl
float det = M[0][0] * M[1][1] - M[0][1] * M[1][0];
float3 tint = det < 0 ? flipColor : growColor;
```

## Repo and links
- code_repo: fill when the repo folder exists, for example learn-with-me-code/ep01-linear-algebra
- shader_url: fill with the altpsyche.dev link when the shader is live

## Checklist to ship the visual
- [ ] from-scratch code runs and produces the real matrix and eigenvectors
- [ ] shader reads those real values, not a faked animation
- [ ] determinant tint and eigenvector rays match the math
- [ ] medium tag set
