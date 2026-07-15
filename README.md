# Larder 🥕

**Cook what's on your shelves.** Enter your pantry, and Larder matches recipes you can actually make — plus an AI chef, **Chef Boye R. Dee**, who researches brand-new recipes from what you have.

It's a single static HTML file: no build step, no server, no framework install. Host it on GitHub Pages and you're done.

---

## Features

- **Pantry (Page 1)** — tap common staples, add your own, or upload a shopping list by **paste, file (txt/csv), or photo** (photos are read by AI).
- **Four tabs**, each with a **1 / 3 / 5** count toggle, a **Strict ↔ Flexible** ingredient toggle, a **Reshuffle** button, and per-recipe **PDF export**:
  - **Vegan** — 100% plant-based; no animal products, only plant substitutes.
  - **Vegetarian** — plant-based **plus cheese, yogurt and butter only** (no eggs, milk, cream or meat).
  - **Meat & Fish** — everything else, built around animal proteins.
- **Chef Boye R. Dee** — the AI researcher. Give him your API key and he develops new recipes from your pantry (respecting each tab's diet rules), writes a short punchy description + flavor profile, and **saves them to your cookbook** so they persist and appear in future searches.
- **Dietary safety filter** — every recipe, from the built-in library *and* the AI, is screened ingredient-by-ingredient. Vegan and Vegetarian rules are enforced after generation, so a non-compliant recipe is dropped, never shown.
- **Approximate calorie estimator** — each recipe shows ≈ kcal per serving, computed from parsed ingredient quantities and a food-energy table.
- **Persistence** — your pantry, saved recipes and keys are stored in your browser (via `localStorage` when hosted).

---

## Run it

### Option A — GitHub Pages (recommended)
1. Create a new repository and add `index.html` (and this README/LICENSE) to the root.
2. In the repo, go to **Settings → Pages**, set **Source: Deploy from a branch**, branch **main**, folder **/ (root)**, and Save.
3. Open the published `https://<you>.github.io/<repo>/` URL.

### Option B — Locally
Serve it over HTTP (don't open the file directly — browser API calls and storage behave badly on `file://`):
```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## The API key (required for the Chef)

Larder is **bring-your-own-key**. The pantry, library matching, calories, and PDF export all work with **no key**. Only the AI features need one:
- **Chef Boye R. Dee** (new-recipe research)
- **Photo** shopping-list reading

**Get a key** at [console.anthropic.com](https://console.anthropic.com). Paste it into the panel on Page 1 (or the "API key" ring, top-right).

Browser calls use Anthropic's [direct browser access](https://docs.claude.com/en/api/overview) — the app sends `x-api-key`, `anthropic-version: 2023-06-01`, and `anthropic-dangerous-direct-browser-access: true`.

### ⚠️ Security
A key typed into a web page is visible in that browser and billed to your account.
- **Use your own key for personal use.**
- **Never commit a key** to the repo, and **never publish a hosted copy carrying a shared key** — anyone visiting could use it.
- Keys are stored only in your browser. "Remember on this device" is **off by default**; leave it off on shared machines.

Usage is kept small: the Chef is instructed to be terse (a 4–5 sentence description, flavor profile, and a compact recipe per call).

---

## Recipe sources

Recipes are original formulations developed *in the style of* these trusted kitchens — the culinary references Larder draws on.

**Vegan & vegetarian:** Minimalist Baker · Oh She Glows · Rainbow Plant Life · The Full Helping · It Doesn't Taste Like Chicken · Bianca Zapatka · Cookie and Kate · Love and Lemons
**Universal:** Serious Eats · NYT Cooking · BBC Good Food · Bon Appétit · Food Network

---

## How it's built

- One file, `index.html`. React 18 + Babel (in-browser) + jsPDF, all via CDN. No build or install.
- Recipe engine is **hybrid**: a curated library matches first; the Chef fills gaps and adds to your saved collection.
- Accessibility: colors were tuned for WCAG AA contrast, with non-color cues (shapes/labels) so meaning doesn't depend on red/green — relevant for color-vision deficiency.

## Disclaimers

- **Calories are approximate**, from free-text parsing and a compact food table — a ballpark, not a nutrition label.
- The **dietary filter is best-effort**; always double-check ingredients for allergies or strict dietary needs.

## License

MIT — see [LICENSE](LICENSE).
