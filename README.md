# Personal Thinking System

**Turn your AI from a clever stranger you re-brief every morning into a chief of staff who has been with you for years — one that remembers your world, sounds like you, builds tools for you, and gets sharper every night.**

Built for busy, senior, non-technical people. You do not write code or edit settings. You hand this to an AI assistant, it becomes your **coach**, and it does the technical work while walking you through the rest, one step at a time.

---

## Why this exists

If you are a senior leader, your edge is judgment built on an enormous amount of context: the projects, the people, the relationships, the history, and the decisions and why you made them. Off-the-shelf AI throws that context away at the end of every chat. You spend half your time re-explaining yourself, and the output never quite sounds like you.

This system fixes that. It gives your AI a private, compounding memory of *your* world, teaches it to write in *your* voice at *your* standard, lets you build small tools for *your* workflow, and turns all of it into a living map you can navigate. It runs on your own machine, in plain files you control.

## One brain, many vaults

Your life has separate worlds — a company, a client, a board seat, personal life — and some of them must not bleed into each other. So this system keeps each world in its **own physically separate vault** on your machine: separate files, separate map, openable on its own. That physical separation *is* the privacy boundary. If something must never co-mingle, its vault can be sealed off entirely.

But it still thinks as **one brain**. A shared map sits on top of the vaults, so when you ask a question the assistant draws on everything at once and surfaces the connection between two worlds you'd never have spotted side by side. You get the privacy of separate filing cabinets with the insight of a single mind. You never manage any of this — the coach sets up the vaults for you, and new information files itself into the right one automatically.

## What you get, and the "why" behind each phase

You deploy it in four phases. **You move to the next one only when you say so** (see "How deployment works"). Each phase is a complete win on its own.

### Phase 1 — Memory · *the AI finally knows your world*
Your assistant builds a private knowledge base of your projects, documents, meetings, people, and decisions — one separate vault per context — and refreshes it automatically every night, filing each new thing into the vault it belongs to. 
**What it does for you (for a busy senior leader):** brief yourself on any project, relationship, or decision in seconds; pressure-test a choice against your own prior thinking; stop re-explaining context to a tool that forgot it. 
**The why:** insight compounds only if it is retained. Generic AI starts from zero every time; this makes it start from everything you have ever told it.

### Phase 2 — Voice & Design · *everything it writes sounds like you*
A short interview captures how you write and what you stand for, and turns it into a reusable skill. From then on, memos, board updates, proposals, and emails come out in your voice, on your standards, without the generic-AI tell — and a built-in "taste pass" sharpens anything before it ships.
**What it does for you:** produce executive-grade writing at your bar, fast, that reads like *you* wrote it. 
**The why:** your name is on it. It should sound like you, every time, not like a chatbot.

### Phase 3 — Build · *turn "I wish I had a tool that…" into a real tool*
With guardrails that keep everything safe and reversible, you create small personal tools and automations for your own workflow — a task-triage checklist, a comparison helper, a project tracker — directing the work in plain language.
**What it does for you:** the software that fits your exact process, without waiting on an IT queue or learning to code. 
**The why:** the highest-leverage tools are the ones shaped to how *you* actually work. Now you can make them.

### Phase 4 — Graph & Ontology · *see how everything connects — across every world*
Your knowledge becomes a navigable, color-coded map that spans *all* your vaults at once, and it keeps its own structure current automatically. You can see how projects, people, and decisions relate — including across contexts that live in separate vaults — and surface the non-obvious connection between two things you already know.
**What it does for you:** find the non-obvious link between two things you already know, even when they sit in different worlds; navigate years of context visually. 
**The why:** the value is in the connections, and the highest-value ones cross the boundaries between your separate worlds. This makes them visible and self-maintaining.

## Who it is for

Senior professionals with deep expertise and a lot of context to manage, who want an AI that genuinely knows their world — and who would rather answer a few good questions than configure software. No technical background needed.

---

## Start here (your one step)

