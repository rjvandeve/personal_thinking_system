# Phase 1 — Give Your Assistant a Memory

*Goal: stop re-explaining your world every time. Build a memory the assistant reads from and writes to, so every conversation is better-informed than the last.*

---

## Why this is first

Everything else stands on this. An assistant with no memory is a brilliant stranger you meet again every morning — you spend half your time bringing it up to speed. An assistant *with* memory is a colleague who's been with you for years.

By the end of this phase you'll have a tidy, organized knowledge base — built and maintained mostly by the assistant itself — covering the projects, people, documents, and decisions that matter to you. When you ask a question, the assistant reads its own notes first and answers from what it already knows about *you*, not just the internet.

---

## What you'll be able to do

- **Get briefed** on any project in seconds, drawing on everything you've fed it.
- **Stress-test decisions** against your own accumulated knowledge.
- **Drop in a document** (a report, an email thread, meeting notes) and have it permanently absorbed — summarized, filed, and connected to what you already knew.
- **Ask "what do we know about X?"** and get a sourced answer instead of a guess.

---

## What you'll end up with

A single folder on your computer that holds three kinds of things. You don't manage these — the assistant does — but it helps to know the shape:

- **Raw** — the original stuff you feed in (a PDF, a pasted email, notes). Never changed, just stored.
- **Wiki** — the assistant's own clean, organized pages. One page per topic, person, project, or idea. This is what gets *smarter over time*.
- **Index & Log** — a table of contents and a running history, so nothing gets lost and you can always see what changed.

Think of it like a well-run research desk: raw clippings in one tray, polished briefings in another, and a catalog so you can always find things.

A starter version of this folder is in [`templates/vault-scaffold/`](../../templates/vault-scaffold/) — copy it to your computer and you have an empty memory ready to fill.

---

## Where this comes from (and why it works)

This isn't a homemade trick. The memory system implements a well-known pattern — the **"LLM Wiki."** The core idea: instead of dumping documents into a black box and hoping for the best, you let the assistant act as a **compiler** — it reads your raw source material and *compiles* it into a clean, organized, interlinked wiki. The raw stays untouched as the record of truth; the wiki is the assistant's polished understanding, and it gets richer every time you add something.

That single idea — *raw in, organized wiki out, never re-deriving from scratch* — is why this beats simply pasting documents into a chat. You're not just storing information; you're building a knowledge base that compounds.

---

## Which runner you're using

This kit works with two kinds of assistant. Wherever setup differs, the helper guides say so explicitly.

- **Claude Cowork** — the desktop assistant. The memory folder is a folder on your own machine that you connect to the session. Automatic jobs (like the nightly sweep) are set up as **scheduled tasks**.
- **Hermes** — a self-hosted runner. The memory folder lives in a workspace it can read and write. Automatic jobs are set up as **cron** entries.

Both end up at the same place: an assistant that reads your memory first and keeps it current. Pick whichever you have; the day-to-day asks are identical.

---

## The coached steps at a glance

Each step has its own short helper guide in this folder.

1. **Set up the folder.** Copy the starter scaffold to your computer, connect it to your assistant, and drop in the memory rulebook (the `CLAUDE.md` file in the scaffold) so the assistant knows how to keep things organized. No accounts to wire together, no code.

2. **Feed it information** → [`helper-feeding-information.md`](helper-feeding-information.md)
   Hand the assistant a document or some notes; it summarizes, files, and connects them.

3. **Get briefed / ask questions** → [`helper-getting-briefed.md`](helper-getting-briefed.md)
   Ask anything; it answers from your memory first, with sources.

4. **Keep it tidy** → [`helper-keeping-memory-tidy.md`](helper-keeping-memory-tidy.md)
   Every so often, ask it to clean up — find gaps, fix broken links, flag outdated facts.

5. **Let it update itself** → [`helper-nightly-sweep.md`](helper-nightly-sweep.md)
   A nightly automatic job that sweeps your recent conversations and new documents into memory, so you don't have to remember to feed everything. Set up once (scheduled task on Cowork, cron on Hermes).

---

## Your first session

1. Confirm the folder is connected and the `CLAUDE.md` rulebook is in place.
2. Feed in **one** real document you care about (see the Feeding guide).
3. Ask the assistant to **brief you** on it (see the Getting Briefed guide).
4. Feed in a **second, related** document and watch it connect the two.
5. Ask: *"What do we now know across both of these?"*

When that feels natural, you're done with the core of Phase 1.

---

## When your memory gets big (optional — later)

At first, the assistant finds things using its catalog (the index) — fast, and needs nothing installed. That works well for a long time.

Once your memory grows large — many dozens of pages — the catalog alone can miss things. At that point you can switch on a **search layer** that searches *across all your notes* by meaning, not just keywords, and hands the best matches to the assistant. You won't operate it; it just makes "what do we know about X?" sharper as your knowledge base grows.

You do **not** need this to start. It's a later upgrade.

---

## What "good" looks like

- You've fed in a handful of documents and the assistant references them by name.
- Asking a question returns an answer that cites your own materials.
- You haven't had to manually organize anything — the assistant did the filing.
