# Monthly Consolidation — Scheduled Task

*The Coach uses this to set up a monthly memory-hygiene job that runs the `consolidate-memory` skill automatically. It is coordinated with the nightly sweep so the two never collide, and it refreshes the ontology once that layer exists.*

## Schedule (coordinate with the nightly sweep)

The nightly sweep runs every night (typically ~2 AM). The monthly consolidation must run **after** that window, on one day a month, so they never overlap.

- **Cron:** `0 3 1 * *` — 3 AM on the 1st of each month (one hour after the nightly sweep's 2 AM window).
- If the user's nightly sweep runs at a different time, offset this to at least one hour later.
- Cowork: create it with the `scheduled-tasks` MCP. Hermes: register the equivalent monthly cron.

## The task prompt (self-contained — paste as the scheduled task's instructions)

> Run the MONTHLY MEMORY CONSOLIDATION for the Obsidian memory vault at `<VAULT PATH>`.
>
> First read the vault's `CLAUDE.md` (memory rules), `reference/`-style protocols if present, and the `consolidate-memory` skill. Then:
> 1. Check `wiki/.sweep-state.json`. If a nightly sweep is currently running, wait a few minutes and retry, or defer — do not run concurrently with it.
> 2. Run a full `consolidate-memory` pass over the vault: merge duplicate pages (preserving every distinct fact and citation), reconcile stale or contradicted facts, prune or fold orphans, repair broken `[[links]]`, dedupe and update `index.md`, and add takeaways where enough evidence now exists.
> 3. If a `wiki/ontology/` layer exists, refresh it: re-classify new or changed pages onto the controlled vocabulary, extend the vocabulary only when clearly warranted, refresh hubs and cross-domain bridges, and keep classification additive so the graph does not thrash. Update `/.obsidian/graph.json` color groups only if projects or themes were added.
> 4. Append one summary entry to `wiki/log.md` (operation: `consolidate | monthly`) listing merges, prunes, fixes, and any ontology changes.
> 5. Make the safe, clear fixes automatically. For large or risky structural changes, do them but call them out clearly in the log so the user can review. Never modify `raw/` or the user's own top-level notes.
>
> When done, report a concise summary.

Replace `<VAULT PATH>` with the user's actual vault path before creating the task.

## Notes

- This job **grows with the system**: set it up during Phase 1 (memory), and it does memory hygiene only. Once Phase 4 (ontology/graph) is in place, the same monthly job automatically starts refreshing the ontology too, because step 3 checks for `wiki/ontology/`. No second cron is needed.
- Approving it is a 🧑 HUMAN-ACTION: the user approves the scheduled task and its permissions once; after that it runs unattended.
