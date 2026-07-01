---
name: consolidate-memory
description: "Run a deep, periodic hygiene pass over the user's memory wiki: merge duplicate pages, reconcile stale or contradictory facts, prune orphans, fix broken links, dedupe the catalog, and (if an ontology exists) refresh classifications, hubs, and cross-domain bridges. ALWAYS use this when the user says 'consolidate memory', 'clean up my memory', 'run a memory review', 'deduplicate the wiki', or when invoked by the monthly consolidation scheduled task. This is the deep monthly counterpart to the light 'tidy' in memory-keeper and the nightly sweep. Do NOT trigger for a single-page edit or a quick save (use memory-keeper for those)."
---

# Consolidate Memory

A reflective, whole-vault hygiene pass. The nightly sweep captures new material fast; this pass, run monthly, keeps the whole memory clean, non-duplicative, and well-structured. It follows the vault's `CLAUDE.md` rules, the sweep protocol, and (if present) the ontology protocol.

## Coordinate with the other jobs (important)

- Do NOT fight the nightly sweep. Run this pass at a time the nightly sweep is not running (the monthly schedule is set for after the nightly window). If `wiki/.sweep-state.json` shows a run in progress, wait or defer.
- This pass is about **restructuring** existing memory, not capturing new sessions. Leave session capture to the nightly sweep.

## Steps

1. **Take stock.** Read `index.md`, `log.md`, and scan `wiki/` (and `ontology/` if it exists). Note counts by topic.
2. **Merge duplicates.** Find pages covering the same thing and merge them into one canonical page, preserving every distinct fact and citation. Update inbound `[[links]]` to point at the survivor.
3. **Reconcile stale facts.** Where a newer source contradicts an older claim, update the claim and note the change; keep the citation trail.
4. **Prune and repair.** Remove or fold in true orphans; fix broken `[[links]]`; add missing `index.md` entries; promote facts-only pages to add takeaways where enough evidence now exists.
5. **Refresh the ontology (only if `ontology/` exists).** Re-classify new or changed pages onto the controlled vocabulary; extend it only when clearly warranted; refresh hubs and any cross-domain bridges; keep classification additive so graph colors do not thrash. Follow the ontology protocol.
6. **Log it.** Append one entry to `wiki/log.md` (operation: `consolidate`) summarizing merges, prunes, fixes, and any ontology changes.

## Mode

Run automatically and conservatively. Make the safe, clear fixes (merges of obvious duplicates, broken-link repair, catalog updates) without asking. For large or risky structural changes (renaming or deleting a major hub, collapsing many pages), do them, but call them out clearly in the log and in the run summary so the user can review. Never touch `raw/` or the user's own top-level notes.
