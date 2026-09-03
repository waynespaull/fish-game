# Fish Game

A senior-friendly flashcard quiz for identifying Southern African fish, built to run entirely as a static site on GitHub Pages. Large touch targets, high contrast, no timers, haptic feedback on answer.

Live at: `https://<your-username>.github.io/fish-game/`

## How images work

Each card in `index.html` tries an image in this order, so the game never shows a broken-image icon:

1. **Local photo** — `images/<name>.jpg`, hosted in this repo (fastest, no external dependency).
2. **Fallback** — a Wikimedia Commons hotlink, if one is set for that card.
3. **Placeholder** — a "Photo coming soon" card if neither is available.

The 6 fish currently in the game (Tigerfish, Galjoen, Snoek, Sharptooth Catfish, Red Roman, Spotted Grunter) use Wikimedia Commons photos as their fallback. **Uploading a local file to `images/` with the matching filename automatically takes over — no code changes needed.**

### Photo credit / licensing

Wikimedia Commons photos are typically CC BY or CC BY-SA, which require attribution. Each active card links its "Photo credit" line to the photo's Commons file page, where the photographer and exact license are listed — don't drop that link if you replace an image with your own Commons find.

If you upload your **own** photos (not from Commons), you can just delete that card's `credit` line in `index.html` — no attribution needed for your own pictures.

## Adding more fish

The game currently ships 6 species with working photos. `index.html` has a commented-out `pendingSpecies` list with **14 more species** ready to go — freshwater and coastal/ocean species from the same region, chosen to make plausible multiple-choice distractors alongside the existing 6.

To activate one:

1. Find/take a photo of the species and save it with the exact filename below into `images/`.
2. Upload it: repo home page → **Add file → Upload files** → select the photo(s) → **Commit changes**.
3. In `index.html`, cut that species' line out of the commented `pendingSpecies` list near the top of the `<script>` block and paste it into the `deck` array above it (matching the existing object shape — add a `fallback`/`credit` field too if you're using a Commons photo).

| Species | Habitat | Filename |
|---|---|---|
| Cape Yellowtail | Ocean Pelagic | `images/yellowtail.jpg` |
| Kob (Kabeljou) | Estuary & Ocean | `images/kob.jpg` |
| White Steenbras | Ocean Coastal | `images/steenbras.jpg` |
| Garrick (Leervis) | Estuary & Ocean | `images/garrick.jpg` |
| Blacktail | Ocean Coastal | `images/blacktail.jpg` |
| Geelbek (Cape Salmon) | Ocean Coastal | `images/geelbek.jpg` |
| Largemouth Yellowfish | Inland Freshwater | `images/yellowfish.jpg` |
| Mozambique Tilapia | Inland Freshwater | `images/tilapia.jpg` |
| Vundu Catfish | Inland Freshwater | `images/vundu.jpg` |
| Kingklip | Ocean Deep-water | `images/kingklip.jpg` |
| Cape Hake | Ocean Deep-water | `images/hake.jpg` |
| Shad (Elf) | Ocean Coastal | `images/shad.jpg` |
| Cape Stumpnose | Estuary & Ocean | `images/stumpnose.jpg` |
| Longfin Eel | Inland Freshwater / Estuary | `images/eel.jpg` |

Quiz answer choices are generated automatically (the correct name plus 3 random others from the deck, reshuffled every time), so adding a species is just the one array entry above — no options to write by hand.

> **Why aren't these 14 photos already in the repo?** They were meant to be downloaded and uploaded automatically, but the environment this was built in only allows network access to GitHub itself (no access to Wikimedia, stock photo sites, etc.), so the photos couldn't be fetched. The checklist above is everything needed to finish the job in a couple of minutes from a phone.

## Installing on a phone

1. Open the live link in Chrome for Android.
2. Tap the **⋮** menu → **Add to Home screen** (or **Install app**).
3. It installs with its own icon (`icons/icon-192.png` / `icons/icon-512.png`) and opens full-screen, no address bar, via `manifest.json`.

## Deployment

Pushing to `main` triggers `.github/workflows/static.yml`, which deploys the whole repo to GitHub Pages via GitHub Actions — no build step needed.
