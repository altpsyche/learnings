---
title: Vault Handbook
type: moc
created: 2026-06-16
updated: 2026-06-16
---
# Vault Handbook

The operator's manual. How to actually drive this vault day to day, get the most out of every plugin, and keep it healthy as it grows. New to the vault? Start with [[quickstart]] for the ten-minute on-ramp, then come back here. Read [[vault-guide]] for what the parts are, and keep [[workflows]] open for the short rules. This document is the long version with steps, examples from your own notes, and the rhythms.

## How the three meta docs fit
- [[vault-guide]] answers "what is this." Folders, naming, properties, tags, the design idea.
- [[workflows]] answers "what are the rules." The class-notes flow, the episode pipeline, the loops, in brief.
- This handbook answers "how do I do it." The keystrokes, the tools, the daily and weekly and long-term motions, and what to do when something looks wrong.

When the three ever disagree, vault-guide owns the definitions, workflows owns the rules, and this doc owns the procedures.

## The whole system in one loop
Everything in the vault is the same short motion, repeated:
1. Capture a thing. A thought goes to today's daily note. A source you are about to study gets a source note. A file you downloaded goes to 00-Inbox.
2. Distill it into one atomic concept note in Notes, in your own words, one idea per note.
3. Link it before you leave it. At least one neighbour concept and at least one MOC, so it is never an orphan. Add a domain, a topic tag, and a recall prompt.
4. Recall it. The #flashcard prompt comes back on a schedule so the idea sticks.
5. Mature it. Over the weeks a note moves from seed to growing to evergreen, and clusters of notes earn a sub-MOC.

If you only remember one thing, remember that the friction of naming a note and choosing where to link it is the learning. The tools below just make that motion fast and visible.

## Driving the tools

### Core Obsidian
Two display modes matter. Editing mode shows the raw markdown. Reading mode, and the live preview in between, renders links, embeds, queries, and tags. Ctrl+E toggles between them. A live query or an embedded image looks like plain text in editing mode and only renders in reading or live preview, which is normal, not a bug.
- Make a link. Type two open square brackets and start typing a note name, then pick it from the list. To show different text, write the target, then a vertical bar, then the label, the way the Home links read as friendly names. A link to a note that does not exist yet is allowed; it shows dimmed until you create that note.
- Embed something inline. Put an exclamation mark in front of a link to embed it, so an image, an Excalidraw drawing, or even another note shows in place rather than as a clickable link.
- Tags. Type a hash and the tag, nested with slashes, as in #topic/linear-algebra. Tags carry cross-cutting themes; fixed facts belong in properties, not tags.
- Quick switcher. Press Ctrl+O, type part of a note title or alias, jump there. Your aliases (for example "matmul" and "GEMM" on [[matrix-multiplication]]) make this fast.
- Command palette. Press Ctrl+P and type the start of any command. Almost everything below is a command you run from here. Plugin command labels can change between versions, so if a command name in this handbook does not match exactly, type the feature word instead (template, review, drawing, commit, base, extract) and pick the closest match. That makes every command instruction here version-proof.
- Backlinks and outgoing links. The right sidebar shows what links to the current note and what it links out to. This is how you check a note is not an orphan: open it, look at backlinks, confirm a MOC is in the list.
- Properties panel. The frontmatter at the top of a note is editable as fields. Changing status from seed to growing here is what moves the note between the Home queries.
- Graph view. Open it from the left ribbon or the command palette. Nodes are notes, lines are links. With the color groups set up (see below) you can see each domain as a color and spot a note drifting on its own.

### Dataview (live queries)
What it is: a community plugin that runs a small query language inside a note and renders a live table or list. Version 0.5.68 here.

Where it already runs:
- [[Home]] has five live query blocks: active projects, the reading queue, seeds to grow, orphans, and recently touched. The two other sections on Home, the Maps list and the Saved collections links, are plain static lists you maintain by hand, not queries.
- Every MOC has two live blocks: all notes in that domain, and the sources in that domain. For example [[moc-math]] lists all six linear-algebra notes because they each carry `domain: [math]`. The Curated entry points list above those blocks is static, chosen by you.
- The weekly template has a seeds block and an orphans block.

