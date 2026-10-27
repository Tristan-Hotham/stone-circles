# Same Shape, Different Millennia

Every stone circle in Europe's open map data on one map: 3,451 stone circles and ship settings from OpenStreetMap and Wikidata, cleaned, de-duplicated and sorted into the traditions archaeologists recognise, with when each tradition was built.

**Interactive version:** https://tristan-hotham.github.io/stone-circles/

This repository holds the interactive page, the cleaned catalogue, the dating evidence and the analysis code for the data study *Same Shape, Different Millennia: stone circles in Europe's open data* by Dr Tristan Hotham (Independent researcher, ORCID 0000-0003-4931-9349). Companion studies built from the same data pull: [Megalith Highway](https://tristan-hotham.github.io/megalith-highway/) and [Barrows of Europe](https://tristan-hotham.github.io/barrows-of-europe/). Blog: https://blog.tristanhotham.com/

## Headline results

- After cleaning and merging, the catalogue holds 3,451 records in 21 countries: 3,334 stone circles and 117 ship settings.
- 62% (2,143) are Iron Age judge's rings in Scandinavia and Finland; only 20% are the Neolithic and Bronze Age circles of Britain, Ireland, Brittany and south-west Iberia. 95% of Sweden's 2,172 records come only from Wikidata, so the size of this lead partly reflects what has been digitised.
- The traditions span 6,400 years on their published dates, from the Alentejo cromlechs (6000 BC) to the Gothic circles of Pomerania (to AD 400). Almendres and Odry are 2,605 km apart.
- 356 p3k14c radiocarbon dates link to 43 named circles. Of 37 dated circles in Britain and Ireland, 30 have a middle date inside 3300 BC to 900 BC; three Pyrenean circles fall between 890 BC and 804 BC.
- Traditions that touch in both time and space: Britain and Brittany (116 km), Sweden and Pomerania (186 km, overlapping by 325 years). Britain and Scandinavia do not: 411 km of sea and about 400 years apart. The data are consistent with at least two separate beginnings, though they cannot prove reinvention.
- In Britain and Ireland, 65% of circles stand higher than the typical random point 1 to 5 km away, relative to ground within 1 km, and 60% have a wider view within 5 km: a real but gentle preference.

## Files

- `index.html`: the interactive page (Leaflet map with tradition, year and country filters, date ribbon, charts, small multiples).
- `header.png`: social card.
- `data/stone_circles.csv` and `data/stone_circles.geojson`: the cleaned catalogue, one row per record: id, name, form (stone circle or ship setting), tradition, country, lat, lon, source (osm, wikidata or both), evidence, OSM id, Wikidata QID, English Wikipedia link, OSM and Wikidata period tags, whether the OSM object is an outline (point = first vertex).
- `data/traditions.csv`: each tradition's published date range, core period, quoted sentence, source and URL.
- `data/radiocarbon_links.csv`: every radiocarbon date used, with the circle it is linked to, the link distance and shared word, and its calibrated median and 95% range. `data/radiocarbon_link_audit.csv`: all 115 candidate links within 5 km and whether each was used.
- `data/famous_circles.csv`: the twelve circles in the small multiples and how each was located.
- `data/landscape_bi.csv`: height, local rank and view for each circle in Britain and Ireland and the means of its ten comparison points.
- `data/audit_name_only.csv`: every OpenStreetMap name match and whether it was kept. `data/audit_excluded.csv`: records removed (modern, outside Europe, not a circle).
- `data/results.json`: every number quoted on the page, in the README, paper, blog and collage.
- `code/`: Python scripts, run in order: `01_catalogue.py`, `02_dates.py`, `03_geography.py`, `04_landscape.py`, `05_results.py`, `06_build_site.py`, `07_header.py`. `dem.py` is the elevation reader and line-of-sight function from Within Sight. Release outputs (`release/`: paper, blog, Zenodo files) come from `08_release_figs.py`, `09_paper.py` (fills `paper_template.tex`, needs xelatex) and `10_release.py` (fills `blog_template.html`); the collage from `reddit/collage.py`. `shots.py` takes checking screenshots of the page.

The raw inputs are not included (see Sources). `02_dates.py` downloads the IntCal20 curve file from the rcarbon package on GitHub if it is missing.

## Method in brief

OpenStreetMap: objects tagged `megalith_type=stone_circle`, `cromlech` or `stone_ship`, or `historic=stone_circle` (1,096), plus name matches in many languages (117 kept of 2,415, see the audit file). Wikidata: instances of stone circle and its subclasses, and of stone ship (2,585 in Europe). De-duplication: 180 by shared Wikidata QID, 98 by distance (nearest same-form item within 100 m), 48 OSM repeats. 22 modern circles removed. Traditions are assigned by place and form. Dates come from published ranges for each tradition and from p3k14c radiocarbon dates linked by name within 1 km, calibrated with IntCal20.

Caveats: counts are records, not monuments, and coverage differs greatly by country (Sweden via a register import into Wikidata; Britain and Ireland about 53% of the roughly 1,300 circles archaeologists list); dates belong to traditions, not to individual circles; a radiocarbon date at a circle dates some activity there, not necessarily its building; OSM outlines are placed at their first vertex.

## Sources and licences

- OpenStreetMap: © OpenStreetMap contributors, ODbL 1.0 (https://www.openstreetmap.org/copyright). Pulled from the QLever OSM planet endpoint on 27 October 2026.
- Wikidata: CC0 (https://www.wikidata.org).
- p3k14c: Bird, D. and others 2022, "p3k14c, a synthetic global database of archaeological radiocarbon dates", Scientific Data 9, 27. CC BY 4.0. https://github.com/people3k/p3k14c
- IntCal20: Reimer, P. and others 2020, Radiocarbon 62. File from the rcarbon R package (https://github.com/ahb108/rcarbon).
- Elevation: AWS Terrain Tiles by Mapzen/Tilezen (https://registry.opendata.aws/terrain-tiles/), attribution https://github.com/tilezen/joerd/blob/master/docs/attribution.md
- Natural Earth (public domain): coastline and countries.
- Published date ranges: see `data/traditions.csv` (Wikipedia articles on Stone circles in the British Isles and Brittany, Almendres Cromlech, Stone ship, Stone circle (Iron Age) and Wielbark culture; Mujika-Alustiza and others 2018, Munibe Antropologia-Arkeologia 69; medievalheritage.eu pages on Odry and Grzybnica).
- Base map tiles on the page: © Esri. Map library: Leaflet.

**Licence.** The derived data in `data/` include OpenStreetMap data and are released under the Open Database License (ODbL 1.0). Text and figures are CC BY 4.0. Code is MIT (see `LICENSE`).

## Citation

Hotham, T. (2026) *Same Shape, Different Millennia: stone circles in Europe's open data.* Zenodo. https://doi.org/10.5281/zenodo.23685256

I wrote the text, with drafting and editing assistance from Claude (Anthropic), which also helped prepare the analysis code. I reviewed and checked all text and results.
