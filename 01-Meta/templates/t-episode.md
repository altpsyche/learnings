---
title: <% tp.file.title %>
type: episode
domain: [ai]
status: seed
module:
episode:
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
created: <% tp.date.now("YYYY-MM-DD") %>
updated: <% tp.date.now("YYYY-MM-DD") %>
tags: []
---
> One-line premise of this episode.

## Goal
<!-- The single capability the viewer walks away with. -->

## Concepts to master
- [[ ]]

## What to read
<!-- source notes -->
- [[ ]]

## The visual
<!-- Medium tag: #medium/shader, #medium/plot, or #medium/code. What is rendered, and from what real values. -->

## The build
<!-- The from-scratch artifact. Ships in the code repo. -->

## Teaching note
<!-- The one framing to dwell on. -->

## Video hook
> 

## Production
Statuses live in the frontmatter. Board: Maps/episodes.base
- Script brain: [[epNN-script]]
- Blog brain: [[epNN-blog]]
- Code and shader brain: [[epNN-code]]
- Shipping code and shader live in the separate repo. Fill code_repo and shader_url.
- Published blog and video: fill blog_url and video_url, set statuses to published.
