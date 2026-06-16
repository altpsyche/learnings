---
title: Vault Handbook
type: moc
created: 2026-06-16
updated: 2026-06-16
---
# Vault Handbook

The operator's manual. How to actually drive this vault day to day, get the most out of every plugin, and keep it healthy as it grows. Read [[vault-guide]] first for what the parts are, and keep [[workflows]] open for the short rules. This document is the long version with steps, examples from your own notes, and the rhythms.

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
- Quick switcher. Press Ctrl+O, type part of a note title or alias, jump there. Your aliases (for example "matmul" and "GEMM" on [[matrix-multiplication]]) make this fast.
- Command palette. Press Ctrl+P and type the start of any command. Almost everything below is a command you can run from here.
- Backlinks and outgoing links. The right sidebar shows what links to the current note and what it links out to. This is how you check a note is not an orphan: open it, look at backlinks, confirm a MOC is in the list.
- Properties panel. The frontmatter at the top of a note is editable as fields. Changing status from seed to growing here is what moves the note between the Home queries.
- Graph view. Open it from the left ribbon or the command palette. Nodes are notes, lines are links. With the color groups set up (see below) you can see each domain as a color and spot a note drifting on its own.

### Dataview (live queries)
What it is: a community plugin that runs a small query language inside a note and renders a live table or list. Version 0.5.68 here.

Where it already runs:
- [[Home]] has six blocks: active projects, the reading queue, seeds to grow, orphans, recently touched, and the links to the Bases.
- Every MOC has two blocks: all notes in that domain, and the sources in that domain. For example [[moc-math]] lists all six linear-algebra notes because they each carry `domain: [math]`.
- The weekly template has a seeds block and an orphans block.

How to use it:
- These tables update themselves. You never edit them by hand. You change a note's frontmatter and the tables re-sort on next open.
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
The graph is color-coded by domain (the groups are set in the graph settings). Maps show as one color, the project and its episodes as another, and each knowledge domain as its own.

How to read it:
- A tight cluster is a well-linked topic. The linear-algebra notes pull together around [[moc-math]].
- A node floating with one thin link is a note that needs another neighbour or a MOC link. That is your cue to adopt it in the weekly pass.
- As a domain grows into a dense blob, that is the signal to split a sub-MOC out of it.

## Day in, day out

### Studying a course or video right now
1. Make the source note first. "Templater: Create new note from template," pick t-source, name it like `video-author-year-slug`. Fill source_type, author, year, url, set status to growing once you start.
2. As each idea lands, make its atomic note. t-concept, one idea, your own words. Do not keep a running lecture log.
3. Before leaving each note: link a neighbour, link its MOC under the Map section, add a domain and a `#topic` tag, write one `#flashcard` prompt. This is exactly how the six linear-algebra notes were built from [[book-mml-deisenroth]] and [[video-3blue1brown-linear-algebra]].
4. Add each new note to the source's "Concepts this seeds" list, so the source remembers what it grew.

### A thought with nowhere to go yet
Put it in today's daily note under Capture. It is scratch. When it becomes a real idea, promote it to a concept note the same day and clear it from the daily note. The daily note is a holding pen, never the record.

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

## Troubleshooting
- A new note shows literal `<% %>` text. Templater is not running. Re-enable it and confirm its template folder.
- Flashcards do not appear in review. The note needs the `#flashcard` tag, and a card needs the `prompt :: answer` shape. Then run the review command, not just open the note.
- A Dataview table is empty. Either no note matches yet, or a property name or folder name in the query is misspelled. Check a note that should match has the exact property.
- A base is empty. Same as above: no note matches the filter yet. papers.base stays empty until you add a source with `source_type: paper`.
- A link broke after a rename. Obsidian updates links on rename by default. If one slips, the unresolved link shows in the note; retype it from the switcher so it points at the real file.
- The daily note is not filling its date. Confirm Templater's trigger-on-creation is on, since the daily note relies on it to resolve the `<%` fields.

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
| Back up the vault | Obsidian Git | "Commit-and-sync" |
| See the structure | Core | Graph view, colored by domain |

The fixed vocabulary (types, domains, statuses, tags) lives in [[vault-guide]]. This handbook does not repeat it, so when in doubt about a value, look there.