How to use it:
- The query blocks update themselves. You never edit them by hand. In reading mode or live preview they re-run when you open the note and refresh on a short timer, so a frontmatter change moves a note between blocks within a few seconds. In editing mode they show as raw query text, which is expected.
- Worked example: open [[dot-product]], change `status: seed` to `status: growing` in the properties panel. Reopen [[Home]]. The note drops out of "Seeds to grow" on its own. That is the whole mechanism.
- To read a query, switch the MOC to source mode (Ctrl+E toggles edit and preview). A block fenced as dataview is the query. The MOC queries say, in plain terms, "list every note whose domain contains this MOC's domain, show status and updated, sort by status."
- To make a new view, copy an existing block and change the one filter line. If you ever want "all notes tagged #has-code," copy a MOC block and set the WHERE to `contains(file.tags, "#has-code")`.

Gotcha: a query returns nothing if the property name is misspelled, the folder name in FROM is wrong, or no note matches yet. An empty table usually means "no matching notes," not "broken query."

### Bases (core plugin)
What it is: the core Bases plugin gives a spreadsheet-style view over notes with frontmatter properties, filtered and sorted in the interface and saved as a `.base` file. It is the no-code cousin of Dataview.

The three you have, in Maps:
- [[papers]] shows every source whose `source_type` is paper, newest first. It is empty today because your two sources are a book and a video, not papers. It will fill as you add papers.
- [[concepts]] shows every concept note with its status and domain.
- [[episodes]] is the production board: every episode with its five channel statuses, sorted by episode number.

How to use it:
- Open a base by clicking the `.base` file in Maps, or follow the links at the bottom of [[Home]].
- Make a new base by running "Bases: Create new base" from the command palette, or from the new-file menu choosing Base. Save it in Maps and link it from [[Home]] the way the three above are linked.
- Change a view in the interface (add a column, change a filter, switch from table to cards) and it saves into the file. You do not write query text.
- When to reach for Bases over Dataview: Bases for a board you scan and tweak in place, like the episode dashboard. Dataview for a query you want embedded inline in a note's prose, like a MOC.

### Templater (now enabled)
What it is: the templating plugin, version 2.20.5, pinned for Obsidian 1.12.7. It fills the `<% %>` fields in your templates, such as `<% tp.file.title %>` and `<% tp.date.now("YYYY-MM-DD") %>`. It is now enabled and pointed at 01-Meta/templates.

How to use it:
- New concept note from a template: run "Templater: Create new note from template" from the command palette, pick t-concept, name it. The title and the created and updated dates fill themselves, and the cursor lands on the first field.
- Insert a template into the current note: "Templater: Open insert template modal."
- Daily notes: "Open today's daily note" creates today's note in Journal from t-daily, and because trigger-on-creation is on, the date fields resolve automatically. You do not need to run Templater by hand for daily notes.

Gotcha: if a new note ever shows literal `<% ... %>` text, Templater did not run. Check it is still enabled in Settings, Community plugins, and that the template folder is 01-Meta/templates.

### Spaced Repetition (the flashcards)
What it is: the review plugin, version 1.15.4. It turns your recall lines into flashcards and schedules them.

How a card is made (you already do this):
- A note carries the `#flashcard` tag in its Recall section. That marks the whole note as a deck.
- Each line of the form `prompt :: answer` becomes one card. The `::` is the separator, configured in the plugin.
- Example: [[eigenvector]] has `#flashcard` and two `::` lines, so it contributes two cards.
- Card formats: the vault convention is the single-line form, prompt then `::` then answer. The plugin also supports a multiline card (the question, a line with a single question mark, then the answer) and cloze deletions, but the convention here is single-line, so stay with `::` unless you have a clear reason.

How to review:
- Run "Spaced Repetition: Review flashcards" from the command palette, or click the due count in the status bar. Read the prompt, think, reveal, then rate Again, Hard, Good, or Easy. The rating sets when the card returns.
- Whole-note review is separate and uses the `#review` tag. Tag a note `#review` to put it in the note-review queue when you want to revisit the whole note rather than single prompts.

Best ways to write prompts:
- One fact per prompt. If an answer has two parts, make two cards. See the two-card split on [[matrix-as-transform]].
- Ask for the idea, not the wording. "What do the columns of a transform matrix represent" beats "recite the definition."
- Write the prompt the moment you write the note, while the gap in your understanding is fresh.

### Excalidraw (diagrams)
What it is: a drawing plugin, version 2.24.1, for hand-drawn diagrams stored as notes.

