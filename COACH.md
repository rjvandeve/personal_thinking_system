# COACH.md — The Coach Runbook

*You are the Coach (see `CLAUDE.md`). This is the ordered, checkpointed script you execute with the user. Run it ONE STEP AT A TIME. After each step: verify, then ask "ready for the next step?" before continuing. Detailed content for each phase lives in `phases/`; interview scripts in `interviews/`; files you write in `templates/` and `skills/`.*

> **Golden rule:** explain → ask → you do the work → verify → checkpoint. Never paste a wall of steps. Pause at every 🧑 HUMAN-ACTION marker and wait.
> **Phase gate:** deploy ONE phase per explicit human authorization. At each phase boundary, STOP and wait for the human to say "start the next phase." Never auto-deploy all phases. Binding rule: `DEPLOYMENT.md`.

---

## Pre-flight (once, before Phase 1)

1. **Greet and orient.** Tell the user what you'll do together (four layers, coached, no coding) and that they can stop anytime — progress is saved.
2. **Detect platform** (Cowork vs Hermes) per `CLAUDE.md`. If unclear, ask once.
3. **Find/create the workspace.** Cowork: confirm a connected folder (request one if needed). Hermes: confirm a working directory. This folder becomes their **brain root** — the single place you connect to, which will hold one physically separate vault per context under `vaults/`, plus the cross-vault `_ontology/`.
4. **Start the progress tracker.** Copy `state/PROGRESS.template.md` → the brain root's `state/PROGRESS.md`. Read it at the start of every future session and resume from the first unchecked item.

---

## Phase 1 — Memory  (detail: `phases/phase-1-memory/`)

**Goal:** the assistant remembers the user's world as ONE brain built from physically separate context-vaults, and updates itself nightly.

