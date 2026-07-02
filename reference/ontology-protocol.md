# Ontology Refresh Protocol (cross-vault)

*The full mechanics behind the nightly ontology refresh. You don't need to read this to use the system — the [Phase 4 guide](../phases/phase-4-graph-ontology/README.md) covers the day-to-day. This is the reference for whoever sets it up or wants to tune it.*

**Purpose:** Keep the brain's semantic spine current automatically **across every vault**. As new pages land in the vaults (largely from the nightly [Wiki Sweep](wiki-sweep-protocol.md)), they need to be classified onto one shared controlled vocabulary — given their project, their top themes, and the entities they mention — so the graph links them instead of leaving them floating, *including across context boundaries*. This is what makes physically separate vaults behave as one brain. Over time the vocabulary itself must grow carefully, synonyms must be folded together, and new cross-vault connections surfaced. This protocol does all of that.

**Scope:** All vaults under `vaults/` **except** any with `private: true` in their `CLAUDE.md`. Private vaults are classified only *within their own vault* — never pulled into the master index or cross-vault bridges.

**Mode:** Fully automatic. The refresh classifies and maintains without waiting for approval, and logs every change. It runs as a stage *after* the wiki sweep on the same nightly schedule, so it always classifies the pages the sweep just created and routed.

**Run cadence:** Nightly. The protocol is **additive and resumable** — each run classifies what it can and records progress, so an interrupted run continues next time.

**Source of truth:** `_ontology/ontology.yaml` (one shared vocabulary for the whole brain). The protocol reads it, applies it, and is the only thing that edits it. The master catalog `_ontology/index.md`, hub pages, and per-page tags are *derived* from it.

---

## How it's triggered (both runners)

The refresh is the same logic on either runner; only the trigger differs.

- **Claude Cowork** — the nightly **scheduled task** that runs the wiki sweep runs this protocol immediately afterward as its final stage.
- **Hermes** — the nightly **cron** entry runs this protocol after the sweep completes.

Wherever this document says "the controlled vocabulary," it means the `projects`, `themes`, and `entities` defined in `_ontology/ontology.yaml`.

---

## The classification each page carries

Every wiki page across every non-private vault (outside the ontology's own hub pages) ends up with:

**Frontmatter:**
```yaml
project: project-a                          # exactly one project id
concepts: [example-theme-one, example-theme-two]   # canonical theme ids, top 1-5
entities: [example-org, example-person]     # entity ids referenced
keywords: [free, long, tail, terms]         # free text, NOT controlled vocab
tags: [project/project-a, concept/example-theme-one, entity/example-org]
```

**And, near the top of the body, an ontology line** that creates the visible graph edges to the hubs:
```markdown
> **Ontology** — Project: [[Project A (project)]] · Concepts: [[Example Theme One]] · Entities: [[Example Organization]]
```

The frontmatter drives the graph coloring (via the `tags`); the ontology line drives the link edges to the hub pages. Both are derived purely from `_ontology/ontology.yaml`.

---

## The operations (run in this order each night)

Run these across **all non-private vaults**. Skip `private: true` vaults except for step 1 *within their own vault* (they still get local classification; they just never reach the master index or bridges).

### 1. Classify new and changed pages

For every page created or modified since the last run, in any non-private vault:

1. Assign **exactly one project** from the existing project list (the closest fit).
2. Pick the **top 1-5 themes** the page is actually about, using existing canonical theme ids only.
3. List the **entities** (people/orgs/products) the page mentions that already exist in the vocabulary.
4. Write the frontmatter and the ontology line above.

Classification is **additive**: prefer placing a page onto the *existing* vocabulary. Only reach for operation 2 when nothing fits.

### 2. Extend the vocabulary — only when something genuinely doesn't fit

If a page is clearly *about* a concept, person, org, or product that has no home in the vocabulary, add it:

- Add the new theme/entity to `_ontology/ontology.yaml` (id, name, one-line definition for themes; id, name, type for entities; the projects it touches).
- Generate its hub page.
- Bump `version` and set `updated`.

Be conservative. The value of the vocabulary is that it's *small and stable*. A new theme should represent a genuinely distinct idea, not a slight rephrasing of an existing one. When in doubt, classify onto the nearest existing theme and move on.

### 3. Normalize synonyms

Scan for the same idea expressed under different tags ("billing" vs "invoices" vs "payments"). Fold them into the single canonical theme and re-tag the affected pages. Never let one concept fork into multiple tags — that fragmentation is exactly what the controlled vocabulary exists to prevent. Record every fold in the log.

### 4. Mine cross-vault and cross-project gaps (bridges)

Look for concepts, entities, or theses that appear in **more than one project OR more than one vault** but aren't yet linked across them. Where a real structural connection exists — a shared dependency, the same idea applied in two contexts, an unreconciled discrepancy between what one vault knows and what another does — add or refresh a **bridge** in `_ontology/ontology.yaml` and write/update its synthesis page in `_ontology/`. Cross-vault bridges are the highest-value output of the whole system: they are exactly the connections a set of siloed vaults would lose, and the reason the brain is worth more than its parts. **Never bridge into or out of a `private: true` vault.**

### 5. Refresh the master index

Rebuild `_ontology/index.md` so it catalogs **every page across every non-private vault**, one line each, grouped by vault (or by project). This master catalog is the singular interface the brain reads first when answering. Private vaults are omitted entirely.

### 6. Recolor on structural change

If operations 2-4 changed the set of projects or vaults (added, renamed, merged), update the graph's native color Groups so every project/vault still has a distinct color and the hubs/bridges keep theirs. If nothing structural changed, leave the graph configuration alone — don't churn colors night to night.

---

## Logging

Append every ontology change to `_ontology/log.md` under an `ontology` operation: pages classified (and in which vaults), themes/entities added, synonyms folded, cross-vault bridges created or refreshed, master-index rebuilds, recolors applied. The log plus the `version` field in `_ontology/ontology.yaml` make every change traceable.

---

## Stability rules (so the graph doesn't thrash)

- **Additive by default.** Night to night, prefer classifying onto the existing vocabulary over changing it.
- **Reserve renames, merges, and splits** for when the evidence is clear, and always record them in the log — these are the changes that move graph colors around, so they should be deliberate.
- **Keep the vocabulary small.** Resist the drift toward hundreds of near-duplicate themes. A couple dozen well-defined themes is the target; growth past that is usually a sign operation 3 (normalize) needs to run harder.
- **One canonical name per idea, always.** This single rule is what keeps the graph legible.

---

## State file

`_ontology/.ontology-state.json`:

```json
{
  "last_run": "ISO timestamp of the most recent completed run",
  "classified_page_paths": ["vault-qualified page paths already classified this cycle"],
  "ontology_version": 1,
  "notes": "freeform"
}
```

Read it at the start of every run; update it incrementally so an interrupted run resumes cleanly. The `ontology_version` here should always match the `version` in `_ontology/ontology.yaml` after a successful run.
