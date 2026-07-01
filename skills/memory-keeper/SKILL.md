---
name: memory-keeper
description: "Maintain and use the user's personal memory wiki. ALWAYS use this skill when the user wants to (a) SAVE something to memory: 'remember this', 'save this', 'add this to memory', 'keep this', 'file this', or hands over a document, notes, or a link to absorb; (b) GET BRIEFED from memory: 'what do we know about', 'brief me on', 'catch me up on', 'remind me about', or asks a question that should be answered from their own prior work rather than the open internet; or (c) TIDY memory: 'clean up memory', 'is memory current', 'find gaps', 'tidy the wiki'. The memory lives as markdown in the user's vault; the rules are in that vault's CLAUDE.md. Do NOT trigger for casual chat, quick factual web questions, or code. When a request is clearly about the user's own accumulated knowledge, use this."
---

# Memory Keeper

Maintain and use the user's compounding memory wiki. The authoritative rules and folder layout live in the vault's own `CLAUDE.md` (the memory rulebook); read it first if present, and follow it. This skill makes the memory operations trigger automatically rather than relying only on that always-loaded rulebook.

The memory has three parts: `raw/` (immutable sources), `wiki/` (compiled pages, one per topic), and `index.md` + `log.md` (catalog and history). Group everything under the user's topics.

## Operation A: Feed it (save to memory)

1. Read the material the user handed over.
2. Summarize the key points in plain language and ask if anything should be emphasized.
3. Save the original into `raw/<topic>/` (if it was pasted text or a new file).
4. Create or update a facts-first `source` page in `wiki/<topic>/`, citing the raw source.
5. Read `index.md`, update related pages, and link them with `[[wiki-links]]`.
6. Update `index.md` and append to `log.md`.
7. Tell the user, in one or two sentences, what you filed and what you connected.

## Operation B: Get briefed (answer from memory)

1. Read `index.md` to find relevant pages, then read them.
2. Answer the question from those pages, citing them by name.
3. If the answer is substantial and reusable, offer to save it as a `summary` page.
4. If memory has nothing relevant, say so plainly rather than guessing, and offer to research and then file it.

## Operation C: Tidy (light lint)

Report, as a short prioritized list, any: orphan pages, facts-only pages ready for takeaways, broken links, missing catalog entries, and outdated or contradicted facts. Wait for approval before changing anything. For a deep monthly pass, defer to the `consolidate-memory` skill.

## Rules

- Never modify `raw/` or the user's own top-level notes.
- Always update `index.md` and `log.md` on any change.
- Always cite sources; no unsourced claims in the wiki.
- Ask before creating a new topic or saving a question's answer as a page.
- Keep the wiki a compiled briefing, not a transcript dump.
