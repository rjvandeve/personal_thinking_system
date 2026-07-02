# Wiki Sweep Protocol (multi-vault)

*The full mechanics behind the nightly memory sweep. You don't need to read this to use the sweep — the [helper guide](../phases/phase-1-memory/helper-nightly-sweep.md) covers the day-to-day. This is the reference for whoever sets it up or wants to tune it.*

**Purpose:** Automatically capture knowledge from *all* of your assistant sessions and any new connected documents into memory — not just deliberate hand-fed material — and file each item into the **context-vault it belongs to**. This closes the gap left by manual feeding, which only captures what you remember to file. Without the sweep, strategic, research, and creative sessions (plans, analyses, drafts, decisions) never reach memory.

**Mode:** Fully automatic. The sweep captures everything it judges memory-worthy without waiting for approval, routes it by content, and logs every change. The one thing it does **not** do silently is guess a vault it isn't confident about — those go to `_inbox/` for a one-tap human confirm.

**Run cadence:** Nightly (a recurring scheduled job), plus an optional one-time historical backlog sweep. The protocol is **resumable** — each run processes what it can and records progress, so an interrupted run continues next time.

---

## The shape it operates on (the brain)

```
<brain root>/
  _ontology/            ← cross-vault vocabulary + master index (the "singular interface")
    .sweep-state.json   ← the one state file for the whole brain
  _inbox/               ← items the sweep could not confidently route
  vaults/<context>/     ← one physically separate vault per context (raw/ + wiki/ + CLAUDE.md)
```

The sweep captures once, then **routes by content** into the right `vaults/<context>/`. It never dumps everything into one place.

---

## How it's triggered (both runners)

The sweep is the same logic on either runner; only the trigger differs.

- **Claude Cowork** — a **scheduled task** (via the scheduled-tasks tooling) fires nightly and tells the session to run this protocol. It reads past sessions using the session-info tooling (list sessions, read a transcript).
- **Hermes** — a **cron** entry fires nightly and launches the runner to execute this protocol. It reads past sessions from the runner's session history.

Throughout this document, "list sessions" and "read a transcript" mean *whichever mechanism your runner provides*. The rest of the protocol is identical.

---

## State file

`_ontology/.sweep-state.json` (one state file for the whole brain):

```json
{
  "last_run": "ISO timestamp of the most recent completed run",
  "processed_session_ids": ["session ids already swept"],
  "backlog_complete": false,
  "inbox_open": ["ids of items parked in _inbox awaiting a routing decision"],
  "notes": "freeform"
}
```

Read it at the start of every run. Update it incrementally — after each session is processed, add its id — so a crash mid-run loses nothing.

---

## Inputs

**1. Assistant sessions.** List your sessions (raise the limit to cover the backlog) and read each transcript. A session is in scope if its id is **not** in `processed_session_ids`. On nightly runs, also re-check the few most-recently-active sessions in case they gained new content after being processed.

**2. Connected documents.** Scan connected folders for files created or modified after `last_run`. In scope: genuine source material you added (documents, notes, exports). Out of scope: any vault's `wiki/`, every `CLAUDE.md`, `_ontology/`, `_inbox/`, the kit's own folders, and anything already mirrored in a vault's `raw/`.

---

## Triage — what is memory-worthy

**Capture:** decisions and their rationale; durable facts and figures; entities (people, companies, products, projects); research findings; deliverables produced (a plan, essay, analysis, deck) and their key conclusions; strategic or positioning discussions; anything reusable in a future session.

**Skip:** transient tool debugging with no durable takeaway; trivial back-and-forth; sessions that only build or edit this kit; pure formatting or one-off mechanical tasks. When a session is mixed, capture the durable parts and skip the noise.

If a session yields nothing worth keeping, still mark its id processed (with a one-word note) so it isn't re-examined.

---

## Route — decide which vault it belongs to (classify by content)

For every memory-worthy item, decide its context **from the content**, not from which folder happened to be connected:

