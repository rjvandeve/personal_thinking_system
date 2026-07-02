# Helper — Feeding the Assistant Information

*How to hand the assistant a document or some notes so it permanently absorbs them: summarized, filed, and connected to what it already knows.*

---

## The idea in one sentence

Instead of pasting a document, getting an answer, and losing it — you "feed" it once, and it becomes part of the assistant's permanent memory that every future conversation can draw on.

## What you can feed it

- A document on your computer (PDF, Word, slides, notes)
- An email or message thread (just paste it)
- Something you typed up yourself
- A link to a web page or article

## How to do it

Open your assistant and say something like this (copy, then fill in the blanks):

> **Please add this to memory.** Here is [a document / some notes / an email] about **[what it is]**. Read it, summarize the key points for me, file it under the **[work / learning / personal]** topic, and connect it to anything related you already know. Then tell me what you filed and what you linked it to.

Then attach the file or paste the text.

## What the assistant will do

1. Read it and give you a plain-language summary.
2. Ask if anything should be emphasized — **answer this**, it makes the memory better.
3. Decide (by its content) which context-vault the document belongs to, then save the original into that vault's `raw/` and create a clean "facts first" page for it in that vault's `wiki/`. If the material clearly spans two contexts, it files it in the primary one and cross-links to the other.
4. Look through what it already knows and link the new page to related ones.
5. Update its catalog (`index.md`) and history (`log.md`) so nothing is lost.
6. Report back: *"Filed under work as 'Q3 Review'; connected it to your 'Hiring Plan' page."*

## Tips for good memory

- **Feed one thing at a time.** Clearer filing, better connections.
- **Say what it is when you hand it over.** "This is the board deck for our March meeting" beats a silent attachment.
- **Answer the emphasis question.** If you tell it "the part that matters is the budget section," the memory reflects that.
- **You don't need to organize anything.** That's the assistant's job. Resist the urge to tidy manually.

## How to know it worked

Ask right afterward: *"What do you now know about [the topic]?"* If it answers from the document you just fed it — and names it — the memory is working.

---

*Both runners (Cowork and Hermes) handle feeding identically — the only difference is how your folder is connected, which you set up once. The asks above are the same either way.*
