# MAGICA School 2026 — Workshop Project Summary

_24 forks checked · 119 new files found · ~18 forks with substantive work_

---

## Collaborative Groups

Notebooks with the same (or very similar) filename appearing in multiple forks indicate attendees working together.

**Group 1 — Gulf of Tunis (Tunisia team): SilverFox275 + nadia-mkh + MALEK313-sketch**
All three share: `cmems_salinity_tunisia.ipynb`, `copernicus_marine-Tunisia.ipynb`, `gulf_of_tunis_tutorial.ipynb`, `marine_heatwave_gulf_of_tunis.ipynb`, `planetary_computer_Tunis.ipynb`

**Group 2 — Mediterranean Climatology: emmaventura2102-ship-it + Moccia13**
Both carry numbered `Group Project/1–5.ipynb` covering Mediterranean SST, salinity, and chlorophyll climatology/anomalies (1987–2025). Notebooks are identical — worked as a group.

**Group 3 — Tarragona Coastal Change: cirozugar + RakeshSwain2604**
Both carry `spain-v1.ipynb` with the same Tarragona bbox and structure. RakeshSwain also has `ibi_wave_icechunk.ipynb` writing to an `rswain` Icechunk bucket — same bucket referenced in cirozugar's IBI wave work.

**Group 4 — Gulf of Lion Oceanography (LAR project): LauraF97 + robertasaulporrino-bit + angelagarzia-byte**
Named explicitly: folder `LAR(Laura_Angela_Roberta)_Project/`. All three carry T-S diagrams, salinity, temperature, surface current quiver maps, and SOCIB WMOP model access.

**Group 5 — Baltic Sea: maexer1998 + MoeinDst**
Both carry `baltic_sst_yearly_comparison.ipynb`; MoeinDst has `_v2`. maexer1998 adds a Baltic wave hindcast (Storm Babet, Oct 2023).

**Group 6 — Cyclone Mocha: sofiaalovato + ItaloRLopes + capellaraquelgn-hue**
Three complementary perspectives on Cyclone Mocha (Bay of Bengal, May 2023): atmosphere+ocean+Icechunk (sofiaalovato), ERA5 pressure + IBTrACS track + DTM/flood VAPs (ItaloRLopes), ocean biogeochemical response (capellaraquelgn-hue).

**Group 7 — Equatorial Pacific SST / El Niño: pendaoriana47-svg + valsazonova + virginiasofiacampanella-beep**
All use the NASA MUR SST Zarr dataset on AWS S3 to compute monthly climatology and anomaly. pendaoriana47-svg frames it as "Equatorial Pacific SST and its influence on the Peruvian coast."

**Solos:**
- **Astro-Helen**: Red Sea SST yearly comparison (CMEMS MetOffice L4)
- **majidniazkar**: Mediterranean SST/salinity/chlorophyll anomalies + ERA5 wind anomalies + ERA5 Icechunk virtual store from ARCO-ERA5 on GCS
- **grokun**: Added a CF/UGRID lecture notebook
- **TheJeran**: Arctic imagery processing — converting EXR to float16 global arrays

---

## Project Summaries & FAIR Assessment

---

### 1. Gulf of Tunis — SST, Salinity, Marine Heatwaves

**Members:** SilverFox275, nadia-mkh, MALEK313-sketch

**Science:** Multi-source oceanographic analysis of the Gulf of Tunis. Salinity from CMEMS Mediterranean Physics Reanalysis (4.2 km daily), SST from the L3S satellite composite product, chlorophyll from Sentinel-3 OLCI via Planetary Computer STAC, and marine heatwave detection using the Hobday et al. (2016) method (90th-percentile threshold per pixel, ≥5 consecutive days, JAS 2016–2025, with a fixed climatological baseline 1994–2015). The most complete version includes spatial MHW frequency maps, SST maps at peak events, and co-located Chl-a from STAC.