When a drawing beats prose: pipelines and mechanisms. A render pipeline, a backprop graph flowing in reverse, the four shader primitives and what reuses them. Anything where the spatial layout is the explanation.

How to use it:
- Run "Excalidraw: Create new drawing." Draw, then it saves as a `.excalidraw.md` file.
- Store drawings in Assets, the same folder pasted images use.
- Embed a drawing into a concept note with an embed link, so the diagram lives next to the prose it explains. A diagram of the GPU memory hierarchy would sit inside the Episode 5 code note, for instance.

Note: the review plugin is set to ignore `.excalidraw.md` files, so drawings never pollute your flashcard or note-review queues.

### Obsidian Git (backup)
What it is: version control and backup, version 2.38.5. The vault is a git repository, so every note has history and an off-machine backup.

How to use it:
- Run "Obsidian Git: Commit-and-sync" at the end of a session, or set an auto-commit interval in the plugin settings so it backs up on a timer.
- The weekly pass is a natural commit point: commit after you finish the review.
- Keep this separate in your head from the shipping code repo. The shipping code and shaders for each episode live in their own repository, not in this vault. This repo backs up the brain, that repo holds the artifact.

### Graph view and color groups
The graph is color-coded. The groups are set in the graph settings panel, so open the graph and expand Color groups to see the legend live. The scheme:
- Maps, meaning your MOCs, are gold, so the hubs stand out.
- The project and its episodes are magenta.
- Each knowledge domain has its own color: ai blue, graphics green, math red, tech-art orange, gamedev teal, gpu purple, tools grey, career light green. Concept notes and sources take their domain color. The meta docs and daily notes carry no domain, so they stay the default node color.

A note with several domains matches several groups and still shows one color, decided by the group order in the list. Maps and Projects are placed first, so hubs and production nodes always keep their own color. To change which domain a multi-domain note shows, drag the groups into the order you want in the graph settings panel. The graph recolors live as you reorder, so you set it by eye rather than by remembering a rule. If you edit the colors in the config and the graph looks unchanged, close the graph tab and reopen it.

How to read it:
- A tight cluster is a well-linked topic. The linear-algebra notes pull together around [[moc-math]].
- A node floating with one thin link is a note that needs another neighbour or a MOC link. That is your cue to adopt it in the weekly pass.
- As a domain grows into a dense blob, that is the signal to split a sub-MOC out of it.

## What updates itself, and what you keep by hand
Nothing warns you when a static list goes stale, so know which is which.
- Updates itself: every Dataview block (the Home query blocks, the two blocks in each MOC, the weekly queries) and every Base (papers, concepts, episodes). These read the notes and refresh on their own. You never hand-edit them.
- You keep by hand: the Maps list and the Saved collections links on [[Home]]; each MOC's Curated entry points and Sub-maps lists; a source note's Concepts this seeds list; and the links inside an episode hub. When you add a new MOC, a new base, or a note worth featuring, add its link to these lists yourself. The live queries will already include the note in their tables; these curated lists are the human-picked shortcuts on top.

## Making things, the end-to-end recipes
Every creatable item, from nothing to a finished, linked thing. Most recipes start the same way, with "Templater: Create new note from template," which fills the frontmatter and dates for you. The narrative versions of the note recipes are under Day in, day out below; these are the short checklists.

What you never invent:
- Domains. The eight values (ai, graphics, tech-art, gamedev, math, gpu, tools, career) are fixed. A new subject is not a new domain. It is a topic tag, and once the cluster is big enough, a sub-MOC.
- Property keys. The frontmatter fields are fixed per type, listed in [[vault-guide]]. You fill them, you do not add new ones, so the queries and bases keep working.

### Make a concept note
1. Create from t-concept. Name it lowercase kebab and singular, like dot-product.
2. Write the one-line definition, the intuition, the detail, in your own words.
3. Fill Connects to (a neighbour), Map (its MOC, for example [[moc-math]]), and Sources.
4. Set domain (one or several) and a #topic tag. Leave status at seed.
5. Write at least one #flashcard prompt under Recall.
Finished when it links to a neighbour and a MOC and carries a recall prompt.

### Make a source note
1. Create from t-source. Name it type-author-year-slug, like video-sanderson-2016-linear-algebra.
2. Fill source_type, author, year, url, domain, and a #topic tag. Set status to growing when you begin it.
3. As you study, list each atomic note you spin off under Concepts this seeds.

