# Wiki Sweep Protocol

*The full mechanics behind the nightly memory sweep. You don't need to read this to use the sweep — the [helper guide](../phases/phase-1-memory/helper-nightly-sweep.md) covers the day-to-day. This is the reference for whoever sets it up or wants to tune it.*

**Purpose:** Automatically capture knowledge from *all* of your assistant sessions and any new connected documents into the wiki — not just deliberate hand-fed material. This closes the gap left by manual feeding, which only captures what you remember to file. Without the sweep, strategic, research, and creative sessions (plans, analyses, drafts, decisions) never reach memory.

**Mode:** Fully automatic. The sweep captures everything it judges memory-worthy without waiting for approval, and logs every change.

**Run cadence:** Nightly (a recurring scheduled job), plus an optional one-time historical backlog sweep. The protocol is **resumable** — each run processes what it can and records progress, so an interrupted run continues next time.

---

## How it's triggered (both runners)

The sweep is the same logic on either runner; only the trigger differs.

- **Claude Cowork** — a **scheduled task** (via the scheduled-tasks tooling) fires nightly and tells the session to run this protocol. It reads past sessions using the session-info tooling (list sessions, read a transcript).
- **Hermes** — a **cron** entry fires nightly and launches the runner to execute this protocol. It reads past sessions from the runner's session history.

Throughout this document, "list sessions" and "read a transcript" mean *whichever mechanism your runner provides*. The rest of the protocol is identical.

---

## State file

`wiki/.sweep-state.json`:

```json
{
  "last_run": "ISO timestamp of the most recent completed run",
  "processed_session_ids": ["session ids already swept"],
  "backlog_complete": false,
  "notes": "freeform"
}
```

Read it at the start of every run. Update it incrementally — after each session is processed, add its id — so a crash mid-run loses nothing.

---

## Inputs

**1. Assistant sessions.** List your sessions (raise the limit to cover the backlog) and read each transcript. A session is in scope if its id is **not** in `processed_session_ids`. On nightly runs, also re-check the few most-recently-active sessions in case they gained new content after being processed.

**2. Connected documents.** Scan connected folders for files created or modified after `last_run`. In scope: genuine source material you added (documents, notes, exports). Out of scope: `wiki/` (the sweep owns it), `CLAUDE.md`, the kit's own folders, and anything already mirrored in `raw/`.

---

## Triage — what is memory-worthy

**Capture:** decisions and their rationale; durable facts and figures; entities (people, companies, products, projects); research findings; deliverables produced (a plan, essay, analysis, deck) and their key conclusions; strategic or positioning discussions; anything reusable in a future session.

**Skip:** transient tool debugging with no durable takeaway; trivial back-and-forth; sessions that only build or edit this kit; pure formatting or one-off mechanical tasks. When a session is mixed, capture the durable parts and skip the noise.

If a session yields nothing worth keeping, still mark its id processed (with a one-word note) so it isn't re-examined.

---

## Save the source to `raw/` (provenance — REQUIRED)

Before (or alongside) writing the wiki page, **save the immutable source to `raw/`**, exactly as the manual feed workflow does. A wiki page must never be the only copy of its source.

1. For a **session**: export the full transcript (high limit) and write it verbatim to `raw/<topic>/<short-id>-<short-slug>.md` with a small header (`title`, `session_id`, `topic`, `type: raw-transcript`, `captured: <date>`). One raw file per session; reuse it if multiple pages cite the same session. If a transcript is too large to capture whole, save head + tail and note the elision. If a transcript is unreadable, write a short stub raw file recording that, so provenance still resolves.
2. For a **document**: copy the original into `raw/<topic>/` (kebab-case name).
3. Redact obvious live secrets (API keys, tokens, private keys) from the raw copy and flag them — never store a working credential verbatim.

Then set the wiki page's frontmatter `sources:` to the **raw file path(s)** (e.g. `sources: [raw/work/4e93c1be-quarterly-review.md]`), not just the session title. Never leave `sources: []`.

---

## Compile — how to write it

Follow the page format in `CLAUDE.md` exactly: frontmatter, **Facts first**, **Takeaways** only when there's enough. Cite the source as the session title + id (e.g. `[session: "Q4 planning" <id>]`) and point `sources:` at the `raw/` file saved above.

- **One source page per session** (type `source`), under the right topic.
- **Update existing topic/entity pages** when a session adds to something already known; link with `[[wiki-links]]`.
- Prefer enriching an existing page over creating a near-duplicate.

---

## Topic routing

Route to an existing topic (`work`, `learning`, `personal`) when it fits. When a session clearly belongs to a recurring area that deserves its own topic, **create the topic automatically** (fully automatic mode): add it to the topic list in `CLAUDE.md`, create `wiki/<topic>/` and `raw/<topic>/`, and note the new topic in the run log. Use `personal` only for genuinely one-off items.

---

## Refresh the ontology (optional — fully automatic when enabled)

*Skip this section if you haven't set up an ontology layer. It's an advanced add-on that structures the knowledge graph; the sweep works fine without it.*

If a controlled vocabulary lives in `wiki/ontology/ontology.yaml` (projects, themes, entities, bridges), then on every run:

1. **Classify** each new or updated page onto the existing vocabulary: set frontmatter `project:` / `concepts:` / `entities:` / `keywords:`, merge `tags:`, and add an ontology line after the H1 linking the relevant hubs.
2. **Extend** the vocabulary only when something genuinely doesn't fit — add a new theme/entity, regenerate its hub page, link it from the relevant project hub, bump `version`. Prefer reusing an existing concept.
3. **Normalize** — fold synonyms into one canonical concept; never let an idea fork into multiple tags.
4. **Mine gaps** — detect related-but-unlinked concepts; add or refresh a bridge page and register it.

Log ontology changes in the run entry. Keep nightly classification additive so the graph stays stable.

---

## Finish each run

1. Update `wiki/index.md` with new and changed entries.
2. Append one entry to `wiki/log.md`:

   ```
   ## [YYYY-MM-DD] sweep | nightly|backlog
   - Sessions processed: N (ids…)
   - Docs ingested: N
   - Pages created: …
   - Pages updated: …
   - New topics: …
   - Backlog remaining: ~N sessions (or "complete")
   ```
3. Update `wiki/.sweep-state.json` (`last_run`, append processed ids, set `backlog_complete: true` when the full session history is done).

---

## Batch sizing & resumability

Process sessions in modest batches (about 10–20 per run) so a single run completes cleanly. The backlog run repeats until `backlog_complete` is true; the nightly run then only handles new sessions and docs since `last_run`. Because state is updated per session, any run can stop and resume safely.

---

## Guardrails

- **Never** modify `raw/` or your own root personal notes — read only.
- **Always** cite the source (session id/title or document path).
- **Always** update `index.md` and `log.md`, and the state file.
- Facts first; add Takeaways only with enough evidence.
- Prefer updating existing pages over creating duplicates.
- Keep the wiki a *compiled* knowledge base, not a transcript dump — capture the knowledge, not the chatter.

---

## Relationship to hand-feeding

Deliberate feeding (the *Feeding* helper) remains the precise path for important documents you want confirmed and emphasized right away. The sweep is the **safety net** that catches everything else and anything the manual path missed. They coexist; the sweep simply ensures nothing of value is lost just because you didn't think to file it.
