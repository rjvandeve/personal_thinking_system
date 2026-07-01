# Phase 4 — Graph & Ontology

*Goal: turn your memory from a flat pile of notes into a navigable, color-coded **map**. The assistant derives a structure (your projects, themes, and the people and things that recur), wires every page into it, colors the graph by project, and then maintains all of it automatically every night.*

---

## Why this is the capstone

After Phase 1 you have a memory. After a few weeks of feeding it, that memory is *big* — and a big flat memory has a quiet problem: it's a "hairball." Everything links to the index and to little else, so the graph view is a cloud of disconnected dots and you can't *see* the shape of what you know.

This phase fixes that by giving the memory a **semantic spine**: a small, controlled vocabulary of your **projects → themes → entities**, with every page classified onto it. The result is hub-and-spoke clusters instead of a hairball — related work pulls together, and the graph becomes something you can actually read at a glance.

You don't build any of this by hand. The assistant derives the structure from what's already in your memory, writes all the files, and configures the graph. Your job is to confirm the structure looks right and approve one optional plugin install.

---

## What you'll end up with

- **An ontology** — a small machine-readable file (`ontology.yaml`) that is the source of truth for your projects, themes, entities, and the cross-project *bridges* between them.
- **Hub pages** — one page per project, theme, and entity, that acts as the gravity well its related notes orbit. These collapse the "everything orbits the index" star into legible neighborhoods.
- **A colored graph** — every note colored by the project it belongs to, hubs in their own color, cross-project bridges in another. You can read the map by color and zoom into any one project or theme.
- **(Optional) A North-Star page** — if your work has a portfolio or venture structure, a single pinned, read-first page that frames everything: who's who, what reports to what, what the priorities are. The assistant reads it first in every session.
- **Self-maintenance** — the nightly sweep keeps the whole structure current without you touching it.

---

## The four axes (the controlled vocabulary)

The ontology classifies every page on a few axes. The assistant derives these from *your* memory — the names below are illustrative.

- **Projects** — your primary organizing spine and the main graph color. Every page belongs to exactly one project. (e.g. "Client Work", "Personal", "Research".)
- **Themes / concepts** — canonical, normalized ideas with a one-line definition each. A page carries its top one-to-five themes. This is the controlled vocabulary: "billing", "invoices", and "payments" all fold into *one* canonical theme so the same idea never forks into three tags.
- **Entities** — the people, organizations, and products that recur across your notes.
- **Keywords** — lighter free-text tags for long-tail terms; *not* part of the controlled vocabulary, so they don't need hubs.

For portfolio / venture users, the ontology can carry two extra optional layers — **ventures** (a parent org and the things it owns) and **research** (research programs or workstreams). These only appear if your work actually has that shape; most users won't need them.

---

## Which runner you're using

- **Claude Cowork** — the desktop assistant. The ontology files and hub pages live in your connected memory folder; the graph is viewed in Obsidian. The nightly refresh is a **scheduled task**.
- **Hermes** — a self-hosted runner. The same files live in its workspace; the nightly refresh is a **cron** entry.

The asks are identical on both; only the "make it run nightly" step differs.

---

## The coached steps

### Step 1 — Derive the ontology from your memory

The assistant reads your whole memory and proposes a structure: your projects, your top themes (each with a one-line definition), the entities that recur, and any cross-project bridges it can spot. It seeds this from [`templates/ontology.seed.yaml`](../../templates/ontology.seed.yaml) and fills it with *your* real categories.

> Read my whole memory and derive an ontology: my projects, my top themes (each with a one-line definition), the people/orgs/products that recur, and any connections that span more than one project. Show me the proposed structure before writing anything — I want to confirm the categories are right.

Review the list together. The point is a *small, stable* vocabulary — a couple dozen themes, not hundreds. Fold near-duplicates together.

### Step 2 — Build the hub pages and tag pages

Once you've approved the structure, the assistant writes it out: `ontology.yaml` plus one hub page per project, theme, and entity, and it adds the classification to every existing page (its project, its top themes, the entities it mentions) so the links exist.

> Write the ontology to `ontology.yaml`, create a hub page for each project, theme, and entity, and tag every existing page with its project, top themes, and entities so the graph links them. Keep a log of what you classified.

**North-Star (portfolio/venture users only).** If your work has a portfolio or venture structure, ask for a single read-first page:

> Create a North-Star page — one pinned, read-first page that frames my whole portfolio: what the ventures/areas are, who's who, what reports to what, and current priorities. Make it the first thing you read each session.

This page is the assistant's operating context: it reads it before answering, so it always knows the lay of the land. Skip it if your work doesn't have that shape.

### Step 3 — Configure the graph (color by project)

The assistant configures the graph's **native color Groups** so each project gets its own color, the hubs get a color, and cross-project bridges get another. This needs nothing installed — it's built into the notes app.

> Configure the graph's native color Groups: one color per project (by its project tag), one color for the ontology hubs, one for the cross-project bridges. Tune the layout so the clusters spread out and are readable.

After this, reload the graph (close and reopen the Graph view, or restart the app) to see the colors.

**Optional — node sizing with the Extended Graph plugin.** Native Groups handle *color*. If you also want important hubs to render *larger* (sized by how many notes link to them), install one community plugin:

- 🧑 HUMAN-ACTION: in Obsidian, go to **Settings → Community plugins → Browse**, search for **Extended Graph**, and install + enable it. Tell your coach when it's enabled.
- The assistant then configures it via its settings file (`data.json`): enable **`elements-stats`** and set the **`nodesSizeFunction`** to **`degree`** — that sizes each node by its number of connections, so your hubs grow large and the long-tail notes stay small.

This is purely cosmetic polish — the graph is already useful with color alone. Skip it if you like.

### Step 4 — Wire the refresh into the nightly sweep

The last step makes the structure self-maintaining. The assistant folds the **ontology-refresh protocol** ([`reference/ontology-protocol.md`](../../reference/ontology-protocol.md)) into your existing nightly sweep so that, every night, it classifies new pages onto the vocabulary, extends the vocabulary only when something genuinely new appears, normalizes synonyms, mines for new cross-project connections, and re-colors if the structure changed.

> Fold the ontology-refresh protocol into my nightly sweep, so every night it classifies new pages, extends the vocabulary only when truly needed, normalizes synonyms, refreshes the cross-project bridges, and re-colors the graph if the structure changed. Log every ontology change.

You don't operate this. Once it's wired, the map stays current on its own.

---

## What "good" looks like

- Your graph reads as colored clusters by project, not a hairball — you can see the shape of your work at a glance.
- Searching the graph for one theme or project isolates just that neighborhood.
- New notes get classified and colored automatically overnight; you never tag anything by hand.
- (If you built one) the assistant opens each session already grounded in your North-Star.

This is the top of the whole arc. With all four phases in place, your assistant remembers your world, sounds and looks like you, builds you tools, and keeps its own map of everything current every night.
