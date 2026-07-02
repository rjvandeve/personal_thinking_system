# Helper — The Jobs–Ive Taste Pass

*A two-part critique that runs on anything before it ships: a memo, a deck, a page, an email. It's the difference between "fine" and "genuinely good." This is the single highest-leverage capability in the whole kit for content quality.*

> **This is an installed skill, not just a prompt.** During Phase 2 setup, your Coach installs the `jobs-ive-taste` skill (the file lives in [`skills/jobs-ive-taste/SKILL.md`](../../skills/jobs-ive-taste/SKILL.md)). Once installed, it triggers automatically whenever you're creating or finalizing real content. You don't have to remember to ask. This document explains what it does and how to invoke it on demand. Setup instructions: see [`helper-installing-skills.md`](helper-installing-skills.md).

---

## How it triggers (after setup)

Once installed, the skill activates on its own when you're working on user-facing content: drafting or finalizing a memo, post, email, deck, one-pager, or page. It is especially likely to fire when you say things like "is this good," "before I send this," "make this better," or "this feels off." It stays out of the way for casual chat, scratch notes, and quick questions.

You can also invoke it explicitly any time with the prompt below.

---

## Why this exists

AI produces competent work easily. Competent is the trap. It's good enough to send and forgettable enough to ignore. Excellence comes from a critical pass that competent output never gets. So we borrow two of the most demanding critics imaginable and let the assistant channel both:

- **"Steve" — the strategic critic.** Asks the brutal conceptual questions. Is this even the right thing? Is it honest? What should be cut entirely? Does it say one clear thing, or five muddy ones? Steve attacks the idea.
- **"Jony" — the craft critic.** Asks the questions of refinement. Is every element earning its place? Is it restrained? Is the spacing, the wording, the structure considered, or accidental? Where's the polish missing? Jony perfects the execution.

Run Steve first (is this the right thing?), then Jony (is it made beautifully?). Fixing craft on a wrong idea is wasted effort.

---

## The taste pass prompt

Paste this with whatever you're about to ship:

> **Run a Jobs–Ive taste pass on this before I send it.**
>
> First, as **Steve**, the strategic critic. Ignore polish. Attack the concept: What is the one thing this is trying to do, and does it do it? What's confused, hedged, or dishonest? What should be cut entirely? Is there a simpler, braver version? Be blunt.
>
> Then, as **Jony**, the craft critic. Assume the concept is now right. Refine the execution: What doesn't earn its place? Where is it cluttered, generic, or accidental? What small changes would make it feel considered and restrained?
>
> Give me Steve's conceptual problems and Jony's specific fixes separately. Then show me a revised version that applies them. Hold to my Voice & Style Card and design system.

---

## The quick "volume check" (for anything visual)

Borrowed from how mature design systems judge a page. Ask:

> Where does this sit on the Quietness Spectrum: Quiet, Calm, Focused, or Loud? It should land between Calm and Focused. If it's Loud (too many things competing for attention), tell me exactly what to cut.

And the diagnosis prompts, when something feels off but you can't name why:

> This feels [cramped / empty / noisy / flat / confusing / dated / accidental] to me. Diagnose why and fix it.

| If it feels… | The usual culprit |
|---|---|
| Cramped | Too much packed in; not enough space; too many columns |
| Empty | Content too sparse; nothing anchoring the space |
| Noisy | Too many elements competing at equal weight |
| Flat | No hierarchy; everything the same size and weight |
| Confusing | No clear focal point; eye doesn't know where to go |
| Dated | Heavy borders, busy decoration, over-styling |
| Accidental | Inconsistent spacing and alignment; nothing on a grid |

---

## When to use it

- **Always** before anything external goes out (client, board, public).
- On any deck or document that represents you.
- When something feels "off" and you can't articulate why. The diagnosis prompts name it for you.

## The mindset

The taste pass works because it gives the assistant permission to be critical. Left alone, it tends toward agreeable and competent. Steve and Jony give it license to tell you the headline is weak, the third slide is unnecessary, and the whole thing would be stronger at half the length. That criticism is the gift. Don't skip it because the draft "looks fine." Fine is exactly what it's there to catch.
