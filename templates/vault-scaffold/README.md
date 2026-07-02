# Vault Scaffold — the brain, in starter form

*The Coach copies this whole folder to the user's connected folder (the **brain root**), then adapts it. This scaffold shows the multi-vault shape.*

```
<brain root>/
  CLAUDE.md          ← the Coach writes this from templates/ROOT-CLAUDE.md.template
                       (routing + cross-vault synthesis + the Active Capabilities ledger)
  _ontology/         ← the singular interface across every vault (built out in Phase 4)
    index.md         ← MASTER catalog: every page in every non-private vault
    README.md
  _inbox/            ← items the nightly sweep could not confidently route (one-tap confirm)
    README.md
  vaults/
    EXAMPLE-context/ ← ONE context = ONE physically separate Obsidian vault. Duplicate this
                       per context, rename it, delete the EXAMPLE placeholders.
      CLAUDE.md      ← the Coach writes this from templates/USER-CLAUDE.md.template
      raw/           ← immutable sources for THIS context
      wiki/          ← compiled pages for THIS context (index.md, log.md, topic folders)
  state/PROGRESS.md  ← the Coach writes this from state/PROGRESS.template.md
```

**How to use it (Coach):**
1. Copy this scaffold to the brain root.
2. Write the root `CLAUDE.md` from `ROOT-CLAUDE.md.template`.
3. For each context from the interview, duplicate `vaults/EXAMPLE-context/`, rename it to the context id, write its `CLAUDE.md` from `USER-CLAUDE.md.template` (set `context:` and `private:`), and create one `wiki/<topic>/` + `raw/<topic>/` per topic. Delete the `EXAMPLE-context` and `EXAMPLE-topic` placeholders once real ones exist.
4. `_ontology/` stays mostly empty until Phase 4 (only its master `index.md` grows as the sweep runs); `_inbox/` fills only when the sweep is unsure where something belongs.

Each `vaults/<context>/` is its own Obsidian vault — open it alone in Obsidian and you see only that context. That physical separation is the privacy boundary.
