---
name: consolidate-memory
description: "Run a deep, periodic hygiene pass over the user's multi-vault memory brain: within each context-vault merge duplicate pages, reconcile stale or contradictory facts, prune orphans, fix broken links, and dedupe that vault's catalog; resolve items parked in _inbox/; and (if a cross-vault ontology exists) refresh classifications, hubs, the master index, and cross-vault bridges. ALWAYS use this when the user says 'consolidate memory', 'clean up my memory', 'run a memory review', 'deduplicate the wiki', or when invoked by the monthly consolidation scheduled task. This is the deep monthly counterpart to the light 'tidy' in memory-keeper and the nightly sweep. Do NOT trigger for a single-page edit or a quick save (use memory-keeper for those)."
---

# Consolidate Memory

A reflective, whole-brain hygiene pass across every context-vault. The nightly sweep captures and routes new material fast; this pass, run monthly, keeps each vault clean and non-duplicative and keeps the shared cross-vault map well-structured. It follows the brain root `CLAUDE.md` (routing + synthesis), each vault's `CLAUDE.md`, the sweep protocol, and (if present) the ontology protocol.

## Coordinate with the other jobs (important)

- Do NOT fight the nightly sweep. Run this pass at a time the nightly sweep is not running (the monthly schedule is set for after the nightly window). If `_ontology/.sweep-state.json` shows a run in progress, wait or defer.
- This pass is about **restructuring** existing memory, not capturing new sessions. Leave session capture to the nightly sweep.

## Steps

1. **Take stock.** Read the root `CLAUDE.md` (note which vaults are `private: true`), the master `_ontology/index.md`, and each vault's `index.md` + `log.md`; scan each vault's `wiki/` (and `_ontology/` if it exists). Note counts by vault and topic.
2. **Merge duplicates — within each vault.** Find pages covering the same thing and merge them into one canonical page, preserving every distinct fact and citation. Update inbound `[[links]]` to point at the survivor. (Don't merge across vaults; instead surface cross-vault overlap as a bridge in step 5.)
3. **Reconcile stale facts.** Where a newer source contradicts an older claim, update the claim and note the change; keep the citation trail.
4. **Prune, repair, and clear the inbox.** Remove or fold in true orphans; fix broken `[[links]]`; add missing `index.md` entries; promote facts-only pages to add takeaways where enough evidence now exists. Resolve `_inbox/` stubs into their correct vault where the context is now clear; leave genuinely ambiguous ones and note them for the user.
5. **Refresh the cross-vault ontology (only if `_ontology/` exists).** Re-classify new or changed pages across all non-private vaults onto the shared vocabulary; extend it only when clearly warranted; refresh hubs and **cross-vault bridges**; rebuild the master `_ontology/index.md`; keep classification additive so graph colors do not thrash. Never surface a `private: true` vault across contexts. Follow the ontology protocol.
6. **Log it.** Append one entry to `_ontology/log.md` (operation: `consolidate`) summarizing per-vault merges, prunes, fixes, inbox resolutions, and any ontology changes.

## Mode

Run automatically and conservatively. Make the safe, clear fixes (merges of obvious duplicates, broken-link repair, catalog updates, clear inbox resolutions) without asking. For large or risky structural changes (renaming or deleting a major hub, collapsing many pages, proposing a whole new vault), do the safe ones and call the risky ones out clearly in the log and run summary so the user can review — and never create a new vault on your own. Never touch any `raw/` or the user's own top-level notes.
