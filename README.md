# bgg-images

Cover art for the games listed in [**bg-recommender**](https://github.com/manuelarcer/bg-recommender).
Each file is named after the game's BoardGameGeek `ObjectID`:

```
images/224517.jpg   →  Brass: Birmingham
images/167791.jpg   →  Terraforming Mars
images/342942.jpg   →  Ark Nova
…
```

The images live in their own repo so the consumer app stays small while the
files themselves are served from a free public CDN.

---

## How they got here

A scraper in a separate local project downloads cover art from BoardGameGeek:

- **Scraper:** `~/github/bgg/bgg_scraper_v2.ipynb` (a Jupyter notebook)
- **Output:** `~/github/bgg/images/<ObjectID>.jpg`

The notebook fetches each game's image URL via BGG's XML API, downloads the
JPEG, and writes it to the output folder.

## How to refresh

After running the scraper to pull new covers:

```bash
# 1. Copy the latest scraper output into this repo's images/ folder
cp -R ~/github/bgg/images/. ~/github/bgg-images/images/

# 2. Commit and push
cd ~/github/bgg-images
git add images/
git commit -m "Refresh covers"
git push
```

## How the app loads them

`bg-recommender` loads each cover via [jsDelivr](https://www.jsdelivr.com/),
which serves files from this GitHub repo over its global CDN:

```
https://cdn.jsdelivr.net/gh/manuelarcer/bgg-images@main/images/<ObjectID>.jpg
```

The URL always reflects the latest committed file on `main`. jsDelivr handles
edge caching; browsers also cache each image for a week.

## Source & licensing

Images originate from [BoardGameGeek](https://boardgamegeek.com) and are the
publishers' cover art — subject to the original copyrights. See the
business-plan docs in `bg-recommender` for notes on BGG data licensing if
this work moves to commercial use.
