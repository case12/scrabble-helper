# Rack Attack

A Scrabble rack trainer: draw seven tiles and see every word hiding in them.

Single self-contained `index.html` — no build step, no dependencies, no network
calls at runtime. Open the file in a browser and it works offline.

## Run it

Open `index.html` directly, or serve the folder:

    python3 -m http.server 8000

## What it does

- Draws tiles from the real 100-tile bag; drag to rearrange the rack, or type
  your own letters (`?` for a blank).
- Lists every valid word in the rack, sorted by length, score, or A–Z, with
  filters for Collins vs. TWL-only.
- Flags bingos (all seven tiles, +50), words using every tile, and words using
  a blank.
- Marks Collins-only words that aren't valid in North America.
- Links each word out to Wiktionary, Merriam-Webster, Collins, or
  Dictionary.com so you can check it yourself.
- Keyboard: `space` for a new rack, `s` to shuffle.

Scores are base tile values only — no board premiums.

## Word lists

Both dictionaries are embedded in `index.html` as gzipped, base64-encoded
blobs, decompressed in the browser via `DecompressionStream`:

- `B64` — Collins/SOWPODS, words 2–12 letters, stored as a front-coded list.
- `TWLB64` — a bitmap marking which of those words are also in the North
  American TWL list.

Those two lines are ~470 KB of opaque data, so diffs on `index.html` will not
be readable if the word lists are ever regenerated.