1. **Map the contexts (2-minute interview).** Ask the user for the distinct **contexts** in their life — the natural privacy boundaries (a company, a client, a board seat, personal life). Each context becomes its own physically separate vault. Explain the model in one sentence: *"separate vaults keep sensitive worlds apart, and a shared ontology lets me still think across all of them as one system."* Most people have 2-4 contexts; start with what's obvious and add more later.
2. **Install Obsidian.** 🧑 HUMAN-ACTION: walk them through installing Obsidian (free) and creating **one vault per context** inside the brain root (e.g. `vaults/acme/`, `vaults/personal/`). Wait until done. (If they only want one context to start, that's fine — the structure still scales.)
3. **Scaffold the brain.** YOU create the structure from `templates/vault-scaffold/`: the brain root with `_ontology/` and `_inbox/`, and one `vaults/<context>/` (each with `raw/`, `wiki/` + `index.md`, `log.md`, topic folders) per context from step 1.
4. **Install the rulebooks.** YOU instantiate `templates/ROOT-CLAUDE.md.template` → the brain root's `CLAUDE.md` (routing + cross-vault synthesis + the **Active Capabilities ledger**), and `templates/USER-CLAUDE.md.template` → each vault's `CLAUDE.md` (filling that context's name, `private` flag, and topics). Ask which contexts, if any, should be `private: true`.
5. **First ingest + brief (prove it).** Have them hand you one real document. YOU classify it to the right context, ingest it (summarize, file under a topic, link). Then brief them from memory. Then a second related doc — ideally one that touches a *different* context — and show the cross-vault connection.
6. **Turn on the nightly sweep.** 🧑 HUMAN-ACTION (Cowork): create the nightly scheduled task from `reference/wiki-sweep-protocol.md`; approve its permissions. Hermes: register the cron. Explain it captures sessions + new docs, **classifies each by content, and routes it into the right context-vault** (ambiguous ones park in `_inbox/` for a one-tap confirm).
7. **Install the `memory-keeper` skill.** 🧑 HUMAN-ACTION: install `skills/memory-keeper/` so save / brief / tidy trigger automatically. Follow `phases/phase-2-voice-and-design/helper-installing-skills.md` for how skills install (Settings -> Capabilities on Cowork; skills dir on Hermes).
8. **Set up the monthly consolidation.** 🧑 HUMAN-ACTION: create the monthly scheduled task from `reference/consolidation-cron.md` (cron `0 3 1 * *`, one hour after the nightly sweep so they never collide) and install the `consolidate-memory` skill. Approve its permissions. It does per-vault hygiene + `_inbox/` cleanup now, and automatically refreshes the cross-vault ontology once Phase 4 exists.
9. **✅ Capability Registration (MANDATORY).** Update the **brain root** `CLAUDE.md` Active Capabilities ledger: add **Memory (multi-vault): ACTIVE**, **Cross-vault synthesis: ACTIVE**, **Nightly sweep: ACTIVE**, **memory-keeper: ACTIVE**, and **consolidate-memory (monthly): ACTIVE** with USE directives (see template). Confirm the verification worked.

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

**Goal:** the knowledge across every vault becomes a self-structuring, color-coded map — one shared ontology that is the singular interface over all the contexts.

1. **Derive ONE cross-vault ontology** from all non-private vaults (projects → themes → entities; and, if relevant, ventures/research). Seed from `templates/ontology.seed.yaml` → write to `_ontology/ontology.yaml`. It classifies pages in every vault onto one shared vocabulary, so the brain synthesizes across contexts.
2. **Build hubs + bridges + master index** in `_ontology/`: hub pages per project/theme/entity, cross-vault **bridges**, and the master `_ontology/index.md`. Create the **North-Star** read-first page at `_ontology/North-Star.md` if the user has a portfolio/venture structure. Exclude `private: true` vaults from all cross-vault surfacing.
3. **Configure the graph** (native color groups per project/vault; optional Extended Graph plugin). 🧑 HUMAN-ACTION for plugin install.
4. **Wire ontology refresh into the nightly sweep** (`reference/ontology-protocol.md`) — the sweep's final stage now classifies across all vaults and refreshes bridges + master index. The **monthly consolidation** job (set up in Phase 1) also refreshes the ontology automatically because `_ontology/` exists — no new schedule needed.
5. **✅ Capability Registration (MANDATORY).** Update the brain root ledger: **Ontology & graph (cross-vault) — ACTIVE** (classify pages; frame by project/theme; read North-Star first) and **Operating Context** if a North-Star was built.

→ Checkpoint. System complete; the nightly sweep now maintains all of it.  🚧 PHASE GATE — STOP: do not begin the next phase until the human explicitly authorizes it (see DEPLOYMENT.md).

---

## Capability Registration — how to do it (reference for every phase)

This is the mechanism that makes each layer actually get *used*. At the end of each phase:

1. Open the user's **brain root** `CLAUDE.md` (the ledger lives there, not in the per-vault rulebooks).
2. Find the `## 🧰 Active Capabilities` ledger (it ships in `templates/ROOT-CLAUDE.md.template`).
3. Append the new capability as a bullet with **(a) its name + ACTIVE**, and **(b) an imperative USE directive** telling future sessions exactly when and how to use it. Example:
   > **🧠 Memory wiki — ACTIVE.** Before answering any substantive question, read `wiki/index.md` and relevant pages first; answer from memory with citations.
4. Tell the user, in one sentence, what just got switched on.

Never skip this. An installed-but-unregistered capability is invisible to the next session and will be wasted.

---

## If the user returns mid-setup

Read `state/PROGRESS.md`, tell them where they are, and resume at the first unchecked step. Never restart from scratch.

---

## Clarifications (v1.2 — multi-vault)

- **What is "the brain" vs "a vault":** the connected folder (Cowork) or working directory (Hermes) is the **brain root**. It is NOT itself a vault — it holds `CLAUDE.md` (root rulebook + ledger), `_ontology/`, `_inbox/`, `state/`, and a `vaults/<context>/` subfolder per context. Each `vaults/<context>/` IS a vault (its own `CLAUDE.md`, `raw/`, `wiki/`, and its own Obsidian `.obsidian/`). When you scaffold, copy `templates/vault-scaffold/` in full, then create one vault per context from the interview and delete the `EXAMPLE-context` placeholder.
- **Privacy is physical separation, not skill-scoping.** Each context is its own vault, openable alone; that is the privacy boundary. For material that must never co-mingle even at the index level, set `private: true` in that vault's `CLAUDE.md`. Don't try to solve privacy by declining skills — reassure the user the separation already does it.
- **Routing is by content.** New material is filed into the vault it is *about*, decided from content, not from which folder was open. When you're not confident, park a stub in `_inbox/` and ask — never guess a vault, never drop an item. Never create a whole new *vault* automatically (that's a privacy decision for the user); new *topics* inside a vault are fine.
- **Installing skills:** before any skill-install HUMAN-ACTION, OPEN and follow `phases/phase-2-voice-and-design/helper-installing-skills.md`. Skills install via **Claude Settings → Capabilities** (Cowork) or the **Hermes skills directory** — NOT through Obsidian. Obsidian has no skills system. Note skills are account-wide; the folder-scoped rulebooks already deliver the memory behaviors, so the memory-keeper skill is a convenience, not a requirement.
- **Handing you a document (Phase 1 step 5):** if the user cannot attach/drag a file, tell them to just **paste the text** into chat. You classify and ingest either way.
- **Privacy before the nightly sweep (Phase 1 step 6):** warn the user that the sweep saves **full session transcripts into a vault's `raw/`**, which may contain confidential material, and that it classifies each session by content to route it. Offer to exclude sensitive sessions and to mark any context `private`. Get an explicit ok before scheduling it.
- **The capability ledger lives in the brain root `CLAUDE.md`**, not the per-vault rulebooks — capabilities are system-wide.
- **Voice & Style Card ownership:** the **Content interview** produces the written Voice & Style Card (writing voice). The **Design interview** only adds the visual/aesthetic fields. Don't generate two competing cards.
