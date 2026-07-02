# Monthly Consolidation — Scheduled Task

*The Coach uses this to set up a monthly memory-hygiene job that runs the `consolidate-memory` skill automatically. It is coordinated with the nightly sweep so the two never collide, and it refreshes the ontology once that layer exists.*

## Schedule (coordinate with the nightly sweep)

The nightly sweep runs every night (typically ~2 AM). The monthly consolidation must run **after** that window, on one day a month, so they never overlap.

- **Cron:** `0 3 1 * *` — 3 AM on the 1st of each month (one hour after the nightly sweep's 2 AM window).
- If the user's nightly sweep runs at a different time, offset this to at least one hour later.
- Cowork: create it with the `scheduled-tasks` MCP. Hermes: register the equivalent monthly cron.

## The task prompt (self-contained — paste as the scheduled task's instructions)

> Run the MONTHLY MEMORY CONSOLIDATION for the Personal Thinking System brain at `<BRAIN ROOT PATH>`. This brain holds MANY context-vaults under `vaults/`, plus a cross-vault `_ontology/`.
>
> First read the brain's root `CLAUDE.md` (routing + synthesis rules), each vault's own `CLAUDE.md` (note any with `private: true`), and the `consolidate-memory` skill. Then:
> 1. Check `_ontology/.sweep-state.json`. If a nightly sweep is currently running, wait a few minutes and retry, or defer — do not run concurrently with it.
> 2. Run a full `consolidate-memory` pass **within each vault**: merge duplicate pages (preserving every distinct fact and citation), reconcile stale or contradicted facts, prune or fold orphans, repair broken `[[links]]`, dedupe and update that vault's `index.md`, and add takeaways where enough evidence now exists.
> 3. Resolve `_inbox/`: for each parked item, file it into the correct vault if the right context is now clear; leave genuinely ambiguous ones and note them in the summary for the user.
> 4. If a `_ontology/` layer exists, refresh it **across all non-private vaults**: re-classify new or changed pages onto the shared vocabulary, extend the vocabulary only when clearly warranted, refresh hubs and **cross-vault bridges**, rebuild the master `_ontology/index.md`, and keep classification additive so the graph does not thrash. Update `_ontology/.obsidian/graph.json` (or per-vault graph configs) color groups only if projects/vaults were added. **Never surface a `private: true` vault across contexts.**
> 5. Append one summary entry to `_ontology/log.md` (operation: `consolidate | monthly`) listing per-vault merges, prunes, fixes, inbox resolutions, and any ontology changes.
> 6. Make the safe, clear fixes automatically. For large or risky structural changes, do them but call them out clearly in the log so the user can review. Never modify any `raw/` or the user's own top-level notes.
>
> When done, report a concise summary.

Replace `<BRAIN ROOT PATH>` with the user's actual brain-root folder path before creating the task.

## Notes

- This job **grows with the system**: set it up during Phase 1 (memory), and it does per-vault memory hygiene plus `_inbox/` cleanup only. Once Phase 4 (ontology/graph) is in place, the same monthly job automatically starts refreshing the cross-vault ontology too, because step 4 checks for `_ontology/`. No second cron is needed.
- Approving it is a 🧑 HUMAN-ACTION: the user approves the scheduled task and its permissions once; after that it runs unattended.
