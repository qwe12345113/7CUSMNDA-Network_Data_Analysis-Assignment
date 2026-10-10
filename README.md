# 7CUSMNDA — Network Data Analysis Coursework

**King's College London | Network Data Analysis | 2026**

This repository contains the code and supporting materials for a two-part network data analysis coursework project. The analyses examine (1) co-participation networks among Wikidata editors and (2) a driving-road network and historical road accidents in central Leeds.

## Project overview

| Part | Focus | Main techniques |
| --- | --- | --- |
| **Part 1: Wikidata editor networks** | Construct and compare editor interaction networks; assess potential exposure to suspicious behaviour | Weighted undirected graphs, connected components, degree distributions, clustering, shortest paths, Erdős–Rényi baselines, exposure ranking and illustrative SIR simulation |
| **Part 2: Leeds road network** | Characterise road structure, analyse accident locations and investigate marathon route feasibility | OSMnx road-network extraction, spatial metrics, planarity, accident snapping, Moran's I, network K-function, network Voronoi cells and closed-route search |

## Part 1 — Wikidata editor networks

Three datasets of different scales are analysed: `BOT_REQUESTS`, `PROPERTIES` and `PROJECT_CHAT`.

### Task A: Network construction

Each editor is represented by a node. Two editors are connected if they participated in the same page–thread discussion group; an undirected edge weight records the number of distinct discussion groups shared by the pair. The construction process removes missing and duplicate records, groups observations by page and thread, and connects unique participants in each group.

| Dataset | Editors | Edges | Largest-component ratio |
| --- | ---: | ---: | ---: |
| `BOT_REQUESTS` | 552 | 2,424 | 0.940 |
| `PROPERTIES` | 1,942 | 9,198 | 0.833 |
| `PROJECT_CHAT` | 4,136 | 40,255 | 0.949 |

### Task B: Network structure

The networks are evaluated using density, degree statistics, clustering, shortest paths and matched Erdős–Rényi random-graph baselines. All three exhibit much higher clustering than their random baselines while retaining relatively short paths, consistent with small-world organisation. Their strongly right-skewed degree distributions indicate a small number of highly connected editors.

### Task C: Exposure monitoring

A network-based monitoring framework ranks potentially exposed editors using proximity to suspicious sources, neighbourhood similarity, shared neighbours, tie strength and activity. Single-source and dual-source cases are considered. Short SIR-style simulations provide **illustrative scenarios**, not evidence that any editor actually engaged in trolling or that behavioural transmission occurred.

## Part 2 — Leeds road network and accidents

### Task A: Road-network construction

An approximately **1 km²** study area in central Leeds was selected using accident data aggregated over **2012–2016**. The chosen area contains **452 unique accidents**. A driving-road network was extracted from OpenStreetMap using OSMnx.

| Measure | Result |
| --- | ---: |
| Nodes | 211 |
| Edges | 359 |
| Intersections | 179 |
| Total edge length | 21.834 km |
| Average circuitry | 1.6071 |
| Graph-theoretic planarity | Non-planar |

### Task B: Road accidents

Accident locations are snapped to the road network and aggregated by road arc. The analysis uses Moran's I and a network K-function to investigate spatial clustering, and measures accident position as a fraction of road-arc length from the nearest intersection.

Key findings include **Moran's I = 0.1437** (permutation **p = 0.001**) and a mean nearest-intersection fraction of **0.2212**. The observed accident distribution is uneven and shows evidence of clustering across connected road segments.

### Task C: Network Voronoi cells and marathon routes

Four seed points are selected with attention to spatial separation, road accessibility and accident concentrations. A **node-based network Voronoi** partition assigns road-network nodes to their nearest seeds by shortest-path distance. A heuristic searches for closed routes close to **42 km** within the resulting cells.

The initial three-cell test and subsequent four-cell evaluation found **no feasible marathon-length closed route**. Reconfiguring the seeds did not change that outcome. The principal limitation identified in the report is the small geographic extent of the selected road network relative to the proposed marathon-route length.

## Repository contents

The coursework deliverables are a written report and documented analysis code. Refer to the files and folders in this repository for the exact notebook names, supporting datasets and generated figures. The submitted report provides the full interpretation of methods and findings.

## Running the analysis

The code uses Python network and spatial-analysis tools, including packages such as:

- `pandas` and `networkx` for data processing and graph analysis
- `matplotlib` for visualisation
- `osmnx` for driving-road network extraction and spatial graph metrics
- `geopandas` and `shapely` for spatial data handling
- `spaghetti` and associated spatial-analysis tools for network-constrained accident analysis

**Before running:** check the imports in the notebooks and install their required packages in a compatible Python environment. Obtain the Wikidata discussion CSV files and Leeds accident datasets from the sources identified in the coursework instructions. Update local data paths where necessary, then run the notebooks in their documented order. Package versions, notebook filenames and data paths should be taken from the repository itself; they are not fixed here.

## Interpretation and limitations

- Wikidata edges indicate **shared discussion participation**, not verified direct replies or observed behavioural transmission.
- The SIR model is **illustrative**, and network exposure scores are not accusations of misconduct.
- Road-accident results describe recorded events and network associations; they do not establish causality or exposure-adjusted collision rates.
- A valid Voronoi service-area partition does not guarantee a feasible 42 km route. The selected 1 km² study area is too limited for the specified four-cell marathon design under the analysed route-search procedure.

## Data sources

- **Wikidata Talk-page datasets:** dataset collection supplied for the coursework.
- **Road network:** [OpenStreetMap](https://www.openstreetmap.org/), accessed programmatically through OSMnx.
- **Leeds road traffic accidents:** [UK government road-traffic-accident dataset](https://data.gov.uk/dataset/6efe5505-941f-45bf-b576-4c1e09b579a1/road-traffic-accidents).

## Author

**Hsiang-Yin Cheng**  
King's College London — 7CUSMNDA Network Data Analysis Coursework (2026)
