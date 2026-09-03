# Southern African Fish Quiz

A senior-friendly flashcard quiz for identifying Southern African fish species. Built as a
single-page static site (`index.html`) — large touch targets, high-contrast colors, and
big readable text. Hosted via GitHub Pages.

## How it works

- Each round shows a fish photo and four name options (the correct name plus three random
  distractors, reshuffled every time the page loads).
- Tapping an answer shows immediate correct/wrong feedback (color + light vibration on
  supported devices) before moving to the next fish.
- Works as an installable PWA ("Add to Home Screen") via `manifest.json`.

## Image loading

Each card loads its photo through a fallback chain so a broken link never shows a broken-image
icon:

1. **Local photo** in `images/` (fast, works offline once cached).
2. **Wikimedia Commons hotlink** if the local file is missing or fails to load.
3. **"📷 Photo coming soon" placeholder** if both of the above fail.

All photos preload in the background (`Image()` objects, references retained so the browser
doesn't garbage-collect them early) while the first card is showing.

## Fish deck (19 species)

| Fish | Habitat | Photo credit | License |
|---|---|---|---|
| Tigerfish | Inland Freshwater | Andrew Deacon | CC0 |
| Galjoen | Ocean Coastal | Brian Gratwicke | CC BY 2.0 |
| Snoek | Ocean Pelagic | Brian Gratwicke | CC BY 2.0 |
| Sharptooth Catfish | Inland Freshwater | Zahara5555 | CC BY-SA 4.0 |
| Red Roman | Ocean Reef | Peter Southwood | CC BY-SA 3.0 |
| Spotted Grunter | Estuary & Ocean | Craig Thom | CC BY-SA 3.0 |
| Largemouth Yellowfish | Inland Freshwater | Mahomed Desai | CC BY 4.0 |
| Mozambique Tilapia | Inland Freshwater | John Robert McPherson | CC BY-SA 4.0 |
| Largemouth Bass | Inland Freshwater | sisor | CC BY 4.0 |
| Vundu | Inland Freshwater | Cuvier & Valenciennes | Public domain |
| Yellowtail | Ocean Pelagic | A. R. Mc Culloch | Public domain |
| Kingklip | Ocean Deep | JMK | CC BY-SA 4.0 |
| Cape Salmon | Ocean Pelagic | Andrew Smith | Public domain |
| Blacktail | Ocean Reef | Bernard DUPONT | CC BY-SA 2.0 |
| Elf (Shad) | Ocean Coastal | JaredMcKenzie | CC0 |
| White Steenbras | Estuary & Ocean | F. H. Van der Bank, Univ. of Johannesburg | Free use |
| Garrick | Ocean Coastal | F. H. Van der Bank, Univ. of Johannesburg | Free use |
| Silver Kob | Estuary & Ocean | Show_ryu | CC BY-SA 3.0 |
| Cape Stumpnose | Estuary | Andy Mabbett | CC BY-SA 4.0 |

All photos are from [Wikimedia Commons](https://commons.wikimedia.org). Each card in the app
links to its source file's Commons page for full license terms and attribution, per each
license's requirements.

## Adding more fish

To add a species, append an entry to the `deck` array in `index.html`:

```js
{
  name: "Species Name",
  habitat: "🌊 Ocean Coastal",   // or 🏞️ Inland Freshwater / 🌊 Estuary, etc.
  image: "images/species.jpg",
  fallback: "https://commons.wikimedia.org/wiki/Special:FilePath/Original_File_Name.jpg?width=600",
  credit: { author: "Photographer", license: "CC BY-SA 4.0", url: "https://commons.wikimedia.org/wiki/File:Original_File_Name.jpg" }
}
```

Download the matching photo into `images/species.jpg` (via the same `Special:FilePath` URL) so
it loads locally first. Multiple-choice distractors are generated automatically from the rest
of the deck, so no per-card option list is needed.