| FAIR | Assessment |
|------|-----------|
| **F — Findable** | Good — notebooks have clear titles and explicit dataset IDs in metadata headers. Slight issue: some notebooks use `(1)` suffixes rather than meaningful names. |
| **A — Accessible** | Good — all data streamed via `copernicusmarine` Python client (no downloads) and Planetary Computer STAC API. One notebook accesses a local `.nc` file, breaking reproducibility. |
| **I — Interoperable** | Strong — xarray + CF-compliant CMEMS datasets, Kelvin→Celsius conversions documented, CF variable names used (`so`, `thetao`, `adjusted_sea_surface_temperature`). |
| **R — Reusable** | Moderate — bbox defined once and reused, parameters set at top. However, **passwords are hardcoded in plain text** in several notebooks (significant security concern). Notebook structure is well-documented with numbered sections. |

---

### 2. Mediterranean Climatology & Anomalies (SST, Salinity, Chlorophyll)

**Members:** emmaventura2102-ship-it, Moccia13

**Science:** Systematic basin-wide analysis of the Mediterranean Sea (1987–2025 for physics, 1999–2025 for BGC). Five notebooks: (1) SST climatology/anomalies/extremes with MP4 export, (2) SST pixel time series at Venice and Gulf of Lion, (3) salinity climatology/anomalies, (4) chlorophyll climatology/anomalies, (5) chlorophyll pixel time series. Uses CMEMS Mediterranean Multiyear Physics and BGC reanalysis (4.2 km monthly), with Coiled distributed computing (30 ARM workers on spot instances).

| FAIR | Assessment |
|------|-----------|
| **F** | Excellent — numbered workflow steps in each notebook, clear titles, organized in a `Group Project/` folder. |
| **A** | Excellent — all data via `copernicusmarine` open API, Coiled cluster for scalable access. |
| **I** | Very strong — standard CF variable names, proper unit labels (`°C`, `PSU`, `mg m-3`), `cmocean` colormaps follow oceanographic convention. |
| **R** | Strong — `MED_BBOX`, `TIME_START`, `TIME_END` parameters defined once and reused across all five notebooks. Consistent structure throughout. Missing: no `requirements.txt` or package pinning. |

---

### 3. Coastal Shoreline Change — Tarragona, Spain

**Members:** cirozugar, RakeshSwain2604

**Science:** Cloud-native time series analysis of shoreline change on the Tarragona coast / Ebro Delta (2017–2024). Uses Sentinel-2 L2A (Planetary Computer STAC) to compute NDWI and MNDWI water indices. Methodology iterated from Otsu thresholding (v2) to a fixed threshold at 0 (v3/final) after finding Otsu unreliable across seasons with different illumination geometry. CMEMS sea level anomaly and significant wave height provide environmental context. cirozugar also studied Arrecife Alacranes coral islands (Gulf of Mexico) with the same approach. RakeshSwain adds an EOPF GeoZarr demo for the Ebro Delta, IBI wave reanalysis in Icechunk, and a Panel satellite data explorer app.

| FAIR | Assessment |
|------|-----------|
| **F** | Excellent — cirozugar explicitly includes a FAIR compliance checklist in each notebook: "All data via public APIs, reproducible on JupyterHub, outputs documented, results to be published via Zenodo + STAC catalog." |
| **A** | Excellent — Sentinel-2 via STAC, CMEMS via Python client, IBTrACS via NOAA CSV. No local files. |
| **I** | Strong — rioxarray for CRS handling, geopandas for vector, standard water indices cited (McFeeters 1996, Xu 2006), EOPF GeoZarr backend for Sentinel-2. |
| **R** | Very strong — best-documented project at the school. Clear scientific question at top of each notebook, methodology comparison table, versioned notebooks (v1→v3→final) with documented rationale for each change. Zenodo publication planned. |

---

### 4. Gulf of Lion — Water Mass Characterization

**Members:** Laura (LauraF97), Angela (angelagarzia-byte), Roberta (robertasaulporrino-bit)

**Science:** Multi-variable oceanographic characterization of the Gulf of Lion: surface temperature, salinity, ocean currents (quiver maps and streamlines), T-S diagrams, and — uniquely — seawater potential density (σ_t) computed from scratch using the UNESCO EOS-80 polynomial equation from T and S fields. Also accesses the SOCIB WMOP model (Western Mediterranean Operational Model) via OPeNDAP for near-real-time surface circulation.

