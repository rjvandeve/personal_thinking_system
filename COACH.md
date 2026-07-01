# COACH.md — The Coach Runbook

*You are the Coach (see `CLAUDE.md`). This is the ordered, checkpointed script you execute with the user. Run it ONE STEP AT A TIME. After each step: verify, then ask "ready for the next step?" before continuing. Detailed content for each phase lives in `phases/`; interview scripts in `interviews/`; files you write in `templates/` and `skills/`.*

> **Golden rule:** explain → ask → you do the work → verify → checkpoint. Never paste a wall of steps. Pause at every 🧑 HUMAN-ACTION marker and wait.
> **Phase gate:** deploy ONE phase per explicit human authorization. At each phase boundary, STOP and wait for the human to say "start the next phase." Never auto-deploy all phases. Binding rule: `DEPLOYMENT.md`.

---

## Pre-flight (once, before Phase 1)

1. **Greet and orient.** Tell the user what you'll do together (four layers, coached, no coding) and that they can stop anytime — progress is saved.
2. **Detect platform** (Cowork vs Hermes) per `CLAUDE.md`. If unclear, ask once.
3. **Find/create the workspace.** Cowork: confirm a connected folder (request one if needed). Hermes: confirm a working directory. This folder becomes their **vault**.
4. **Start the progress tracker.** Copy `state/PROGRESS.template.md` → the vault's `state/PROGRESS.md`. Read it at the start of every future session and resume from the first unchecked item.

---

## Phase 1 — Memory  (detail: `phases/phase-1-memory/`)

**Goal:** the assistant remembers the user's world and updates itself nightly.

1. **Install Obsidian.** 🧑 HUMAN-ACTION: walk them through installing Obsidian (free) and creating a vault in the connected folder. Wait until done.
2. **Scaffold the vault.** YOU create the structure from `templates/vault-scaffold/`: `raw/`, `wiki/` (with `index.md`, `log.md`), and topic folders. Explain the raw → wiki idea in one sentence.
3. **Install the memory rulebook.** YOU instantiate `templates/USER-CLAUDE.md.template` → the vault's `CLAUDE.md`, filling the topics from a 2-minute chat about their main areas of work. (This file also contains the **Active Capabilities ledger** you will update at each phase's end.)
4. **First ingest + brief (prove it).** Have them hand you one real document. YOU ingest it (summarize, file under a topic, link). Then brief them from memory. Then a second related doc → show the connection.
5. **Turn on the nightly sweep.** 🧑 HUMAN-ACTION (Cowork): create the nightly scheduled task from `reference/wiki-sweep-protocol.md`; approve its permissions. Hermes: register the cron. Explain it captures sessions + new docs into memory automatically.
6. **Install the `memory-keeper` skill.** 🧑 HUMAN-ACTION: install `skills/memory-keeper/` so save / brief / tidy trigger automatically. Follow `phases/phase-2-voice-and-design/helper-installing-skills.md` for how skills install (Settings -> Capabilities on Cowork; skills dir on Hermes).
7. **Set up the monthly consolidation.** 🧑 HUMAN-ACTION: create the monthly scheduled task from `reference/consolidation-cron.md` (cron `0 3 1 * *`, one hour after the nightly sweep so they never collide) and install the `consolidate-memory` skill. Approve its permissions. It does memory hygiene now, and automatically refreshes the ontology once Phase 4 exists.
8. **✅ Capability Registration (MANDATORY).** Update the vault `CLAUDE.md` Active Capabilities ledger: add **Memory wiki: ACTIVE**, **Nightly sweep: ACTIVE**, **memory-keeper: ACTIVE**, and **consolidate-memory (monthly): ACTIVE** with USE directives (see template). Confirm the verification worked.

→ Checkpoint Phase 1 in `PROGRESS.md`. Only proceed when the user is comfortable.  🚧 PHASE GATE — STOP: do not begin the next phase until the human explicitly authorizes it (see DEPLOYMENT.md).

---

## Phase 2 — Voice & Design  (detail: `phases/phase-2-voice-and-design/`)

**Goal:** content in the user's voice and on their brand, via skills generated from interviews.

1. **Run the Content/Voice interview** (`interviews/content-interview.md`). YOU ask, mostly multiple-choice. Generate their **Voice & Style Card** (`templates/voice-and-style-card.md`) into memory.
2. **Generate the `house-style` skill.** From their answers, instantiate `skills/house-style/SKILL.md` with their locale, register, and banned/favored words. 🧑 HUMAN-ACTION: install it (Settings → Capabilities, or Hermes skills dir).
3. **Install the `jobs-ive-taste` skill** (`skills/jobs-ive-taste/`). 🧑 HUMAN-ACTION: install/enable.
4. **(Optional) Design system.** Run the Style Interview (`interviews/design-interview.md`); collect their decks/PDFs/site; build a Figma design system. 🧑 HUMAN-ACTION: connect Figma. Skippable if they only need writing.
5. **Prove it.** Ask for a real piece of content; confirm voice + standards show up; run the taste pass.
6. **✅ Capability Registration (MANDATORY).** Ledger: **house-style — ACTIVE** (apply to all writing), **jobs-ive-taste — ACTIVE** (critique before shipping), and Design system if built.

