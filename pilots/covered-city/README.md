# Pilots: The Covered City

Three open-data pilots, run in sequence, each building on the last. All use Singapore's covered pedestrian network — footways, void decks, and sheltered walkways tagged in OpenStreetMap — as the shared spatial unit.

Every pilot notebook ends with two sections that are treated as findings, not disclaimers: **what this pilot does not show**, and **limitations, stated plainly**. Read those before citing a headline number elsewhere.

## Pilot 01 — Mapping the Covered City
`01_mapping_the_covered_city.ipynb` / `.html`

**Question.** Which parts of the covered pedestrian network are plausibly invisible to road-based street-view imagery (SVI)?

**Method.** Every covered segment's distance to the nearest drivable road is used as a floor-estimate proxy for SVI visibility (SVI cameras are road-based; segments far from any road are unlikely to be captured). A sensitivity sweep across visibility thresholds (10–50 m) checks how much the headline number depends on that choice.

**Output.** `data/sg_covered_ways_svi_visibility.geojson` — 73,168 covered segments, each flagged `svi_visible: True/False`. This file is reused as the input to both Pilot 02 and Pilot 03.

> **Note on the hosted copy.** The version actually committed to this repo is `data/sg_covered_ways_svi_visibility_6dp.geojson` — coordinates rounded to 6 decimal places (~11 cm precision, far tighter than the 20 m analysis radius used throughout) purely to fit under GitHub's 25 MB web-upload limit. Running the notebook fresh will regenerate the full-precision, un-suffixed file; rename or re-point `DATA` if you want your local output to match the hosted filename exactly.

**Result.** 26.5% of the covered network (~1,567 of 5,911 km) is plausibly beyond road-based camera reach at the primary threshold; the sweep (`data/sensitivity_sweep.csv`, `figures/sensitivity.png`) shows this ranges from 17.8% to 32.9% across the threshold range tested.

## Pilot 02 — Threshold Affordance Overlay
`02_threshold_affordance_overlay.ipynb` / `.html`

**Question.** Are SVI-invisible segments disproportionately located near infrastructure that materially supports lingering — benches, shelters, hawker/food courts, community centres, playgrounds?

**Method.** Affordance points fetched fresh from OpenStreetMap each run (not saved to a static file — see note below) and cross-referenced against Pilot 01's visibility classification at multiple search radii.

**Result.** At a 20 m radius, 19.5% of SVI-invisible segments are affordance-adjacent, compared with 6.1% of SVI-visible segments (`figures/affordance_sensitivity.png`, `figures/invisible_affordance_overlap.png`).

**Note on reproducibility.** This notebook fetches affordance points live from OSM/Overpass on each run; the per-segment affordance-adjacency column is not currently saved as a standalone file. Re-running the notebook regenerates it. A future revision should save this output (e.g. `data/sg_covered_affordance_overlay.geojson`) so Pilot 03's network-vs-proximity comparison can be re-run directly on the affordance signal instead of on SVI-visibility alone.

## Pilot 03 — Network vs. Proximity
`03_network_vs_proximity_pilot.ipynb` / `.html`

**Question.** Does SVI-invisibility cluster more strongly along the covered network's own physical connectivity than along simple geographic proximity? A first, narrower validation step ahead of a fuller graph-diffusion model (see the landing page's Plate 01) — testable entirely on data already in hand, no new fetch, no fieldwork.

**Method.** Within a bounded pilot area (7,970 segments), two spatial weights matrices are built over the same segments: a conventional K-nearest-neighbour matrix on straight-line distance (`W_geo`), and a matrix built from the walkway network's own topology — segments are neighbours only if they physically connect (`W_net`). Global Moran's I and Local Moran (LISA) are computed under both.

**Result.** Global Moran's I rises from 0.64 (`W_geo`) to 0.79 (`W_net`) for SVI-visibility — a +0.15 gap, significant at p<0.001 under 999 permutations (`data/moran_comparison.csv`, `figures/moran_comparison.png`). LISA localises this into 624 segments in a significant invisible cluster, 1,230 in a visible cluster, and 27 spatial outliers — the natural shortlist for future fieldwork (`data/pilot03_lisa.geojson`, `figures/lisa_cluster_map.png`).

**What this does not show.** It tests whether a purely open-data-derived property (SVI-visibility) propagates along network structure — not whether social life, care, or holding does. No affordance/capacity variable is used yet.

A fuller, standalone packet of this pilot (executed notebook + data + figures + its own README) is also available as [`/pilot_03_threshold_transmissibility_packet.zip`](../../pilot_03_threshold_transmissibility_packet.zip) at the repo root.

---

## Reproducing any pilot

```bash
pip install -r ../../requirements.txt
jupyter notebook
```

Each notebook reads from and writes to the `data/` and `figures/` folders alongside it using relative paths — open them from within `pilots/covered-city/` so those paths resolve.

## Regenerating the HTML exports

The landing page links to the `.html` version of each notebook, not the `.ipynb`. After editing any notebook, re-export:

```bash
jupyter nbconvert --to html 01_mapping_the_covered_city.ipynb
jupyter nbconvert --to html 02_threshold_affordance_overlay.ipynb
jupyter nbconvert --to html 03_network_vs_proximity_pilot.ipynb
```
