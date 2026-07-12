# Relational Threshold Urbanism

**A practitioner-researcher portfolio for PhD applications in computational architecture and urban analytics.**

Prepared by **Lin Wei** (United Design Practice, Singapore) as supporting research for PhD applications in computational architecture, urban analytics, and regenerative urbanism.

**→ Read the research brief: [index.html](./index.html)** (or via GitHub Pages, once enabled — see below)

---

## What this is

This repository asks a bounded, falsifiable version of a larger question: *can open geospatial data locate the everyday threshold spaces — sheltered walkways, void decks, playground edges, hawker rims, lift lobbies — that support human relational life in a dense tropical city, and where do dominant urban-sensing systems fail to see them?*

The work does not claim that open data can observe human relationships directly. It uses open data as an **attention-directing instrument**: a reproducible way to detect where spatial capacity, data invisibility, and later human observation may productively meet — narrowing where a fieldwork phase should look, rather than replacing it.

The research proceeds in tiers, each with a different evidentiary burden (stated plainly in the landing page, Section 04):

1. **Data visibility** — which pedestrian threshold spaces are visible or invisible to road-based urban sensing?
2. **Threshold affordance** — which spaces are materially equipped for pausing, waiting, sitting, eating, playing, gathering?
3. **Threshold transmissibility** — do local affordances stay isolated, or form connected fields across the pedestrian network?
4. **Relational holding** — do candidate fields actually hold people, validated through observation and situated accounts?

Tiers 1–3 are supported by open-data pilots in this repo (below). Tier 4 is future fieldwork, not yet run — the repo is explicit about that boundary rather than implying it's further along than it is.

## Repository structure

See [`REPO_STRUCTURE.md`](./REPO_STRUCTURE.md) for the full file tree and provenance of every file.

```
index.html                                   research landing page
pilot_03_threshold_transmissibility_packet.zip   standalone download of Pilot 03
docs/                                        conceptual notes, glossary
pilots/covered-city/                         all three open-data pilots: notebooks, data, figures
```

## The pilots

| Pilot | Question | Current result |
|---|---|---|
| **01 — Mapping the Covered City** | Which parts of Singapore's covered pedestrian network are plausibly invisible to road-based street-view imagery? | 26.5% of the covered network (~1,567 of 5,911 km) is plausibly beyond road-based camera reach |
| **02 — Threshold Affordance Overlay** | Are SVI-invisible segments disproportionately near lingering-supportive infrastructure (benches, shelters, hawker/food courts, community centres, playgrounds)? | 19.5% of SVI-invisible segments are affordance-adjacent at 20 m, vs. 6.1% of SVI-visible segments |
| **03 — Network vs. Proximity** | Does SVI-invisibility cluster more along the covered network's own connectivity than along simple geographic proximity — a first validation step toward a fuller graph-diffusion model? | Global Moran's I rises from 0.64 (simple proximity) to 0.79 (network-connectivity weights) for SVI-visibility, p<0.001 |

Each pilot's notebook, data, and figures live in [`pilots/covered-city/`](./pilots/covered-city/) — see that folder's own README for reproduction instructions.

## What open data can legitimately claim (and what it can't)

This is a deliberate, stated methodological boundary — not a caveat added after the fact:

- **Threshold affordance** → spatial capacity claim only. Cannot prove anyone actually lingers there.
- **Threshold transmissibility** → networked capacity claim only. Cannot prove trust, care, or social comfort spreads.
- **Relational holding** → requires observation and situated accounts. Not yet run.

Every notebook in this repo states its own limitations section as a finding, not an apology — see each pilot's closing markdown cells.

## Data & attribution

Pedestrian network geometry and affordance points are derived from **OpenStreetMap**, © OpenStreetMap contributors, available under the [Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/). Any reuse of the derived `.geojson` files in this repo should carry the same attribution.

## Reproducing the pilots

```bash
pip install -r requirements.txt
jupyter notebook pilots/covered-city/
```

See `requirements.txt` for exact packages (`geopandas`, `networkx`, `libpysal`, `esda`, `mapclassify`, `matplotlib`, `osmnx`).

## Citing this work

See [`CITATION.cff`](./CITATION.cff). If GitHub's citation UI is enabled for this repo, a formatted citation is available from the "Cite this repository" button on the repo homepage.

## License

Code and notebooks: MIT (see [`LICENSE`](./LICENSE)). Written notes, figures, and the landing page's text content: CC BY 4.0 — reuse with attribution. See `LICENSE` for the full split.

## Contact

Lin Wei · United Design Practice, Singapore · [lin.wei@uniteddesignpractice.com](mailto:lin.wei@uniteddesignpractice.com)