1. Read the item and match it against the **context definitions** (in the brain's root `CLAUDE.md`) and the `_ontology/` vocabulary — the projects, entities, and themes each context owns.
2. **Confident, single context** → file it into that `vaults/<context>/`.
3. **Spans two contexts** → file it in the primary context and add a cross-vault link so the secondary context still sees it (the ontology stage turns this into a bridge).
4. **Not confident** (no clear match, or a genuine tie) → **do not guess.** Write a short stub to `_inbox/<short-id>-<slug>.md` recording the item, a one-line summary, and the 1-3 candidate vaults, and add its id to `inbox_open` in the state file. It surfaces for a one-tap human confirm; once resolved it gets filed. **Never drop an item.**

A brand-new context is a bigger decision than a new topic: if a run keeps producing `_inbox/` items that clearly form a new context of their own, **flag it for the user** rather than silently creating a new vault — creating a vault is a physical/privacy decision the person should make.

---

## Save the source to the vault's `raw/` (provenance — REQUIRED)

Before (or alongside) writing the wiki page, **save the immutable source to the destination vault's `raw/`**, exactly as the manual feed workflow does. A wiki page must never be the only copy of its source.

1. For a **session**: export the full transcript (high limit) and write it verbatim to `vaults/<context>/raw/<topic>/<short-id>-<short-slug>.md` with a small header (`title`, `session_id`, `context`, `topic`, `type: raw-transcript`, `captured: <date>`). One raw file per session; reuse it if multiple pages cite the same session. If a transcript is too large to capture whole, save head + tail and note the elision. If a transcript is unreadable, write a short stub raw file recording that, so provenance still resolves.
2. For a **document**: copy the original into `vaults/<context>/raw/<topic>/` (kebab-case name).
3. Redact obvious live secrets (API keys, tokens, private keys) from the raw copy and flag them — never store a working credential verbatim.

Then set the wiki page's frontmatter `sources:` to the **raw file path(s)** (e.g. `sources: [raw/projects/4e93c1be-quarterly-review.md]`), not just the session title. Never leave `sources: []`.

---

## Compile — how to write it

Follow the page format in the **destination vault's** `CLAUDE.md` exactly: frontmatter (including `context:`), **Facts first**, **Takeaways** only when there's enough. Cite the source as the session title + id (e.g. `[session: "Q4 planning" <id>]`) and point `sources:` at the `raw/` file saved above.

- **One source page per session** (type `source`), under the right topic in the right vault.
- **Update existing topic/entity pages** when a session adds to something already known; link with `[[wiki-links]]`.
- Prefer enriching an existing page over creating a near-duplicate.

---

## Topic routing (within the chosen vault)

Once the vault is chosen, route to an existing topic within it when it fits. When a session clearly belongs to a recurring area of that context that deserves its own topic, **create the topic automatically**: add it to the topic list in that vault's `CLAUDE.md`, create `wiki/<topic>/` and `raw/<topic>/`, and note the new topic in the run log. (Creating a new *topic* inside a vault is automatic; creating a whole new *vault/context* is not — see Route step 4.)

---

## Refresh the cross-vault ontology (optional — fully automatic when enabled)

*Skip this section if you haven't set up an ontology layer. It's the Phase 4 add-on that structures the knowledge graph; the sweep works fine without it.*

If a controlled vocabulary lives in `_ontology/ontology.yaml`, run the [ontology refresh](ontology-protocol.md) as the final stage, across **all non-private vaults**:

1. **Classify** each new or updated page onto the existing vocabulary: set frontmatter `project:` / `concepts:` / `entities:` / `keywords:`, merge `tags:`, and add an ontology line linking the relevant hubs.
2. **Extend** the vocabulary only when something genuinely doesn't fit; regenerate the hub, link it, bump `version`.
3. **Normalize** synonyms into one canonical concept.
4. **Mine cross-vault gaps** — detect related-but-unlinked concepts that appear in more than one vault; add or refresh a bridge in `_ontology/`. These cross-context bridges are the single highest-value output of the whole system.
5. **Update the master index** `_ontology/index.md` so it lists every page across every non-private vault.
6. **Exclude `private: true` vaults** from steps 4-5 entirely — classify their pages inside their own vault only.

Log ontology changes in the run entry. Keep nightly classification additive so the graph stays stable.

---

## Finish each run

1. Update each touched vault's `wiki/index.md`, and the master `_ontology/index.md` (non-private vaults), with new and changed entries.
2. Append one entry to the touched vault's `wiki/log.md` (and a brief roll-up to `_ontology/log.md` if present):

   ```
   ## [YYYY-MM-DD] sweep | nightly|backlog
   - Sessions processed: N (ids…)
   - Routed: acme=N, board-seat=N, personal=N, _inbox=N
   - Pages created / updated: …
   - New topics / bridges: …
   - Backlog remaining: ~N sessions (or "complete")
   ```
3. Update `_ontology/.sweep-state.json` (`last_run`, append processed ids, refresh `inbox_open`, set `backlog_complete: true` when the full session history is done).

---

## Batch sizing & resumability

Process sessions in modest batches (about 10-20 per run) so a single run completes cleanly. The backlog run repeats until `backlog_complete` is true; the nightly run then only handles new sessions and docs since `last_run`. Because state is updated per session, any run can stop and resume safely.

---

## Guardrails

- **Never** modify any `raw/` or the person's own root personal notes — read only.
- **Route by content; when unsure, use `_inbox/` — never guess a vault, never drop an item.**
- **Never** create a new *vault/context* automatically — flag it for the user. (New *topics* inside a vault are fine.)
- **Respect `private: true`** vaults — capture into them, but keep them out of cross-vault surfacing.
- **Always** cite the source, and update the touched vault's `index.md` + `log.md`, the master index, and the state file.
- Facts first; add Takeaways only with enough evidence.
- Keep the wiki a *compiled* knowledge base, not a transcript dump — capture the knowledge, not the chatter.

---

## Relationship to hand-feeding

Deliberate feeding (the *Feeding* helper) remains the precise path for important documents you want confirmed and emphasized right away. The sweep is the **safety net** that catches everything else and routes it into the right context automatically. They coexist; the sweep simply ensures nothing of value is lost — or misfiled — just because you didn't think to file it yourself.