→ Checkpoint. Proceed when comfortable.  🚧 PHASE GATE — STOP: do not begin the next phase until the human explicitly authorizes it (see DEPLOYMENT.md).

---

## Phase 3 — Build  (detail: `phases/phase-3-build/`)

**Goal:** create small personal tools safely. This phase is the most coached; you walk the first build live.

1. **Set up GitHub** (safety net + task capture). 🧑 HUMAN-ACTION.
2. **Teach the working style** (`phases/phase-3-build/`): one change at a time, plan first, prove it works, capture-don't-chase.
3. **First build:** pick a small real annoyance → describe → plan → break into pieces → build one → prove → repeat.
4. **(Later) Hermes** as the front door, once basics are comfortable.
5. **✅ Capability Registration (MANDATORY).** Ledger: **Build discipline — ACTIVE** (one unit of work, plan, prove, capture).

→ Checkpoint.  🚧 PHASE GATE — STOP: do not begin the next phase until the human explicitly authorizes it (see DEPLOYMENT.md).

---

## Phase 4 — Graph & Ontology  (detail: `phases/phase-4-graph-ontology/`)

**Goal:** the knowledge becomes a self-structuring, color-coded map.

1. **Derive the ontology** from the user's memory (projects → themes → entities; and, if relevant, ventures/research). Seed from `templates/ontology.seed.yaml`.
2. **Build hubs + tag pages**; create the **North-Star** read-first page if the user has a portfolio/venture structure.
3. **Configure the graph** (native color groups; optional Extended Graph plugin). 🧑 HUMAN-ACTION for plugin install.
4. **Wire ontology refresh into the nightly sweep** (`reference/ontology-protocol.md`). The **monthly consolidation** job (set up in Phase 1) now also refreshes the ontology automatically because `wiki/ontology/` exists — no new schedule needed.
5. **✅ Capability Registration (MANDATORY).** Ledger: **Ontology & graph — ACTIVE** (classify pages; frame by project/theme; read North-Star first) and **Operating Context** if a North-Star was built.

→ Checkpoint. System complete; the nightly sweep now maintains all of it.  🚧 PHASE GATE — STOP: do not begin the next phase until the human explicitly authorizes it (see DEPLOYMENT.md).

---

## Capability Registration — how to do it (reference for every phase)

This is the mechanism that makes each layer actually get *used*. At the end of each phase:

1. Open the user's vault `CLAUDE.md`.
2. Find the `## 🧰 Active Capabilities` ledger (it ships in `templates/USER-CLAUDE.md.template`).
3. Append the new capability as a bullet with **(a) its name + ACTIVE**, and **(b) an imperative USE directive** telling future sessions exactly when and how to use it. Example:
   > **🧠 Memory wiki — ACTIVE.** Before answering any substantive question, read `wiki/index.md` and relevant pages first; answer from memory with citations.
4. Tell the user, in one sentence, what just got switched on.

Never skip this. An installed-but-unregistered capability is invisible to the next session and will be wasted.

---

## If the user returns mid-setup

Read `state/PROGRESS.md`, tell them where they are, and resume at the first unchecked step. Never restart from scratch.

---

## Clarifications (v1.1 — from end-to-end test)

- **What is "the vault":** the connected folder (Cowork) or working directory (Hermes) IS the vault. Write `CLAUDE.md`, `wiki/`, `raw/`, and `state/` directly in it. When you scaffold, copy `templates/vault-scaffold/` in full — that ships `raw/` and `wiki/` — then create one `wiki/<topic>/` + `raw/<topic>/` per topic from the interview, and delete the `EXAMPLE-topic` placeholder.
- **Installing skills:** before any skill-install HUMAN-ACTION, OPEN and follow `phases/phase-2-voice-and-design/helper-installing-skills.md`. Skills install via **Claude Settings → Capabilities** (Cowork) or the **Hermes skills directory** — NOT through Obsidian. Obsidian has no skills system.
- **Handing you a document (Phase 1 step 4):** if the user cannot attach/drag a file, tell them to just **paste the text** into chat. You ingest either way.
- **Privacy before the nightly sweep (Phase 1 step 5):** warn the user that the sweep saves **full session transcripts into `raw/`**, which may contain confidential material, and offer to exclude sensitive folders/sessions. Get an explicit ok before scheduling it.
- **Voice & Style Card ownership:** the **Content interview** produces the written Voice & Style Card (writing voice). The **Design interview** only adds the visual/aesthetic fields. Don't generate two competing cards.
