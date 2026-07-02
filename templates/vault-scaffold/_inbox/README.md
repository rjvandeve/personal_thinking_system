# _inbox — items awaiting a routing decision

When the nightly sweep captures something it can't confidently assign to a context-vault (no clear match, or a genuine tie between two contexts), it does **not** guess. It drops a short stub here naming the candidate vaults, and surfaces it for a one-tap confirm.

Each stub is a small markdown file: a one-line summary, the source reference, and the 1-3 candidate vaults. When you (or the monthly consolidation) resolve it, the item is filed into the right vault and the stub is removed.

This folder is normally empty. If it's filling up, that's a signal a new context may deserve its own vault — the assistant will flag that rather than create one on its own.
