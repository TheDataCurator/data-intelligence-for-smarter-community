# Smart Community Testbed on Databricks: TAMU Smart Campus Workshop

A hands-on, six-lab workshop that takes students end-to-end on the Databricks Data
Intelligence Platform using **synthetic cellular-tower + smart-campus data** for the Texas A&M
campus in College Station — the raw material for the datathon's **transit** and **security** themes.

Students finish with a live, single-tab **Databricks App**: an interactive campus map over
their own data, with an inline **Ask Genie** panel.

## The arc

| Lab | Notebook | Builds |
|---|---|---|
| 01 | `01 - Hands On - Explore & Profile the Data` | Query + profile the Bronze telemetry in UC (generation happens in Classroom-Setup); confirm the TAMU campus geodata is staged in a Volume |
| 02 | `02 - Hands On - Clean & Transform` | Ingest the Texas A&M campus geodata (Volume → `dim_buildings` + `dim_zones`), then clean all Bronze → Silver |
| 03 | `03 - Hands On - Visualize with AI-BI` | AI/BI dashboard (transit + security views) |
| 04 | `04 - Hands On - Build Serving Tables` | Gold serving tables (`building_activity`, `cell_health`) |
| 05 | `05 - Hands On - Create a Genie Space` | Natural-language Q&A space + captured Space ID |
| 06 | `06 - Hands On - Deploy the App` | Live single-tab campus-map app on their data |

Open `00 - Course Overview` first for orientation, then run **labs 01 → 06 in order** — each
depends on the previous.

## How isolation works

Following the Databricks Academy pattern, each lab's first cell runs a
`Includes/Classroom-Setup-0N` that provisions a **per-student catalog**
`labuser_<username>` with `bronze` / `silver` / `gold` schemas (Vocareum catalogs are
detected and reused). No shared state; students only build in their own catalog.

## Layout

```
workshop/
├── 00 - Course Overview.py
├── 01..06 - Hands On - *.py          # the six labs
├── Version Info.py
├── README.md
└── Includes/
    ├── Classroom-Setup-Common.py     # helper library (catalog, schemas, compute check, app helpers)
    ├── Classroom-Setup-01..06.py     # per-lab setup (chains to Common)
    ├── smart_campus_generators.py    # telemetry generator, run by Classroom-Setup (generate_telemetry)
    ├── geojson/                      # TAMU building/zone polygons from OpenStreetMap (ODbL)
    └── reference_code/app/           # the trimmed single-tab app, pre-built (Lab 06 deploys this)
```

## Requirements

- A lab / sandbox workspace (Serverless), Unity Catalog enabled, with permission to create a catalog.
- Not for production workspaces — the setup creates catalogs, schemas, tables, a Genie space, and an App.

## Tuning

- `WORKSHOP_SCALE` in `Includes/Classroom-Setup-Common.py` controls generated row counts
  (default `0.15` for a fast run; set `1.0` for the full-size dataset).

## Attribution

Building footprints, names, and neighbourhoods from **OpenStreetMap** contributors under the
**Open Database License (ODbL)**. All telco-attributed telemetry
is synthetic demo data modeled on publicly-known patterns — not derived from any carrier's
proprietary data.

---

_Modified November 2026 by Hayley Horn for the TAMU Datathon, from the original [databricks-solutions/data-intelligence-for-smarter-community](https://github.com/databricks-solutions/data-intelligence-for-smarter-community): UBC campus data and references replaced with Texas A&M campus data from OpenStreetMap (ODbL)._