### Make a daily note
Run "Open today's daily note." It is created in Journal from t-daily and the date fills itself. Scratch only.

### Make a weekly note
Create from t-weekly with "Templater: Create new note from template." There is no auto-scheduler for these, so you make one when you sit down to do the weekly pass. Name it for the week, the date of that Monday works. Then follow the weekly pass below.

### Make a map (MOC)
There are two kinds and they filter differently. This is the step most people miss.

A domain MOC, one of the eight top-level subjects:
1. You rarely need this, since all eight already exist. If you do, create from t-moc and name it moc-domain.
2. Set domain in the frontmatter.
3. In both Dataview blocks, change the filter to your domain. Change `contains(domain, "ai")` to `contains(domain, "graphics")` in the notes block and again in the sources block. There are two filters, not one.
4. Add the Curated entry points by hand and add the MOC to the Maps list on [[Home]].

A sub-MOC, a cluster inside a domain such as transformers or diffusion:
1. Create from t-moc and name it moc-topic, like moc-transformers.
2. A sub-MOC is not a new domain. Its notes keep their real domain (ai), so you filter by the topic tag, not by domain. Replace the notes block with a tag filter:
```dataview
TABLE status, updated FROM "Notes"
WHERE contains(file.tags, "#topic/transformers")
SORT status ASC, file.name ASC
```
and replace the sources block the same way, with FROM "Sources" instead of "Notes".
3. Move the relevant Curated entry points into it, link it from the parent MOC's Sub-maps section, and add it to the Maps list on [[Home]] if you want it on the dashboard.

### Make a tag
A tag is not created anywhere special. It exists the moment you type it on a note. The discipline is the naming, not the making:
- Topic theme: #topic/thing, kebab and singular, like #topic/diffusion. Nest deeper when a topic earns it, like #topic/diffusion/sampling.
- Medium: only the three the series uses, #medium/shader, #medium/plot, #medium/code.
- Fixed marker tags: #flashcard, #review, #has-code, #series, #production.
Before inventing a tag, check it is not already a property. Do not tag #concept or #ai, since type and domain already carry those. A tag is for a cross-cutting theme no property captures.

### Make an episode
Clone Episode 1. The full step list is in [[workflows]] under "How to start episode N." In short: copy the ep01 folder, rename the four files to epNN-slug, repoint the internal links, set module and episode, reset the statuses.

### Make a base
Run "Bases: Create new base," save it in Maps, link it from [[Home]]. Filter and sort in the interface. You do not write query text. More in the Bases section above.

### Make a drawing
Run "Excalidraw: Create new drawing," save it in Assets, and embed it in the note it explains by putting an exclamation mark in front of the link.

### Make a project
For a new effort beyond the series, create from t-project. Set project_status to active and a start date. It appears in the Active projects block on [[Home]] on its own.

## Day in, day out

### Studying a course or video right now
1. Make the source note first. "Templater: Create new note from template," pick t-source, name it like `video-author-year-slug`. Fill source_type, author, year, url, set status to growing once you start.
2. As each idea lands, make its atomic note. t-concept, one idea, your own words. Do not keep a running lecture log.
3. Before leaving each note: link a neighbour, link its MOC under the Map section, add a domain and a `#topic` tag, write one `#flashcard` prompt. This is exactly how the six linear-algebra notes were built from [[book-mml-deisenroth]] and [[video-3blue1brown-linear-algebra]].
4. Add each new note to the source's "Concepts this seeds" list, so the source remembers what it grew.

### A thought with nowhere to go yet
Put it in today's daily note under Capture. It is scratch. When it becomes a real idea, promote it to a concept note the same day and clear it from the daily note. The daily note is a holding pen, never the record.

### Promoting a daily note thought into a concept note
This step is manual on purpose. Naming the note and choosing its links is the learning, so no tool does it for you. There are two clean ways to do it. Pick by how much text you are moving.

Fast path, for a line or two already written in the daily note (uses the core Note Composer):
1. Select the text of the thought in the daily note.
2. Run "Note Composer: Extract current selection" from the command palette. Obsidian moves the text into a new note and leaves a link to it in the daily note in its place.
3. Open the new note and finish it: add the frontmatter (type concept, a domain, status seed, a topic tag), rewrite the idea in your own words, fill the Connects to, Map, and Sources links, and add a #flashcard prompt.

