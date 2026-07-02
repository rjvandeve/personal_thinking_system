---
name: memory-keeper
description: "Maintain and use the user's personal memory: a multi-vault brain (one physically separate vault per context, tied together by a shared cross-vault map). ALWAYS use this skill when the user wants to (a) SAVE something to memory: 'remember this', 'save this', 'add this to memory', 'keep this', 'file this', or hands over a document, notes, or a link to absorb; (b) GET BRIEFED from memory: 'what do we know about', 'brief me on', 'catch me up on', 'remind me about', or asks a question that should be answered from their own prior work rather than the open internet; or (c) TIDY memory: 'clean up memory', 'is memory current', 'find gaps', 'tidy the wiki'. The brain root holds a root CLAUDE.md (routing + synthesis rules), _ontology/ (the shared cross-vault map), _inbox/, and vaults/<context>/ each with its own raw/, wiki/, and CLAUDE.md. Do NOT trigger for casual chat, quick factual web questions, or code. When a request is clearly about the user's own accumulated knowledge, use this."
---

# Memory Keeper

Maintain and use the user's compounding memory, which is a **multi-vault brain**: the connected folder is the brain root, holding `_ontology/` (the shared cross-vault map), `_inbox/` (unrouted items), and one physically separate vault per context under `vaults/<context>/`. The authoritative rules live in the brain root `CLAUDE.md` (routing + synthesis) and each vault's own `CLAUDE.md` (its memory rules, its `context:` and `private:` flags); read them first if present and follow them. This skill makes the memory operations trigger automatically rather than relying only on those always-loaded rulebooks.

Each vault has three parts: `raw/` (immutable sources), `wiki/` (compiled pages, one per topic), and `index.md` + `log.md` (that vault's catalog and history). The brain-wide catalog across all non-private vaults is `_ontology/index.md`.

## Operation A: Feed it (save to memory)

1. Read the material the user handed over.
2. **Decide which context-vault it belongs to, by content** (match it against the context definitions in the root `CLAUDE.md`). If you can't decide confidently, drop a stub in `_inbox/` naming the candidate vaults and ask — never guess a vault, never drop it. If it spans two contexts, file it in the primary one and cross-link.
3. Summarize the key points in plain language and ask if anything should be emphasized.
4. Save the original into that vault's `raw/<topic>/` (if it was pasted text or a new file).
5. Create or update a facts-first `source` page in that vault's `wiki/<topic>/`, citing the raw source.
6. Read that vault's `index.md`, update related pages, and link them with `[[wiki-links]]`.
7. Update that vault's `index.md` and append to its `log.md` (and the master `_ontology/index.md` if it exists and the vault is not private).
8. Tell the user, in one or two sentences, which vault you filed it in and what you connected.

## Operation B: Get briefed (answer from memory)

1. Read the master `_ontology/index.md` first (if it exists) to see what's known across every vault; otherwise read each relevant vault's `index.md`.
2. Pull relevant pages from **every** relevant vault and answer, citing pages by name and noting which vault. Synthesize across contexts — the cross-vault connection is the highest-value answer. Do NOT read a `private: true` vault unless the user is explicitly working in that context or names it.
3. If the answer is substantial and reusable, offer to save it as a `summary` page in the right vault.
4. If memory has nothing relevant, say so plainly rather than guessing, and offer to research and then file it.

## Operation C: Tidy (light lint)

Report, as a short prioritized list, any: orphan pages, facts-only pages ready for takeaways, broken links, missing catalog entries, outdated or contradicted facts, and anything sitting in `_inbox/` awaiting a routing decision. Wait for approval before changing anything. For a deep monthly pass, defer to the `consolidate-memory` skill.

## Rules

- Never modify any `raw/` or the user's own top-level notes.
- Route by content; when unsure use `_inbox/`; never auto-create a whole new vault (that's a privacy decision for the user) — new topics inside a vault are fine.
- Respect `private: true` vaults: maintain them, but keep them out of cross-vault answers and the master index.
- Always update the touched vault's `index.md` and `log.md` (and the master index) on any change.
- Always cite sources; no unsourced claims in the wiki.
- Ask before creating a new topic or saving a question's answer as a page.
- Keep the wiki a compiled briefing, not a transcript dump.
