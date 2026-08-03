# SC Console

**An offline companion for Star Citizen Alpha 4.9 — mining, ships, crafting and getting around, in a single HTML file.**

![Star Citizen](https://img.shields.io/badge/Star_Citizen-Alpha_4.9-ff8a3d?style=flat-square)
![Game build](https://img.shields.io/badge/build-4.9.0--LIVE.12232306-6fd3e8?style=flat-square)
![Single file](https://img.shields.io/badge/single_file-1.5_MB-58e0b8?style=flat-square)
![Offline](https://img.shields.io/badge/offline-no_server_needed-58e0b8?style=flat-square)
![Languages](https://img.shields.io/badge/languages-10-b98cff?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)

Open `sc-console.html` in any browser. That's the whole installation. No server, no build step, no network calls — the data is baked in, so it works on a second monitor while the game has your GPU, and it works when you're on a plane.

---

## What's actually in it

| | |
|---|---|
| **307** ships and vehicles | every variant, with real hardpoints |
| **7,602** hardpoints | including nested slots (mounts → guns, lasers → modules) |
| **956** components | weapons, shields, power plants, coolers, quantum drives, mining gear |
| **1,588** blueprints | crafting recipes across 25 item types |
| **39** materials | signatures, instability, resistance, prices |
| **33** locations | across Stanton (17), Pyro (12) and Nyx (4) |
| **13** mining lasers · **27** modules · **6** gadgets | with their real modifier values |
| **5** cities · **31** shops | transit routes and what's sold where |
| **10** languages | 689 dictionary entries, 6,201 translations |

---

## The six sections

### ⛏ Mining
Seven tabs covering the whole loop:

- **Scanner** — type the RS value your ship reads and get the mineral plus how many nodes are in the cluster. Handles ambiguous readings and mixed clusters.
- **Signatures** — a multiplier grid of every mineral × node count, searchable live. Built to sit on a second screen. Flags the **12 readings where two materials produce the identical number** and tells you how to tell them apart.
- **Where** — pick one or several materials and see every location that has them, with each material's abundance shown per result. Sorts by coverage, total abundance, or expected rock value.
- **Profitability** — locations ranked by what the *average rock you scan there* is actually worth, and a per-location cheat sheet of which signatures are worth stopping for.
- **Rocks** — full composition of all 26 rock types including **inert material**, the filler the game never shows you. Plus a live evaluator: move the sliders to the percentages on your HUD and see how much of your hold is gravel.
- **Loadout** — pick a target material and get the laser + module combination that suits its instability and resistance, with alternatives ranked and trade-offs visible.
- **Refinery** — the nine refining methods compared, plus all 19 refinery locations.

### 🚀 Ships
Full configurator for all 307 hulls. Compatibility comes straight from the game files: if a component doesn't appear in a slot, it doesn't fit there. Nested slots work properly — gimbal mounts open to weapons, mining lasers open to their module bays, quantum drives open to jump drives.

Each slot opens a **sortable comparison table** with the stats that matter for that component type, showing the delta against what you have equipped. Shields display their per-damage-type resistances, weapons show sustained DPS alongside burst.

Every ship gets a scale schematic with hardpoint positions, a hangar class badge (S/M/L/XL), and a **shareable build code** you can paste to someone else.

### 🔨 Crafting
1,588 recipes searchable in both directions: from an item to what it needs, or from a material to everything it goes into. Every ingredient drills down to price per SCU and where it's mined. Material cost is computed from refined averages; market prices are included where available, with automatic flags on the listings that are obviously junk.

### ⚖ Compare
Up to four ships side by side across 26 rows, with the best value in each row highlighted and rows where everything is equal left neutral.

### 🏙 Cities
The part nobody documents well: **how to get from your bed to your ship.** Lorville, Area18, New Babbage, Orison and the space stations, each with its transit network drawn out and a step-by-step route colour-coded by transport type.

The details that actually trip people up are in there — at the bottom of the Metro Center stairs in Lorville you turn *right*, at New Babbage you turn *left*, and you get off at the **first** stop. Plus what to do when the elevator won't respond or the train never comes.

### 🔍 Global search
`Ctrl+K` from anywhere. Searches ships, components, materials, recipes, locations and cities at once, and jumps you to the right panel with the right thing already selected.

---

## Where the data comes from, and how much to trust it

This matters more than feature lists, so it's stated in the app too.

| Layer | Source | Confidence |
|---|---|---|
| Ships, hardpoints, compatibility, components, crafting recipes | Game files, build `4.9.0-LIVE.12232306` (StarCitizenWiki/scunpacked-data dump, 16 Jul 2026) | **Exact.** No estimation. |
| RS signatures | `Game2.dcb` datamine | **Exact.** |
| Location abundances | SCMINER, patch 4.9 | Community-sourced. May drift from live. |
| Refining methods, hangar specs | Star Citizen Wiki | Community-sourced, verified. |
| Material prices | UEX via SC DataHub, read 3 Aug 2026 | Refined sell averages. Stable enough for comparison. |
| Marketplace prices | UEX Marketplace snapshot, 1 Aug 2026 | **A photograph, not a feed.** Player classifieds with bait listings. |
| Loadout advisor scoring | Mine | A formula I wrote. Documented in the app. |
| Ship silhouettes | Mine | 18 hand-drawn archetypes by role, scaled to real dimensions. **Not** traced hull profiles. |

### Known limits, stated plainly

- **No live prices.** Shop inventories aren't in the game files, and UEX's item API needs a personal token. If you have one, the price layer drops in on top of what's already here.
- **No hull geometry.** The game files don't contain it, and tracing official renders would be reproducing CIG's artwork. The silhouettes are archetypes — you'll tell a fighter from a hauler, not a Cutlass from a Freelancer.
- **Two ships have no dimensions** (Javelin, Argo MOTH). Sources disagree, so rather than invent them the schematic is disabled for those two and everything else still works.
- **Ice pricing is uncertain.** The source only lists "Pressurized Ice" and the mapping isn't confirmed, so the conservative figure was kept.
- **Long-form documentation stays in Italian** when you switch language. The interface, labels, results, city routes and shop entries are all translated; the methodology essays inside the collapsible blocks are not, and the app says so.

---

## Building from source

Using the tool needs nothing. Rebuilding it needs Python 3.10+ and Node (for the test suites).

```
scdata/
├── extract2.py        # game dump  → dataset.json (ships, components, hardpoints)
├── shapes.py          # 18 role silhouettes + role→family mapping
├── city.py            # transit routes and shops
├── build_tool4.py     # ship configurator
├── build_mining.py    # mining terminal
├── build_craft.py     # crafting terminal
└── build_app.py       # merges everything into sc-console.html
```

```bash
python3 extract2.py       # needs ships.json + ship-items.json from the dump
python3 build_tool4.py
python3 build_mining.py
python3 build_craft.py
python3 build_app.py      # → sc-console.html
```

The merge step namespaces each tool into an isolated module — they were written independently and share global names — then injects the shared datasets once instead of three times.

### Tests

Thirteen suites run against a real DOM (jsdom) plus a browser pass (Playwright) for layout and interaction. They've caught real bugs: labels that lost their input association, a function scoped out of reach of its own click handlers, a greedy regex eating half a file, IDs generated inside JS strings that never got prefixed.

```bash
node audit.js          # cross-dataset integrity
node final_test.js     # navigation and section bridges
node i18n_test.js      # translation across all 10 languages
node check.py          # browser layout and interaction
```

---

## Translation

Ten languages: Italian (source), English, German, French, Spanish, Portuguese, Russian, Chinese, Japanese, Polish.

Translation happens **after** rendering, in the DOM, via a MutationObserver per section. The modules keep emitting Italian and the text gets swapped — which meant no rewrite of hundreds of concatenated strings across three independently-built tools.

Three things make it work beyond a flat dictionary:

- **Segment translation.** Labels like `Ship weapons · G1 · 3 ingredients · 28 min` are assembled piece by piece; the combinations run into the thousands. Each segment is translated on its own and the string reassembled.
- **39 dynamic patterns** for anything with a number in it, since plurals differ per language.
- **Normalisation** of source line breaks and typographic apostrophes, both of which silently broke exact matches.

In-game terms the community uses in English stay in English: hardpoint, blueprint, loadout, quantum drive, SCU, aUEC, RS.

---

## Contributing

Corrections to the data are the most useful thing — especially abundance figures, shop inventories, and anything that shifts between patches. Feature ideas welcome too. Open an issue or a PR.

---

## License

MIT. Unofficial tool, not affiliated with Cloud Imperium Games. Star Citizen® is a trademark of Cloud Imperium Rights LLC.

*gnmrclss*