| FAIR | Assessment |
|------|-----------|
| **F** | Moderate — notebooks have generic names (`Temp.ipynb`, `Sal.ipynb`, `Density.ipynb`), not self-describing in isolation. The `LAR(Laura_Angela_Roberta)_Project/` folder name is meaningful. |
| **A** | Good — CMEMS via Python client, SOCIB WMOP via OPeNDAP (standard DAP protocol). Both open services. |
| **I** | Good — CF variable names used throughout, Cartopy for standard map projections, quiver plots follow oceanographic convention. Implementing UNESCO EOS-80 manually demonstrates understanding of the physical equations. |
| **R** | Moderate — notebooks lack introductory markdown cells explaining the scientific goal. Code is functional but sparse on documentation. Parameters (bbox, dates) hardcoded inside cells rather than defined at the top. |

---

### 5. Baltic Sea — SST & Storm Waves

**Members:** maexer1998, MoeinDst

**Science:** Baltic Sea SST yearly comparison (DMI CMEMS L4 product) with careful geographic masking of Lake Vänern, Lake Vättern, and Norwegian/Skagerrak waters. Monthly seasonal cycles and a Warnemünde point SST anomaly heatmap. Also an in-depth analysis of Storm Babet (October 2023) using the CMEMS Baltic Wave Hindcast (1 nmi resolution, hourly): animated Panel Player map of wave height and direction, five wave parameters examined (`VHM0`, `VCMX`, `VHM0_WW`, `VTPK`, `VMDR`).

| FAIR | Assessment |
|------|-----------|
| **F** | Good — version-stamped notebook (`version 1.0.2`, `23.04.2026`), clear descriptive titles. MoeinDst's `_v2` suffix shows iteration. |
| **A** | Excellent — all data via `copernicusmarine` open API. |
| **I** | Good — standard CF wave variable names, geoviews `VectorField` for wave direction (standard meteorological convention), OSM background tiles. |
| **R** | Good — masking logic is well-commented (explains which geographic artifacts are masked and why). Coiled cluster config follows instructor template. Could benefit from parameterized bbox definition. |

---

### 6. Cyclone Mocha — Multi-perspective Analysis

**Members:** sofiaalovato, ItaloRLopes, capellaraquelgn-hue

**Science:** Three complementary perspectives on Cyclone Mocha (May 2023, Bay of Bengal — one of the strongest on record, ~74 m/s peak winds):

- **sofiaalovato**: Integrated atmosphere (ERA5/Open-Meteo: wind, pressure, precipitation, CAPE) + ocean (CMEMS SSH/`zos`) + IBTrACS track. All datasets committed to an Icechunk store on S3 as versioned snapshots, then read back for analysis. Time-travel across commits demonstrated.
- **ItaloRLopes**: ERA5 MSL pressure fields with animated time slider + IBTrACS track visualization. DTM analysis of the Rakhine State landfall zone + Sentinel Asia flood Value-Added Products (VAPs) for the Bangladesh/Chittagong coast.
- **capellaraquelgn-hue**: Ocean biogeochemical response — physical and biogeochemical CMEMS variables across the full Bay of Bengal through the storm lifecycle (pre-storm baseline → peak → recovery).

| FAIR | Assessment |
|------|-----------|
| **F** | Good — clear scientific questions stated, named cyclone as title. |
| **A** | Good — Open-Meteo (free, no auth), IBTrACS (NOAA, free CSV), CMEMS (credentialed but open). ItaloRLopes partially breaks A by requiring pre-downloaded ERA5 files. |
| **I** | Strong — xarray throughout, standard CMEMS variables, IBTrACS CSV format (NOAA standard), Icechunk zarr-compatible store. |
| **R** | sofiaalovato's notebook is the most advanced — explicit commit snapshots enable reproducing any intermediate state. ItaloRLopes has clear multi-part notebook structure. capellaraquelgn-hue's content was largely unfetchable. |

---

### 7. Equatorial Pacific SST / El Niño

**Members:** pendaoriana47-svg, valsazonova, virginiasofiacampanella-beep

**Science:** Monthly SST climatology and anomaly computed from NASA MUR SST (1 km daily, Zarr on AWS S3 public dataset), subsetted to the equatorial Pacific (±25°N). pendaoriana47-svg's final notebook is framed as "Equatorial Pacific SST and its influence on the Peruvian coast" — an El Niño study. Large Coiled clusters (40–200 workers) used for computation.

