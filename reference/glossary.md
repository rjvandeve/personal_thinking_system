# Glossary

*Every term in this system, in plain language. No prior knowledge assumed. Skim it once; come back whenever a word is unfamiliar.*

---

## The tools

**Claude Desktop (Cowork)** — the AI assistant on your computer. Where you have conversations and where everything here happens. **Hermes** is the companion runner that does the same work from the command line; the two are interchangeable runners for this system.

**Cowork (file-working mode)** — the mode in Claude Desktop that can work with files in a folder on your computer (read them, write them, organize them). It's what lets the assistant build and maintain your memory. Hermes does this too.

**Obsidian** — a free notes application. Underneath, it's just a folder of plain text files, with a nice reader on top. Here it holds the assistant's long-term memory. You'll rarely open it yourself.

**Figma** — an app for designing visuals. You won't design in it yourself; here the assistant builds your design system there and you look at the result.

**Design bridge** — the connection that lets the assistant build directly into your Figma file.

**GitHub** — a safety net and history book for things you build. Every change is saved as a numbered version you can return to, and it holds your list of ideas and tasks. (Building phase.)

**Hermes (front door)** — your simple entry point for building: instead of using technical tools, you just message your assistant and it does the building behind the scenes. (Building phase, introduced later.)

## Memory

**Memory / knowledge base** — the organized store of what the assistant knows about your world. It grows and improves as you feed it.

**Vault / folder** — the folder that holds your memory.

**Raw** — the original source material you feed in (a PDF, an email, notes). Never changed; kept as the record of truth.

**Wiki** — the assistant's own clean, organized pages, one per topic. This is what gets smarter over time.

**Index** — the catalog: a table of contents of every wiki page.

**Log** — the running history of every change the assistant made to your memory.

**Facts / Takeaways (two-pass writing)** — every memory page is written facts-first (just what's true, with sources), and gains a "Takeaways" section (judgment, connections, open questions) once there's enough to say.

**Rulebook** — the vault's `CLAUDE.md` memory rulebook: a single file in your folder that tells the assistant how to keep your memory organized. It applies automatically; you don't read it for fun.

**LLM Wiki pattern** — the well-known approach this memory system is based on. The core idea: the assistant acts as a *compiler* that turns your raw documents into a clean, interlinked wiki — so it never re-learns your world from scratch.

**Semantic search layer** — an optional search tool your coach can install later (for example, **qmd**). It searches across all your notes by *meaning*, not just keywords, so the memory stays sharp as it grows large. Not needed to start.

**Nightly memory sweep** — a scheduled job that runs each night, reviews your recent conversations and new documents, and automatically files what's worth remembering into memory. It means you don't have to remember to feed everything in by hand.

**Scheduled task** — a standing job that runs automatically on a schedule (like the nightly sweep), set up once. Your coach configures it.

## Structure & concepts

**Ontology** — the shared vocabulary your memory is organized around: the agreed list of the kinds of things in your world and how they relate. It's what keeps every page filed consistently instead of each note inventing its own categories.

**Projects, themes, entities** — the main building blocks your memory sorts things into. *Projects* are concrete pieces of work with a goal. *Themes* are recurring topics or areas you keep returning to. *Entities* are the people, organizations, and things your notes refer to. Most memory pages are one of these three.

**Hub page (map of content)** — a single page that gathers links to everything about one project, theme, or area, so you have one place to start from instead of hunting. Think of it as the front page for a topic.

**North-Star** — the one overriding aim that everything else is meant to serve. When priorities conflict, the North-Star is the tiebreaker. Keeping it written down keeps day-to-day choices pointed the same direction.

**Portfolio / research layers** — an optional higher-level structure for people who run several initiatives at once. It lets your memory hold a portfolio of distinct ventures or research strands side by side, each with its own projects and themes, without them bleeding into each other. Skip it if you're focused on a single thing.

**Capability ledger** — a running list of what your system can now do, kept up to date as new skills and tools get added. It's how you (and the assistant) remember what's already been set up, so you don't rebuild things or forget a capability exists.

**The Coach** — the assistant acting as your guide through setup: it explains each step, asks what it needs, does the building, and checks in before moving on. You don't need to know the technical steps — the Coach drives, you steer.

**Self-implementing repo** — a project set up so that you describe what you want in plain language and the assistant makes the change itself, end to end. The structure, rules, and instructions live alongside the project, so the assistant can read them and act without you wiring anything by hand.

## Voice & design

**Design system** — a structured set of decisions about how you look and sound (your manifesto, taste rules, colors, fonts, templates), so everything you produce is consistent and on-brand.

**Brand Manifesto** — a short declaration of what you stand for and how you want to come across. The "soul" of your design system. Written in your voice.

**Taste & Composition** — the operating rules of good taste for your brand: the adjectives that describe your look, what to do and never do, and how busy or calm things should feel.

**Style Interview** — the guided conversation where the assistant interviews you and studies your existing materials to build your design system. You answer; it builds.

**Voice & Style Card** — a one-page summary of how you write and look, stored in memory, applied to everything automatically.

**Tokens** — the named master list of every design value (each color, font, size), so everything stays consistent.

**Quietness Spectrum** — a way to judge whether something is at the right "volume": Quiet · Calm · Focused · Loud. Aim for Calm-to-Focused; never Loud.

**Jobs–Ive taste pass** — a two-part critique that raises content quality: one pass attacks the concept (is this the right thing? what to cut?), the other refines the craft (is it made well?). Here it's an installed skill (`jobs-ive-taste`) that runs automatically.

**Content Production Playbook** — the process and standards for producing serious written content (white papers, long-form posts). The process and rules are universal; the voice comes from your design system.

**Content Interview** — the one-time conversation (built on the Playbook) that captures your writing standards and register and turns them into your house-style skill.

**House style** — your own fixed writing standards: locale, punctuation rules, banned words, sourcing expectations. Here it's the house-style skill that enforces them on every draft.

**AI-tell vocabulary** — words and constructions that make writing sound like generic AI (delve, leverage, robust, seamless, landscape, moreover, and many more). The house-style skill removes them.

**Decision log / project brief** — a short, per-piece record of the key choices for a content project (the point, audience, posture, scope, sources, constraints), kept in your memory so drafts stay consistent.

**Non-styled draft** — a plain, unformatted draft written for review. Visual styling is applied later, as a separate pass.

## How capabilities work

**Skill** — a small instruction file you install once (during a phase's setup) that the assistant then uses *automatically* at the right moment. You don't memorize prompts; the skill knows when to fire.

**Trigger** — the built-in description in a skill that tells the assistant *when* to use it. For the taste skill, the trigger is "you're creating or finalizing content."

**Capabilities settings** — where, in Claude Desktop (Cowork) or Hermes, skills get added and enabled. Your coach handles this.

## Building

**Version** — a saved snapshot of your project at a point in time. You can always return to an earlier one, which is why building this way is safe.

**Task / issue** — a captured idea or to-do, written down so it isn't forgotten or acted on impulsively.

**Plan** — the decision about what to build and in what order, made *before* any building starts.

**Prove it works** — the rule that nothing counts as done until it's been demonstrated to work, not just assumed.

**Capture, don't chase** — the habit of writing new ideas down as tasks instead of dropping your current work to do them.

**One change at a time** — building one small, finishable, provable piece before starting the next. The main thing that keeps building safe.
