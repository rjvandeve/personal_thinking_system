# Contributing

This system gets better every time someone runs it and shares what they learned. Contributions are welcome from everyone — including non-technical users who just have an idea or a rough edge to report. It is MIT licensed (see [`LICENSE`](./LICENSE)), so you are free to use, adapt, and share it.

## The easiest way to contribute (no coding)

Open an **Issue** on GitHub and tell us:
- A step in the coach flow that confused you or your coach.
- A better interview question, or an answer option that was missing.
- A capability, phase, or template you wish existed.
- Anything the coach got wrong, dumped too much at once, or skipped.

Your coach can even do this for you: *"Open a GitHub issue describing what tripped us up in Phase 1."*

## Contributing changes (a fix or an addition)

1. **Fork** the repository and create a branch: `git checkout -b improve-phase-1-brief`.
2. Make your change. Good first contributions:
   - Sharper or clearer wording in a `phases/` guide or `COACH.md` step.
   - New or improved questions in `interviews/`.
   - New skill templates in `skills/`, or a new template in `templates/`.
   - A platform adapter (e.g. a new runner beyond Claude Cowork / Hermes).
   - Translations of the human-facing docs.
3. Keep the spirit of the system:
   - **Non-technical first.** The coach does the technical work; the human answers questions.
   - **One step at a time; one phase at a time** (see [`DEPLOYMENT.md`](./DEPLOYMENT.md)). Do not add anything that auto-deploys multiple phases.
   - **Personalize by interview**, never ship a stranger's answers as the user's.
   - **Register capabilities** at each phase end so they actually get used.
   - Follow the writing standard the system itself teaches: plain language, no filler, no em-dashes in shipped templates/skills.
4. **Open a Pull Request** describing what you changed and why. Small, focused PRs are easiest to accept.

## What we especially want

- Real-world friction reports from first-time, non-technical setups.
- New phases or skills that extend the four-layer model without breaking the phase gate.
- Better verification steps ("prove it works") for each phase.

Thank you for making it better for the next person.
