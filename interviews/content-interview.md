# Content Interview

*A one-time interview that captures how you want your written content produced, then turns your answers into your own `house-style` writing skill. The Coach runs it once; the skill applies forever after.*

> This is the writing counterpart to the Design Interview. The Design Interview builds your visual identity (the design system). This builds your writing identity (your standards, register, and process) and personalizes the `house-style` skill so it fires every time you write. It uses the Content Production Playbook as its framework.

---

## What you'll end up with

1. A personalized **`house-style` skill** — your writing standards and register, applied automatically whenever you draft content.
2. A **Project Brief & Decision Log** template — a short, per-piece checklist that locks the key decisions before any large draft.

You answer questions. The assistant assembles both. A starter version of the skill already ships in the kit ([`skills/house-style/SKILL.md`](../skills/house-style/SKILL.md)), so the interview personalizes it with your locale, register, and additions rather than starting from a blank page.

## Before you start

Have these nearby: your design system (or at least your Voice & Style Card from the Design Interview), and one or two pieces of writing you're proud of. The interview leans on the Content Production Playbook as its framework, so a glance at that helper first is useful but not required.

---

## How the Coach runs it

The Coach turns the question bank below into a quick, mostly multiple-choice conversation, one or two questions at a time. Most of the heavy rules are already set by the Playbook (no em-dashes, the AI-tell word list, real sourcing). You're mainly confirming them and adding what's specific to you. The Coach reads your design system and Voice & Style Card first, so it confirms your register rather than reinventing it. When the interview is done, the Coach plays back a summary of Parts A through G before building anything.

If you're running this yourself rather than through the Coach, paste this to start:

> **Let's set my house writing standards and personalize my `house-style` skill.** Use the Content Production Playbook as the framework and interview me using the question bank in this file. Ask in quick multiple-choice form where you can, one or two questions at a time. Cover my locale, my register and posture, which universal rules I want enforced, any extra words I personally want banned or favored, my sourcing expectations, and my naming and confidentiality constraints. Pull my voice and register from my design system and Voice & Style Card; don't reinvent them. When we're done, summarize my standards back to me before building anything.

---

## The question bank

### Part A — Your register (pulled from your design system first)

*The assistant should read your design system and Voice & Style Card before asking these, and confirm rather than reinvent.*

- Single register, or two at once (e.g., executive and technical)?
- How formal? Where do you sit between buttoned-up and conversational?
- "We," "I," or neither in your content?
- Posture you default to: educational, contrarian, category-defining, reassuring?
- Any signature phrases or framings you want to keep using?

### Part B — Locale and language

- Locale: US English (default), UK English, or other?
- Any spellings or usages specific to your field to lock in?

### Part C — The non-negotiable rules (confirm)

*These ship on by default from the Playbook. Confirm you want each enforced; flag any you'd soften.*

- No em-dashes. (keep / soften)
- One idea per sentence; short declaratives. (keep / soften)
- No filler intensifiers (very, really, quite, truly, simply). (keep / soften)
- No tired openers or closers ("in conclusion," "when it comes to," "in today's world"). (keep / soften)
- Drop the AI-tell vocabulary (delve, leverage, robust, seamless, underscore, crucial, pivotal, harness, unlock, elevate, empower, foster, landscape, ever-evolving, game-changer, revolutionize, cutting-edge, holistic, synergy, moreover, furthermore, …). (keep / soften)
- No over-bolding; bold a label, not a sentence. (keep / soften)

### Part D — Your personal additions

- Words, phrases, or clichés you personally never want to see (beyond the standard list)?
- Words or constructions you do like and want favored?
- Anything about formatting you care about (bullets vs. prose, heading style, length defaults)?

### Part E — Sourcing and evidence

- Citation expectation: inline markers plus a References section with URLs? (Playbook default: yes.)
- Are quotes allowed, or paraphrase-and-cite only?
- Preferred or required evidence sources for your field?
- Rule on unverifiable figures: state the qualitative finding and cite it? (Default: yes.)

### Part F — Naming and confidentiality

- Internal codenames or systems that must never appear in outside-facing content?
- Competitors you may or may not name?
- Confidential topics to express only in plain, non-revealing language?

### Part G — Output and workflow defaults

- Default deliverable: non-styled draft for review, then a separate styling pass? (Playbook default: yes.)
- Where do working documents live (shared drive, Word file, your memory)?
- Default review format and one-canonical-document discipline confirmed?

---

## What the assistant produces from this

1. **Personalized `house-style/SKILL.md`** — the non-negotiables (Part C) plus your locale (B), register (A), personal additions (D), sourcing (E), and constraints (F), with a trigger for any content drafting.
2. **Project Brief & Decision Log template** — the per-piece checklist (the point, audience, posture, scope, structure, evidence, constraints, locale, output) from the Playbook. The starter is at [`templates/project-brief-and-decision-log.md`](../templates/project-brief-and-decision-log.md).

The assistant plays back a summary of A through G before generating either.

If you're running this yourself, the build prompt is:

> Now turn my answers into a personalized `house-style` skill, following the structure of the existing skill in [`skills/house-style/SKILL.md`](../skills/house-style/SKILL.md). Bake in the non-negotiable writing rules plus my specific locale, register, and personal additions. Keep the description triggering whenever I'm drafting or editing written content. Have it read my voice from the design system and Voice & Style Card. Save it back over `skills/house-style/SKILL.md`, and write me a one-paragraph plain-language summary of what it does. Also create my Project Brief & Decision Log from the Playbook's brief section.

---

## After the interview

1. **Install (or reinstall) the skill** with your Coach. Same as the taste skill: Cowork adds it in Settings → Capabilities; Hermes picks it up from its skills directory. See [`phases/phase-2-voice-and-design/helper-installing-skills.md`](../phases/phase-2-voice-and-design/helper-installing-skills.md).
2. **Confirm it works.** Ask for a short piece of writing:
   > Draft a 200-word intro on [topic] for [audience].
   If it comes back in your register, in your locale, with no em-dashes and none of the AI-tell words, the skill is live. If a banned word slips through, tell the assistant; it tightens the skill.

## A note on long-form

For anything serious and long (a white paper, a flagship post), don't just ask for a draft. Follow the full Content Production Playbook process: sharp point, research and verify, outline for sign-off, then a non-styled draft. The `house-style` skill enforces the rules at every step; the Playbook gives you the sequence. Your Coach can walk the first big piece with you.