| FAIR | Assessment |
|------|-----------|
| **F** | Weak — many notebooks have generic names (`Project.ipynb`, `Project 2.ipynb`, `Untitled1.ipynb`). The final `main.ipynb` has a proper descriptive title. |
| **A** | Excellent — MUR SST is an AWS Open Data Registry Zarr store, no authentication required. |
| **I** | Good — xarray, Zarr, standard CF-like variable names and dimension names. MUR SST is a well-documented public dataset. |
| **R** | Moderate — the included `aws_mur_sst_tutorial_short.ipynb` (credited to Gentemann, Signell, Abernathey) is well-documented, but the project notebooks are sparse on scientific context and explanation. |

---

### 8. Red Sea SST — Astro-Helen (solo)

**Science:** Yearly comparison of Red Sea SST (MetOffice CMEMS L4 global product), subsetting to 12–30°N, 32–44°E, computing monthly means per year with interactive spatial maps and seasonal cycle plots. Uses Coiled ARM cluster (30 workers, eu-central-1).

| FAIR | Assessment |
|------|-----------|
| **F** | Good — version-stamped (`version 1.0.2`, `23.04.2026`). |
| **A** | Excellent — `copernicusmarine` open API. |
| **I** | Good — standard variable names, spatial subset well-documented. |
| **R** | Moderate — well-structured but few markdown cells explaining the scientific motivation. |

---

### 9. Mediterranean + ERA5 Wind + ERA5 Icechunk — majidniazkar (solo)

**Science:** Most prolific individual fork (7+ files). Mediterranean SST, salinity, and chlorophyll anomalies (same variables as Group 2 but worked independently), a combined SST+Chl notebook, pixel time series, ERA5 10-m wind speed anomalies (1979–2022) from Planetary Computer ERA5-PDS, and — most technically advanced — an **ERA5 Icechunk virtual store** built from ARCO-ERA5 files on Google Cloud Storage (anonymous HTTPS), with the Icechunk repo written to protocoast S3. This bridges two different cloud providers transparently.

| FAIR | Assessment |
|------|-----------|
| **F** | Good — clear descriptive notebook titles throughout. |
| **A** | Excellent — CMEMS Python client, Planetary Computer STAC (ERA5-PDS), and anonymous GCS access. All open. |
| **I** | Excellent — the ERA5 Icechunk notebook is the most technically sophisticated individual contribution, demonstrating true cloud-native interoperability: GCS (source) → S3 (Icechunk store) with virtual chunk references. |
| **R** | Good — parameters defined at top, systematic workflow. ERA5 variable selection table included. |

---

### 10. Arctic Data Processing — TheJeran (solo)

**Science:** Arctic imagery processing — converting EXR format files to float16 global arrays using `openexr_numpy`. Very different approach from the rest of the workshop (no xarray, no CMEMS, no STAC). Limited context available.

| FAIR | Assessment |
|------|-----------|
| **F** | Weak — no descriptive titles or metadata context available. |
| **A** | Unclear — file-based workflow, no open API access demonstrated. |
| **I** | Weak — EXR format is not a standard oceanographic/geoscience format. |
| **R** | Weak — minimal documentation available. |

---

## Overall FAIR Assessment

| Dimension | Strongest | Weakest |
|-----------|-----------|---------|
| **Findable** | cirozugar/RakeshSwain (explicit FAIR tables, versioned titles) | pendaoriana47-svg (generic names), TheJeran |
| **Accessible** | Nearly everyone via CMEMS Python client + STAC | ItaloRLopes (local ERA5 files), TheJeran |
| **Interoperable** | majidniazkar (GCS→S3 Icechunk bridge), Gulf of Lion group (EOS-80 from scratch) | TheJeran (EXR format) |
| **Reusable** | cirozugar (versioned notebooks, method rationale documented), emmaventura group (consistent parameterization) | LAR group (generic names, hardcoded params), Gulf of Tunis group (passwords in plain text) |

---

## Notable Cross-cutting Observation

The **Taranto Icechunk append notebook** appeared in 9 forks (glomoz/SilverFox275, emmaventura, ciri, rswain/rsignell, RakeshSwain, italorlopes, max/maexer1998, and others), each personalized to a different S3 bucket. This was clearly a hands-on exercise that nearly every attendee completed — strong evidence of skill transfer on cloud-native versioned data management with Icechunk.
