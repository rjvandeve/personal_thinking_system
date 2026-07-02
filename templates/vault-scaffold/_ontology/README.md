# _ontology — the cross-vault brain

This folder is what makes physically separate vaults behave as **one thinking system**.

- `index.md` — the master catalog: every page across every non-private vault, one line each. The assistant reads this first.
- `ontology.yaml` — (Phase 4) the one shared controlled vocabulary: vaults, projects, themes, entities, and the cross-vault **bridges** between them.
- `North-Star.md` — (optional, Phase 4) a pinned, read-first page framing the whole world.
- hub pages + bridge pages — (Phase 4) one hub per project/theme/entity, plus synthesis pages for connections that span vaults.
- `.sweep-state.json` / `.ontology-state.json` — resumable state for the nightly jobs (one set for the whole brain).

You don't edit anything here by hand. The nightly sweep and monthly consolidation maintain it. Vaults marked `private: true` are never represented here.
