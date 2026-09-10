# Repaso

A single-file web app for documenting the Spanish words you learn in class and
drilling them with spaced repetition.

## What it does

- **Add** words as `Spanish → English`, one at a time or by pasting a whole list
  (splits on a dash, tab, `=`, `:`, `|`, or comma; skips duplicates).
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

## Running it

It's one file: `repaso.html`. No build step, no dependencies to install.

- **In Claude Artifacts** (where it was created): word data is stored against
  your Claude account and syncs across devices.
- **Standalone** — open `repaso.html` in a browser, or host it anywhere static
  (GitHub Pages, Netlify, etc.). Without the Claude runtime it automatically
  falls back to `localStorage`, so your words are saved in that one browser.

### GitHub Pages

Push this repo to GitHub, then in **Settings → Pages** set the source to the
`main` branch. The app will be live at
`https://<your-username>.github.io/repaso/repaso.html`
(rename the file to `index.html` if you want it at the bare repo URL).

## Fonts

Loads Fraunces, Hanken Grotesk, and IBM Plex Mono from Google Fonts at runtime,
with system fallbacks if that request is blocked.