1. Have the assistant ready: **Claude Desktop (Cowork)** or **Hermes**.
2. Ask your coach to fetch this repository for you. (If you are comfortable with a terminal, you can clone it yourself: `git clone https://github.com/rjvandeve/personal_thinking_system.git`.)
3. Open the assistant and say:

   > **Be my coach. Read this repository and set up my Personal Thinking System, one step at a time. Start with Phase 1 — I'm not technical.**

That is it. The coach takes over, and it will not run ahead of you.

## How deployment works (you stay in control)

The coach deploys **one phase at a time**. When a phase is done, it stops, shows you what is now live, and **waits for you to explicitly say "start the next phase."** It will not auto-install everything at once, even if you ask it to. You absorb and get value from each layer before taking on the next. (The rule the coach obeys is in [`DEPLOYMENT.md`](./DEPLOYMENT.md).)

## Requirements

- **Claude Desktop (Cowork)** or **Hermes** — the assistant that coaches you.
- **Obsidian** (free) — the local notes app that is the home of your memory, from Phase 1 on. Each context gets its own Obsidian vault (that's the privacy boundary); the coach helps you install it and set them up.
- Later phases add **Figma** (design) and **GitHub** (building), introduced only when you reach them.

## Contributing & license

This is **MIT licensed** ([`LICENSE`](./LICENSE)) — free to use, adapt, and share. It improves every time someone runs it and reports what tripped them up. Even a one-line "this step confused me" helps. See [`CONTRIBUTING.md`](./CONTRIBUTING.md) (your coach can open a GitHub issue for you).

---

## What's in here

```
README.md        ← you are here (for humans)
DEPLOYMENT.md    ← the one-phase-at-a-time rule the coach must obey
COACH.md         ← the step-by-step runbook the coach follows
CLAUDE.md        ← the coach's operating rules (auto-loaded by the AI)
AGENTS.md        ← pointer for Hermes / other agents
CONTRIBUTING.md · LICENSE
phases/          ← detailed coached content per layer (1-memory … 4-graph-ontology)
interviews/      ← question banks the coach runs to personalize the system to you
templates/       ← files the coach fills in (brain-root rulebook, per-context vault rulebook, vault scaffold, voice card, ontology seed)
skills/          ← installable skills (house-style, jobs-ive-taste, memory-keeper, consolidate-memory)
reference/       ← glossary, prompt pack, sweep + ontology protocols
state/           ← your resumable progress tracker
```

---

<a name="agent-entrypoint"></a>
## ⚙️ FOR THE AI AGENT — Entrypoint (humans can skip this)

**If you are an AI agent asked to implement, set up, run, or "be the coach" for this repository, this section is your instruction.**

You are the **Coach** for a non-technical user. Stand up their Personal Thinking System interactively.

1. **Load your rules:** read [`CLAUDE.md`](./CLAUDE.md) (role, prime directives, platform handling), [`DEPLOYMENT.md`](./DEPLOYMENT.md) (the binding one-phase-at-a-time gate), and [`COACH.md`](./COACH.md) (the runbook).
2. **Obey the phase gate.** Deploy ONE phase per explicit human authorization. Never begin a phase you were not told to begin. Never auto-deploy all phases, even if asked. See `DEPLOYMENT.md`.
3. **Detect your platform** (Claude Cowork vs Hermes) per `CLAUDE.md`.
4. **Run `COACH.md` one step at a time.** Explain → ask → do the file-writing yourself → verify → checkpoint. Never dump multiple steps. Pause at every human-action step.
5. **Personalize by interview** (question banks in [`interviews/`](./interviews)). Generate the user's memory rulebook, Voice & Style Card, and `house-style` skill from *their* answers — never ship a stranger's answers as theirs.
6. **At the end of every phase, register the new capability** in the user's root memory file so it is actually used (see `COACH.md` → "Capability Registration" and [`templates/USER-CLAUDE.md.template`](./templates/USER-CLAUDE.md.template)).
7. **Track progress** in the user's `state/PROGRESS.md` (from [`state/PROGRESS.template.md`](./state/PROGRESS.template.md)) so setup is resumable, and record the phase gate status there.

Begin with **Phase 1** unless `state/PROGRESS.md` shows a later phase already authorized and in progress.
