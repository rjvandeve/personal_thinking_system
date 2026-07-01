# Helper — Nightly Memory Sweep

*The habit you'll most often forget is feeding things into memory. This removes that burden: every night, the assistant automatically sweeps your recent conversations and any new documents into memory, so nothing valuable is lost just because you didn't think to save it.*

---

## Why this matters

Feeding things in by hand (the *Feeding* helper) is great for important documents you want captured deliberately. But in real life, most of your valuable thinking happens in ordinary conversations — a decision you talked through, a piece of research, a draft you produced — and you'll rarely stop to file each one.

The nightly sweep catches all of it. While you sleep, the assistant reviews the day's conversations and new files, decides what's worth remembering, and compiles it into your memory. You wake up to a memory that's already up to date.

## What it does, each night

1. Looks at your recent assistant conversations and any new documents in your connected folders.
2. **Triages** — keeps what's worth remembering (decisions, facts, people, research, things you made) and ignores the chatter.
3. Compiles the keepers into clean memory pages, filed under the right topic, following your memory rulebook.
4. Writes a short line in your memory's history log so you can see what it added.

It captures *knowledge*, not raw transcripts — your memory stays a tidy briefing, not a pile of chat logs.

The full mechanics (resumable state, provenance, triage rules) live in [`reference/wiki-sweep-protocol.md`](../../reference/wiki-sweep-protocol.md). You don't need to read it; it's there if you're curious or want to tune the behavior.

## How it's set up (once)

This runs as a standing nightly job. The setup differs slightly by runner — pick yours.

### On Claude Cowork

The sweep runs as a **scheduled task**.

1. Create a nightly scheduled task that fires once a day (e.g. around 2 AM) and tells the assistant to *"Run the nightly memory sweep per `reference/wiki-sweep-protocol.md`."*
2. The first time it runs, it may ask permission to read your sessions and write to your folder — approve once, and it's remembered.
3. From then on, it just happens. To check or change the schedule later, edit the scheduled task.

### On Hermes

The sweep runs from **cron**.

1. Add a cron entry that fires once a day (e.g. `0 2 * * *`) and launches the runner with the same instruction: *"Run the nightly memory sweep per `reference/wiki-sweep-protocol.md`."*
2. Make sure the runner has read access to your session history and read/write access to the memory workspace.
3. From then on, it just happens. To change the schedule, edit the cron line.

You don't operate it day to day. You only benefit from it.

## A one-time catch-up (optional)

The first time you turn the sweep on, you can also run a **one-time backlog sweep** that goes back through your existing conversation history and captures anything worth keeping. It's resumable, so it can run across several passes without losing its place. After that, the nightly job only handles what's new.

## Checking what it captured

Each morning (or whenever), you can glance at what it added:

> What did the memory sweep capture recently? Summarize the new pages and anything notable.

If it ever files something you'd rather it hadn't, just say so — *"remove that page"* — and adjust the sweep's instructions if it keeps happening.

## Feeding by hand still has its place

The sweep is your safety net; deliberate feeding is still worth it for anything important. When a document really matters, feed it in directly (see *Feeding the Assistant Information*) so you can confirm the key points and emphasis right away, rather than waiting for the nightly pass.

## The reassurance

This is the difference between a memory you have to *remember to maintain* and one that *maintains itself*. With the sweep on, the honest answer to "did I capture that?" is almost always yes — automatically.
