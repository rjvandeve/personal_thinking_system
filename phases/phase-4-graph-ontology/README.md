# Phase 4 — Graph & Ontology

*Goal: turn your memory — across **every** context-vault — into one navigable, color-coded **map**. The assistant derives a single shared structure (your projects, themes, and the people and things that recur), wires every page in every vault into it, colors the graph by project and vault, surfaces the connections that cross between your separate worlds, and then maintains all of it automatically every night.*

---

## Why this is the capstone

After Phase 1 you have a memory spread across several vaults. After a few weeks of feeding it, that memory is *big* — and a big memory has two quiet problems: within each vault it becomes a "hairball" (everything links to the index and little else, so the graph is a cloud of disconnected dots), and *across* vaults the best connections stay invisible because nothing links your separate worlds.

This phase fixes both by giving the whole brain **one semantic spine**: a small, shared, controlled vocabulary of your **projects → themes → entities**, with every page in every vault classified onto it. The result is hub-and-spoke clusters instead of a hairball, *and* explicit **cross-vault bridges** — the same idea, dependency, or contradiction showing up in two different worlds. The graph becomes something you can actually read at a glance, and the brain finally reasons across contexts, not just inside them.

You don't build any of this by hand. The assistant derives the structure from what's already in your vaults, writes all the files, and configures the graph. Your job is to confirm the structure looks right and approve one optional plugin install.

---

## What you'll end up with

- **One shared ontology** — a small machine-readable file (`_ontology/ontology.yaml`) that is the source of truth for your vaults, projects, themes, entities, and the **cross-vault bridges** between them. It spans every non-private vault so the brain is one mind.
- **A master catalog** (`_ontology/index.md`) — one line per page across every non-private vault; the assistant reads it first.
- **Hub pages** — one page per project, theme, and entity, that acts as the gravity well its related notes orbit. These collapse the "everything orbits the index" star into legible neighborhoods.
- **A colored graph** — every note colored by the project (and vault) it belongs to, hubs in their own color, cross-vault bridges in another. You can read the map by color and zoom into any one project, theme, or world.
- **(Optional) A North-Star page** (`_ontology/North-Star.md`) — if your work has a portfolio or venture structure, a single pinned, read-first page that frames everything: who's who, what reports to what, what the priorities are. The assistant reads it first in every session.
- **Self-maintenance** — the nightly sweep keeps the whole structure current, across all vaults, without you touching it. Vaults you mark private stay out of the shared map entirely.

---

## The four axes (the controlled vocabulary)

The ontology classifies every page on a few axes. The assistant derives these from *your* vaults — the names below are illustrative.

- **Vaults (contexts)** — the physical top level: which world a page lives in. This is set by which vault the page is in, and it's a second color dimension on the graph.
- **Projects** — your primary organizing spine and the main graph color. Every page belongs to exactly one project (a project usually sits in one vault but can span vaults). (e.g. "Client Work", "Personal", "Research".)
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

### Step 1 — Derive one shared ontology across your vaults

The assistant reads *every* non-private vault and proposes a single shared structure: your projects, your top themes (each with a one-line definition), the entities that recur, and any bridges it can spot — including ones that span two different vaults. It seeds this from [`templates/ontology.seed.yaml`](../../templates/ontology.seed.yaml) and fills it with *your* real categories.

> Read all my vaults and derive ONE shared ontology: my projects, my top themes (each with a one-line definition), the people/orgs/products that recur, and any connections that span more than one project or more than one vault. Leave out any vault I marked private. Show me the proposed structure before writing anything — I want to confirm the categories are right.

Review the list together. The point is a *small, stable* vocabulary — a couple dozen themes, not hundreds. Fold near-duplicates together.

### Step 2 — Build the hub pages, bridges, and master catalog

Once you've approved the structure, the assistant writes it out: `_ontology/ontology.yaml` plus one hub page per project, theme, and entity, the cross-vault bridge pages, and the master `_ontology/index.md`; and it adds the classification to every existing page in every non-private vault (its project, its top themes, the entities it mentions) so the links exist.

> Write the ontology to `_ontology/ontology.yaml`, create a hub page for each project, theme, and entity, write bridge pages for the connections that span vaults, build the master `_ontology/index.md`, and tag every page in every non-private vault with its project, top themes, and entities so the graph links them. Keep a log of what you classified.

**North-Star (portfolio/venture users only).** If your work has a portfolio or venture structure, ask for a single read-first page:

> Create a North-Star page at `_ontology/North-Star.md` — one pinned, read-first page that frames my whole portfolio across all my vaults: what the ventures/areas are, who's who, what reports to what, and current priorities. Make it the first thing you read each session.

This page is the assistant's operating context: it reads it before answering, so it always knows the lay of the land. Skip it if your work doesn't have that shape.

### Step 3 — Configure the graph (color by project and vault)

The assistant configures the graph's **native color Groups** so each project gets its own color, each vault is distinguishable, the hubs get a color, and cross-vault bridges get another. This needs nothing installed — it's built into the notes app.

> Configure the graph's native color Groups: one color per project (by its project tag), distinct coloring per vault, one color for the ontology hubs, one for the cross-vault bridges. Tune the layout so the clusters spread out and are readable.

After this, reload the graph (close and reopen the Graph view, or restart the app) to see the colors.

**Optional — node sizing with the Extended Graph plugin.** Native Groups handle *color*. If you also want important hubs to render *larger* (sized by how many notes link to them), install one community plugin:

- 🧑 HUMAN-ACTION: in Obsidian, go to **Settings → Community plugins → Browse**, search for **Extended Graph**, and install + enable it. Tell your coach when it's enabled.
- The assistant then configures it via its settings file (`data.json`): enable **`elements-stats`** and set the **`nodesSizeFunction`** to **`degree`** — that sizes each node by its number of connections, so your hubs grow large and the long-tail notes stay small.

This is purely cosmetic polish — the graph is already useful with color alone. Skip it if you like.

### Step 4 — Wire the refresh into the nightly sweep

The last step makes the structure self-maintaining. The assistant folds the **ontology-refresh protocol** ([`reference/ontology-protocol.md`](../../reference/ontology-protocol.md)) into your existing nightly sweep so that, every night, it classifies new pages across all vaults onto the shared vocabulary, extends the vocabulary only when something genuinely new appears, normalizes synonyms, mines for new cross-vault connections, rebuilds the master catalog, and re-colors if the structure changed — always leaving private vaults out of the shared map.

> Fold the ontology-refresh protocol into my nightly sweep, so every night it classifies new pages across all my vaults, extends the vocabulary only when truly needed, normalizes synonyms, refreshes the cross-vault bridges, rebuilds the master `_ontology/index.md`, and re-colors the graph if the structure changed. Keep private vaults out of the shared map. Log every ontology change.

You don't operate this. Once it's wired, the map stays current on its own.

---

## What "good" looks like

- Your graph reads as colored clusters by project, not a hairball — you can see the shape of your work at a glance.
- Searching the graph for one theme or project isolates just that neighborhood.
- New notes get classified and colored automatically overnight; you never tag anything by hand.
- (If you built one) the assistant opens each session already grounded in your North-Star.

This is the top of the whole arc. With all four phases in place, your assistant remembers your world, sounds and looks like you, builds you tools, and keeps its own map of everything current every night.