Clean path, for a fresh idea you will expand from scratch:
1. Run "Templater: Create new note from template," pick t-concept, name it. The frontmatter, the Map slot, and the Recall slot are already in place.
2. Write the idea, fill the Connects to, Map, and Sources links, set the domain and a #topic tag.
3. Back in the daily note, replace the raw line with a link to the new note, so the daily note points at where the thought now lives.

Either way the result is the same: a durable atomic note, linked, with a recall prompt, and a daily note that is back to being scratch. Do it the same day, while the idea is still fresh.

### Working an episode that day
- Planning or status change: the hub, epNN-slug.md. Set the channel statuses and paste artifact links here.
- Drafting narration: epNN-script.md. Build beats, link the concept notes each beat draws from.
- Drafting the written post: epNN-blog.md.
- Build plan, HLSL notes, understanding snippets: epNN-code.md. The shipping code goes to the separate repo, the snippet that teaches the idea stays here.
- The concept notes the episode needs are written through the class-notes flow above, not pre-stubbed.

### Adding a code snippet
Keep the small version that teaches the idea inside the concept note, tag the note `#has-code`, and link out to the repo path for the full version. The test: if the snippet is what made the idea click, it belongs in the note. If it is what ships, it belongs in the repo.

## The weekly pass
Make a weekly note from t-weekly and work top to bottom. This is the t-weekly checklist turned into a procedure:
1. Empty 00-Inbox. Every file in it gets filed into Sources, Notes, or Assets, or deleted. The folder ends empty.
2. Promote maturity. The weekly note's seeds query lists every seed note, oldest first. For each, decide: is it now understood and linked (growing), or could you teach it from this note alone (evergreen)? Change the status in the properties panel.
3. Adopt orphans. The orphans query lists notes with no links at all. For each, add a neighbour and a MOC link so it rejoins the graph. Also scan the graph view for nodes hanging by a single thread.
4. Clear due flashcards. Run the review and rate honestly.
5. Pick next week's focus. Write it in the weekly note, and update any episode statuses on the board.
6. Commit-and-sync, so the week's work is backed up.

## Long-term maintenance
Roughly monthly, or whenever a part starts to strain:
- Split a sub-MOC. When a domain MOC's "all notes" table passes about fifteen to twenty entries and a sub-topic has clearly formed, make a new MOC (for example moc-transformers or moc-diffusion), move the curated entry points into it, and link it from the parent MOC's Sub-maps section. The placeholder comment is already in each MOC.
- Promote and prune. Move matured notes to evergreen. Merge two notes that turned out to be one idea. Delete a stub that never grew, rather than leaving it empty.
- Asset hygiene. Confirm episode images use the epNN- prefix so they sort with their episode. Keep Assets from becoming a junk drawer.
- Re-audit lightly. Once in a while, check that every wiki-link still resolves, no note is an orphan, property keys still use underscores, and no stray emoji or dash crept in. This is the same check that produced the earlier review.
- Tooling health. Commit history is current, plugins still match Obsidian 1.12.7 before you update anything (Templater in particular is pinned at 2.20.5 for this version), and the templates have not drifted from how your newest notes are actually written.

## Scaling playbook
At one hundred notes and many episodes the design holds, with these moves:
- Notes stays flat. You never make sub-folders in Notes. Structure comes from links and MOCs, not folders. This is deliberate and it scales.
- MOCs branch. The eight domain MOCs are the trunk. Sub-MOCs branch off them as clusters earn it, as above.
- Tags nest. Topic tags go deeper as needed, for example `#topic/diffusion` then `#topic/diffusion/sampling`, without changing the system.
- Episodes clone. Each new episode copies the Episode 1 folder. The step-by-step clone procedure is in [[workflows]] under "How to start episode N." The epNN- prefix on every file keeps wiki-link names unique across all thirty-three episodes.
- One concept, many domains. A note that spans domains gets several domain values and is linked from several MOCs, rather than being duplicated. [[dot-product]] already lives in math, graphics, and ai at once.

