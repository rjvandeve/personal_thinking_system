# Phase 2 — Make It Sound Like You

*Goal: stop producing generic AI output. Capture your voice and your visual identity once, in a form the assistant reuses, so every memo, post, deck, and document is on-brand by default.*

---

## Why this comes second

In Phase 1 you gave the assistant a memory. Now you give it taste: yours.

Most AI writing is competent and forgettable. It sounds like everyone. The difference between "an AI wrote this" and "this is unmistakably you" comes down to two things the assistant can't guess: how you sound (your voice) and how you look (your visual identity). This phase captures both, so they apply automatically from here on.

You are not going to become a designer or a copywriter. The assistant does the building. Your only job is to answer questions and hand over things you already have.

---

## What you'll be able to do

- Produce writing that sounds like you wrote it: your phrasing, your level of formality, what you'd never say.
- Generate documents, posts, and decks that look consistent and professional, drawn from a real design system.
- Have the assistant build you a complete design system in Figma from your existing materials, without you touching Figma.
- Run a taste pass on anything before it ships, so what you send out is genuinely good, not just done.

---

## The two halves of "sounding like you"

This phase has two tracks. You can run them in either order, but most people start with voice because it pays off in the very next message they write.

### The voice track (how you write)

Two layers.

First, your voice: captured through a short interview and a few writing samples, saved as a **Voice & Style Card** the assistant applies to everything.

Second, your writing standards and process: captured through the **Content Interview** and packaged as a **`house-style` skill** that enforces your rules (locale, no em-dashes, no generic-AI vocabulary, real sourcing) on every draft, automatically.

The voice track produces two installed skills:

- **`house-style`** runs while you draft. It sets the rules and register so the first draft is already disciplined and on-voice.
- **`jobs-ive-taste`** runs before you ship. It critiques the concept and the craft, then hands you a sharper version.

### The design track (how you look)

Captured through a guided interview plus your existing materials, then built into a real **design system** in Figma. This is the centerpiece of the design track.

Here's the move that makes this work for a non-technical person. You don't build a design system. You let the assistant interview you and study your materials, then build one for you.

A good design system is a structured set of pages covering:

- **The soul** — your manifesto, your taste, your creative direction (what you stand for, how things should feel).
- **The foundations** — colors, typography, spacing, the building-block decisions.
- **The components** — buttons, cards, tables, slide templates, the reusable pieces.
- **The applied output** — real examples: a letterhead, a deck template, a one-pager.

The full target structure is in [`templates/design-system-blueprint.md`](../../templates/design-system-blueprint.md). The assistant uses it as the target; the interview fills it in.

---

## What you'll set up (the Coach does this with you)

1. **Figma** — a design tool. You won't design in it; the assistant builds your design system there and you simply look at the result. A free account is fine.
2. **The Figma bridge** — the Coach connects Figma to your assistant so it can build directly into your file.
3. **Gather your "raw brand"** — before the interviews, collect things you already have: a few decks, a PDF or two, your website link, a document you're proud of. The assistant learns your identity from these.
4. **Install the Phase 2 skills** — the Coach installs `house-style` and `jobs-ive-taste`. See [`helper-installing-skills.md`](helper-installing-skills.md).

---

## Which runner you're using

This kit works with two kinds of assistant. Wherever setup differs, the helper guides say so explicitly.

- **Claude Cowork** — the desktop assistant. Skills are installed in **Settings → Capabilities**. The Figma bridge is a connector you enable in the app.
- **Hermes** — a self-hosted runner. Skills live as files in its skills directory, and it picks them up from there.

Both end up at the same place: an assistant that writes in your voice and on your brand by default. Pick whichever you have; the day-to-day asks are identical.

---

## The coached steps at a glance

Each step has its own short helper guide in this folder, or an interview script in [`interviews/`](../../interviews/).

1. **Run the Design Interview** → [`interviews/design-interview.md`](../../interviews/design-interview.md)
   The assistant interviews you, ingests your materials, and builds your Voice & Style Card plus your design system (your look).

2. **Run the Content Interview** → [`interviews/content-interview.md`](../../interviews/content-interview.md)
   The assistant captures your writing standards and register, then personalizes your `house-style` skill (your writing). Backed by the Content Production Playbook.

3. **Produce on-brand content** → [`helper-content-production-playbook.md`](helper-content-production-playbook.md)
   Ask for a memo, post, or deck; it comes out in your voice, your standards, and your look automatically. For serious long-form, follow the full Playbook process rather than asking for a one-shot draft.

4. **Run the taste pass before you ship** → [`helper-jobs-ive-taste-pass.md`](helper-jobs-ive-taste-pass.md)
   Two critiques, one strategic and one craft, that turn "fine" into "excellent."

---

## Your first session (do this with your Coach)

1. Confirm Figma is connected.
2. Gather 3 to 5 pieces of your existing material (decks, PDFs, website).
3. Install the `house-style` and `jobs-ive-taste` skills (a few minutes; see the install helper).
4. Run the **Design Interview** (20 to 40 focused minutes; it's worth it).
5. Look at the design system the assistant builds; react and refine.
6. Run the **Content Interview** to set your writing standards and personalize `house-style`.
7. Ask for one real piece of content and watch your voice, standards, and look show up automatically.
8. Confirm the taste skill kicks in by saying "I think this is ready to send."

---

## What "good" looks like

- A Voice & Style Card lives in your memory and the assistant references it unprompted.
- You have a design system file in Figma you didn't have to design.
- Content comes out sounding like you, and you can make it excellent with one taste-pass prompt.

When you're comfortable here, your Coach moves you to **Phase 3 — Build Small Tools Safely**.
