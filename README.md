# Repaso

A single-file web app for documenting the Spanish words you learn in class and
drilling them with spaced repetition.

## What it does

- **Add** words as `Spanish → English`, one at a time or by pasting a whole list
  (splits on a dash, tab, `=`, `:`, `|`, or comma).
- **Re-adding a word you already have** isn't rejected as a duplicate — it's read
  as a signal that the word keeps coming up, so it's flagged **★ important**,
  sent back to box 1, and queued for review right away. A different meaning you
  type gets merged in (`the house / home`).
- **Review** — you're shown the Spanish word and type the English meaning.
  Checking is lenient about accents, capitalization, punctuation, and a leading
  "to"/"the". A one-character typo asks you to self-judge instead of failing you.
- **All words** — searchable, sortable overview with per-word stats (box level,
  accuracy, when it's next due) and inline edit/delete.

## Spaced repetition

Each word lives in one of five boxes (a Leitner system):

| Box | Next review after a correct answer |
|-----|------------------------------------|
| 1   | ~10 minutes (same session)         |
| 2   | 1 day                              |
| 3   | 3 days                             |
| 4   | 7 days                             |
| 5   | 21 days                            |

A correct answer moves the word up one box; a wrong answer sends it back to box 1
**and** keeps it reappearing for the rest of the session until you get it right.
Words that aren't due yet stay out of the review queue.

**★ Important words** never rest for the full 21 days — their interval is capped
at 3 days, so they keep cycling through review even once you know them well. Mark
or unmark any word as important from its row in **All words → Edit**.

## Running it

It's one file: `repaso.html`. No build step, no dependencies to install.

- **In Claude Artifacts** (where it was created): word data is stored against
  your Claude account and **syncs across devices automatically** — open the same
  artifact link on your phone and laptop and you see the same list. This is the
  version to use if you study on more than one device.
- **Standalone** — open `repaso.html` in a browser, or host it anywhere static
  (GitHub Pages, Netlify, etc.). Without the Claude runtime it falls back to
  `localStorage`, which is **per-browser** — a word added on your phone will not
  appear on your laptop. Use Backup (below) to move words between them.

The footer of the app always tells you which mode you're in.

## Backup &amp; moving words between devices

**All words → Backup** has two buttons:

- **Export JSON** downloads every word (with its box, due date, stats, and
  important flag) as `repaso-words-YYYY-MM-DD.json`.
- **Import JSON** reads that file back in. New words are added keeping their
  saved progress; words you already have are left on their current schedule and
  just have any new meaning merged in.

So to consolidate a phone and a laptop that were both using the standalone
version: Export on one, Import the file on the other. To move everything into the
account-synced Artifact version: Export from standalone, open the Artifact, Import.

### GitHub Pages

Push this repo to GitHub, then in **Settings → Pages** set the source to the
`main` branch. The app will be live at
`https://<your-username>.github.io/repaso/repaso.html`
(rename the file to `index.html` if you want it at the bare repo URL).

## Fonts

Loads Fraunces, Hanken Grotesk, and IBM Plex Mono from Google Fonts at runtime,
with system fallbacks if that request is blocked.