## Best ways (the principles worth keeping)
- Atomic. One idea per note. If it will not fit one note, it is two ideas.
- Own words. A note you copied teaches nothing. Distilling in your own words is the point.
- No orphans. Link to a neighbour and a MOC before you leave a note.
- Honest medium. A visual is a shader only if it renders a continuous field or transform from real values. Data gets a plot, a symbolic algorithm gets a code trace. The tag is a promise, per the [[series-bible]].
- From scratch first. Build the thing by hand before the library version. The library is the closing footnote.
- Snippet versus repo. The teaching snippet stays in the note, the shipping artifact stays in the repo.

## Judgment calls, decided
The decisions that otherwise only come with practice, each turned into a test so you are not guessing on day one.
- One note or two? If you need the word "and" to describe it, or it carries two separate definitions, it is two notes. Split it.
- Which domains? Tag every domain the idea genuinely serves. [[dot-product]] is math, graphics, and ai at once. When unsure, fewer is safe, and you can add a domain later.
- Seed, growing, or evergreen? Seed is just captured. Growing is understood and linking out to neighbours. Evergreen is you could teach the idea from this note alone.
- Time to split a sub-MOC? When a MOC's notes table passes about fifteen to twenty entries and a sub-cluster has a clear name, like transformers. Not before, since a map of three notes helps no one.
- Shader, plot, or code visual? A continuous field or transform driven by real values is a shader. Data such as a loss curve or a metric is a plot. A symbolic or algorithmic process is a code trace. The medium is a promise, per the [[series-bible]].
- Snippet in the note or in the repo? If it is the small version that made the idea click, it goes in the note, tagged #has-code. If it is what ships, it goes in the repo and the note links to it.
- New tag or existing property? If type or domain already says it, use the property. Reach for a new tag only for a cross-cutting theme no property captures.

## Troubleshooting
- A new note shows literal `<% %>` text. Templater is not running. Re-enable it and confirm its template folder.
- Flashcards do not appear in review. The note needs the `#flashcard` tag, and a card needs the `prompt :: answer` shape. Then run the review command, not just open the note.
- A Dataview table is empty. Either no note matches yet, or a property name or folder name in the query is misspelled. Check a note that should match has the exact property.
- A query or an embedded image shows as raw text instead of a table or a picture. You are in editing mode. Press Ctrl+E to switch to reading mode, or use live preview.
- A base is empty. Same as above: no note matches the filter yet. papers.base stays empty until you add a source with `source_type: paper`.
- A link broke after a rename. Obsidian updates links on rename by default. If one slips, the unresolved link shows in the note; retype it from the switcher so it points at the real file.
- The daily note is not filling its date. Confirm Templater's trigger-on-creation is on, since the daily note relies on it to resolve the `<%` fields.
- A Git sync reports a conflict. Rare on a single machine. Open the flagged file. The conflict markers (the rows of less-than, equals, and greater-than signs) wrap both versions. Keep the text you want, delete the marker rows, save, then run Commit-and-sync again.
- A new MOC's table is empty or shows the wrong notes. The query is still filtering on the template's default. For a domain MOC, set both filters to your domain. For a sub-MOC, switch both filters to the topic tag, as in the Make a map recipe.

## Cheat sheet
| Task | Tool | How |
|---|---|---|
| Jump to a note | Core | Ctrl+O, type title or alias |
| Run any command | Core | Ctrl+P |
| New concept or source note | Templater | "Create new note from template" |
| Today's daily note | Core plus Templater | "Open today's daily note" |
| See what links here | Core | Backlinks panel, right sidebar |
| List notes by a filter | Dataview | Live blocks in MOCs and Home |
| Scan the episode board | Bases | Open episodes.base |
| Review flashcards | Spaced Repetition | "Review flashcards," or the status bar count |
| Revisit a whole note | Spaced Repetition | Tag it #review |
| Draw a mechanism | Excalidraw | "Create new drawing," store in Assets |
| Make a new MOC | Templater | t-moc, then set both query filters (domain, or a topic tag for a sub-MOC) |
| Make a new tag | Core | Type a hash and the name on a note, follow the #topic or #medium naming |
| New weekly note | Templater | t-weekly, when you start the weekly pass |
| New project | Templater | t-project, set project_status active |
| Back up the vault | Obsidian Git | "Commit-and-sync" |
| See the structure | Core | Graph view, colored by domain |

The fixed vocabulary (types, domains, statuses, tags) lives in [[vault-guide]]. This handbook does not repeat it, so when in doubt about a value, look there.
