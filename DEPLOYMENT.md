# DEPLOYMENT.md — Phase-Gated Deployment Protocol (binding on the Coach)

*This file is a hard constraint on how the Coach deploys the system. The Coach MUST load and obey it before doing any setup work. It exists to prevent an agent from standing up the whole system at once and overwhelming a non-technical user.*

## The one rule that overrides convenience

**Deploy exactly ONE phase per human authorization. Never begin a phase you were not explicitly told to begin.**

The system has four phases (Memory → Voice & Design → Build → Graph & Ontology). They are deployed one at a time, with the human deciding — explicitly — when to move from one to the next. This is not negotiable, even if the user seems eager or says "do everything."

## Phase gates

1. **Start:** on first run, deploy **Phase 1 only** (unless `state/PROGRESS.md` shows a later phase already authorized and in progress).
2. **Between phases (the gate):** when a phase's checkpoint is complete, **STOP**. Do three things and then WAIT:
   - Summarize, in plain language, what is now live and what it does for them.
   - Tell them the name of the next phase and, in one sentence, what it will add.
   - Ask for an **explicit instruction to advance**, e.g. *"When you're ready, tell me to start Phase 2."*
3. **What counts as authorization:** a clear, unambiguous instruction to advance a *phase* — "start Phase 2", "let's do the next phase", "proceed to voice & design". A vague "ok", "continue", "go", "sure", or "keep going" is **NOT** sufficient by itself — it may just mean the next *step within* the current phase. If ambiguous, ask: *"To confirm — do you want to move on to the next phase (Phase N), or keep going within this one?"*
4. **If asked to do it all at once** ("set up everything", "deploy all phases", "just do the whole thing"): **decline politely and explain** — the system is deployed one phase at a time so each layer is understood and stable before the next is added, and so nothing is set up that the user does not yet want. Then begin or continue **only the current phase**.

## Within a phase

Step-by-step is still required (see `COACH.md` golden rule: explain → ask → do → verify → checkpoint). The gate in this file is specifically about **phase boundaries**, not the steps inside a phase.

## Record the gate in PROGRESS.md

When a phase completes, update `state/PROGRESS.md`:
- Mark the phase's items done and its **✅ Capability Registration** done.
- Add a status line: `STATUS: Phase N complete. AWAITING explicit human authorization to begin Phase N+1.`

On any later session, read that status first. If it says "awaiting authorization," do **not** start the next phase — remind the user where they are and wait for the explicit go.

## Why this exists (for the Coach's judgment)

A non-technical user needs to absorb, trust, and get value from each layer before taking on the next. Front-loading all four phases produces a system the user does not understand and will not use. Slow is smooth; smooth is adopted.
