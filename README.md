# 🐦 Birdle

A daily bird-guessing game built on the **AVONET** morphological database. Guess the
mystery species and each guess is scored against it across taxonomy, ecology and six
morphometric traits — with arrows telling you whether the mystery bird measures larger
or smaller than your guess.

**Live site:** `https://<your-username>.github.io/birdle/` *(after you enable Pages — see below)*

---

## How to play

- A new mystery bird is chosen each day (same for everyone, UTC-based).
- Type any of the **11,009** bird species as a guess (autocomplete helps).
- Each guess returns a specimen tag showing how it compares to the mystery bird:
  - **Taxonomy & ecology chips** — Order, Family, Habitat, Trophic niche, Lifestyle, Migration.
    Green = same as the mystery bird, grey = different.
  - **Morphometric traits** — Mass, Wing, Beak, Tarsus, Tail, Hand-wing index.
    Green = within 5%, amber = within 25%, grey = further off.
    `↑` means the mystery bird's value is **larger** than your guess, `↓` means **smaller**.
- You have **8 guesses**. Solve it, then share your emoji grid.
- "Play a random bird" gives unlimited practice rounds.

The daily answer is drawn from a pool of ~4,100 widespread, well-sampled species so the
target is always a bird with solid trait coverage; all 11,009 species remain valid guesses.

---

## Repository structure

```
birdle/
├── index.html     # the whole game (HTML + CSS + JS, no build step)
├── birds.js       # compact AVONET-derived dataset (window.BIRDLE_DATA)
├── .nojekyll      # tells GitHub Pages to serve files as-is
└── README.md
```

No frameworks, no build tooling — it's a static site. Open `index.html` locally to play,
or push to GitHub and turn on Pages.

---

## Deploy to GitHub Pages

1. **Create a new empty repository** on GitHub named `birdle` (public).

2. **Push these files** from inside this folder:

   ```bash
   git init
   git add .
   git commit -m "Birdle: daily AVONET bird-guessing game"
   git branch -M main
   git remote add origin https://github.com/<your-username>/birdle.git
   git push -u origin main
   ```

3. **Enable Pages:** repo → **Settings → Pages** → *Build and deployment* →
   Source = **Deploy from a branch**, Branch = **main**, folder = **/ (root)** → **Save**.

4. Wait ~1 minute, then visit `https://<your-username>.github.io/birdle/`.

That's it — same static-site workflow as a standard GitHub Pages project.

---

## Regenerating / editing the dataset

`birds.js` was generated from `AVONET1_BirdLife.csv` (the BirdLife taxonomy sheet of AVONET
Supplementary dataset 1). Each species keeps its family, order, habitat, migration status,
trophic niche and primary lifestyle, plus six rounded morphometric means. Categorical values
are factored into lookup tables to keep the file small (~770 KB).

To rebuild it — e.g. to switch to the eBird or BirdTree taxonomy, change the answer-pool
rule, or add traits — re-run the generation script against the AVONET CSV and overwrite
`birds.js`. The answer pool is currently "range size ≥ 55th percentile AND ≥ 5 individuals
measured"; adjust that threshold to make the daily bird more or less obscure.

---

## Data & attribution

Bird trait data from the AVONET database, used under its CC-BY license:

> Tobias, J.A., Sheard, C., Pigot, A.L., Devenish, A.J.M., Yang, J., Sayol, F., et al. (2022).
> AVONET: morphological, ecological and geographical data for all birds.
> *Ecology Letters*, 25(3), 581–597. https://doi.org/10.1111/ele.13898

Please keep this attribution on any deployed version.
