# Helper — Installing Your Phase 2 Skills

*Part of Phase 2 setup. A "skill" is a small instruction file that teaches the assistant to do something automatically, without you having to ask. This phase installs two: your house writing standards and the taste critique. Your Coach does this with you; it takes a couple of minutes.*

---

## What a skill is (plain language)

Think of a skill as a standing instruction the assistant carries with it. Instead of pasting a long prompt every time, you install the skill once, and from then on the assistant knows when to use it on its own. Each skill has a built-in description of when to trigger. That's the magic. You set it up during this phase's setup, and it just works afterward.

This mirrors how the professional version of this system works: capabilities live as installed skills, switched on during setup, that fire automatically at the right moment.

## The skills installed in Phase 2

**`house-style`** — your writing standards and register. After install, whenever you draft or edit written content, it applies your rules automatically (your locale, no em-dashes, no generic-AI vocabulary, real sourcing) and writes in your register, which it reads from your design system. You personalize it during the **Content Interview**.

**`jobs-ive-taste`** — the taste critique. After install, whenever you're creating or finalizing content that matters, it runs a two-part review ("Steve" on strategy, "Jony" on craft) and hands you a sharper version. You don't invoke it manually; it recognizes the moment.

They divide the work cleanly: `house-style` runs while you draft; `jobs-ive-taste` runs before you ship.

The skill files are in this repo: [`skills/house-style/SKILL.md`](../../skills/house-style/SKILL.md) and [`skills/jobs-ive-taste/SKILL.md`](../../skills/jobs-ive-taste/SKILL.md).

---

## How to install (depends on your runner)

You can't install a skill from inside a chat. It's done where the assistant looks for its capabilities. The two runners differ here, so follow the path that matches yours. Your Coach handles the mechanics either way.

### If you're on Claude Cowork (desktop)

1. Open **Settings → Capabilities** in the desktop app.
2. Add both skills. Point each at its folder in this repo (`skills/house-style/` and `skills/jobs-ive-taste/`), or paste their contents in as new skills.
3. Confirm both are enabled.

### If you're on Hermes (self-hosted)

1. Copy each skill folder into the runner's skills directory (the place Hermes scans for skills; your Coach knows the path for your setup).
2. Keep the folder structure intact: each skill is a folder containing a `SKILL.md`.
3. Restart or reload the runner if it needs it, so it picks up the new skills.

Both paths end at the same place: the assistant carries both skills and fires them at the right moment.

## How to confirm it's working

After install, draft something small and then say: "I think this is ready to send." If the assistant responds by critiquing it (concept first, then craft) and offering a sharper version, the `jobs-ive-taste` skill is live. To confirm `house-style`, ask for a short piece of writing and check that it comes back in your locale with no em-dashes and none of the AI-tell words. If nothing happens, your Coach checks that the skills are enabled (Cowork) or present in the skills directory (Hermes).

## When to update them

As your Voice & Style Card and design system get richer, both skills automatically get sharper. They read those from memory. You don't need to reinstall. If you ever want to change how critical the taste pass is, or tighten a rule in `house-style`, tell your Coach and they'll adjust the skill's wording.

---

## The pattern across the kit

You'll install more skills in **Phase 3** (the build-discipline skills). The idea is always the same: set a capability up once during a phase's setup, and it becomes automatic afterward, triggered by what you're doing, not by you remembering a prompt. Phase 1's memory rulebook works the same way: it sits in your folder and the assistant follows it without being asked.
