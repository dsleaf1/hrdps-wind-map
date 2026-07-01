# HRDPS Wind Map — BC Coast

A single self-contained web page showing **ECCC HRDPS 10 m wind** for the BC coast,
Beaufort-coloured over a plain coastline, with a 48-hour timeline. In the **San Juan
& Gulf Islands** region it overlays **live NOAA tidal currents** and a
**wind-against-current wave-steepness hazard ring** on each pass — the breaking-sea
danger that matters most to sea kayakers.

**▶ Live map: <https://dsleaf1.github.io/hrdps-wind-map/>**

## Features

- True ~2.5 km HRDPS wind via the `hrdps-ingest` pipeline → Cloudflare R2 (all 48 h
  held in memory for instant zoom/scrub); GeoMet WCS ~3.7 km auto-fallback; optional
  1 km inshore nest.
- Six coast regions (Haida Gwaii → Puget Sound), touch pan/zoom, big +/− buttons.
- San Juan overlay: 14 curated NOAA passes with real mean flood/ebb directions, live
  `currents_predictions`, riding the same timeline.
- Hazard rings coloured by predicted wave steepness (green → crimson), from the
  deep-water wave–current steepening physics; waves from Open-Meteo Marine.

## How the hazard is computed

Full derivations, equations, figures, and the exact data sources (with how the
station coordinates were discovered from NOAA's public directory, no manual input):

- **[Physics & data reference (web, renders equations + figures)](wave_current_steepness.md)**
- **[Same document as PDF](wave_current_steepness.pdf)**

In short: an opposing current shortens a wave's length *and* raises its height, so
steepness `S = H/L` climbs on both counts and runs away toward the **blocking
current `c₀/4 ≈ 0.76·T` kt**, where the waves stop and break in place — a tide race.
The ring colour tracks `S` against kayak-conservative thresholds (1/20, 1/13, 1/10,
1/7).

## Data sources

- **Wind** — ECCC HRDPS (MSC Datamart GRIB2 / GeoMet WCS).
- **Currents** — NOAA CO-OPS `currents_predictions` + station metadata (`mdapi`).
- **Waves** — Open-Meteo Marine.

Static deploy; coastline inlined; `geotiff.js` only for the GeoMet fallback.
