---
title: Vault Rules and Workflows
type: moc
created: 2026-06-16
updated: 2026-06-16
---
# Vault Rules and Workflows

[[vault-guide]] describes what the folders and properties are. This describes how to operate the vault day to day.

The vault is the brain and planning layer. The shipped things, meaning the real code, the live shader on altpsyche.dev, the published blog, and the YouTube video, live elsewhere. The vault is where you learn, think, draft, and track them, linking out to the real artifacts.

## 1. Taking class notes, straight to atomic
When you study a course, book, or video:
1. Make a source note in Sources (t-source) for the thing itself: metadata, your rating, and a running "Concepts this seeds" list. One per source, made when you start it.
2. Write each idea straight into its own atomic concept note in Notes (t-concept) as you learn it. No running lecture log. Distill in the moment, one idea per note, in your own words.
3. Before you leave a concept note, it links back to its source, links to at least one neighbour and its domain MOC (no orphans), sets domain (often several) and a #topic tag, and starts at status seed, ideally with a #flashcard recall line.
4. The daily note is only a holding pen for thoughts you have not turned into a concept yet, such as a question or a TODO. It is not the record. The atomic notes are.

Why straight to atomic: you chose the purest-graph option. The friction of naming a note is the distillation. If an idea will not fit one note, it is two ideas.

## 2. Tagging and metadata
Properties carry fixed fields. Tags carry cross-cutting themes. Do not duplicate, so do not also tag #concept.

| Property | Values |
|---|---|
| type | concept, source, moc, project, episode, script, blog, code, daily, weekly |
| domain (list) | ai, graphics, tech-art, gamedev, math, gpu, tools, career |
| status | seed, growing, evergreen for concepts and sources. For episodes it is the stage: planned, in-progress, shipped |
| source_type | paper, book, course, video, blog |

Tags:
- #topic/thing is the main cross-cutting filter, for example #topic/linear-algebra, #topic/diffusion, #topic/pbr.
- #medium/shader, #medium/plot, #medium/code mark the honest medium a concept or episode visual deserves (the bible's tags).
- #flashcard marks a line carrying a recall prompt (question, then answer after the double colon) for Spaced Repetition.
- #review marks anything to revisit. #has-code marks a note that carries a snippet.

Conventions: underscores in property keys (source_type), kebab-case in filenames and tag values, singular nouns.

## 3. Episode production, folder and dashboard
Each episode is a folder under Projects/learn-with-me-ai/episodes/epNN-slug/ holding four files:

| File | Type | Role |
|---|---|---|
| epNN-slug.md | episode | Hub and dashboard: study spine, production status, links (t-episode) |
| epNN-script.md | script | Narration brain: beats and draft voiceover (t-script) |
| epNN-blog.md | blog | Written-post brain: outline and draft prose (t-blog) |
| epNN-code.md | code | Code and shader brain: from-scratch build plan, HLSL notes, snippets (t-code) |

Keep the epNN prefix on every file so wiki-link names stay unique across episodes.

Episode 1 (the ep01-linear-algebra folder) is the reference blueprint. Copy its shape for every later episode: one hub, one script, one blog, one code note, plus concept notes in Notes and source notes in Sources, with images in Assets.

The hub frontmatter is the production dashboard, the one place each channel's state lives:
- per-channel status (code_status, shader_status, script_status, blog_status, video_status), each one of idea, drafting, done, published.
- real-artifact links (code_repo, shader_url, blog_url, video_url).

See the whole slate in Maps/episodes.base, the production board.

Flow per episode:
1. Plan. Create the folder and hub from [[series-bible]]. Fill goal, concepts, reading, visual, and build. Link the concept notes it needs, which get written through the class-notes flow as you actually learn them.
2. Build. Write the real code and shader in the code repo. Keep the build plan, HLSL notes, and understanding snippets in epNN-code.md, with the repo path and shader URL.
3. Script and blog. Draft in epNN-script.md and epNN-blog.md, linking the concept notes so the explanation reuses your own atomic notes.
4. Publish. Ship the real blog, video, and shader externally. Paste URLs into the hub, set statuses to published, set the episode status to evergreen, and log it in [[learn-with-me-ai]].

Blog and YouTube are not separate notes. They are two channels on the same hub (blog_status and blog_url versus video_status and video_url). The script feeds the video, and the blog is the written narration of the same build. One artifact, narrated three ways.

## 4. Code and snippets
- Shipping code and shader source go in a separate git repo, one folder per episode. Not in the vault.
- In the vault, keep short understanding snippets inside concept notes, the small version that explains the idea, plus the repo path and the shader URL. Tag such notes #has-code.
- The test: a snippet that teaches you the idea belongs in the note. The thing that ships belongs in the repo, and the note links to it.

## 5. The loops
- Daily: scratch in the daily note, then convert anything durable to atomic notes the same day.
- Weekly (t-weekly): empty 00-Inbox, promote seed to growing to evergreen, adopt orphans, review due flashcards, pick the next focus.
- Per episode ship: set hub statuses, paste URLs, mark evergreen, log it in the project hub.

## Where does X go
| Thing | Where | Type |
|---|---|---|
| An idea while studying | Notes/concept.md, straight away | concept |
| The course, book, or video itself | Sources/type-...md | source |
| Raw unsorted thought | today's daily note | daily |
| Downloaded PDF or image | 00-Inbox, then file into Assets | |
| Episode plan and status | episodes/epNN-slug/epNN-slug.md | episode |
| Narration draft | epNN-script.md | script |
| Written-post draft | epNN-blog.md | blog |
| From-scratch code and HLSL notes | epNN-code.md | code |
| Shipping code and shaders | separate repo, linked from the code note | |
| Understanding snippet | inside the concept note (#has-code) | |
| Published blog, video, shader | external, URL in the hub frontmatter | |
