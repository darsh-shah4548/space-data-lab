# Space Data Lab

Analyze real-world environmental events from space using Python and free satellite data.

10 interactive Jupyter notebooks that detect wildfire burn severity, map floods, monitor droughts, and track urban growth — all from Sentinel-2 and Landsat satellite imagery via Microsoft Planetary Computer.

---

## What it does

Each notebook connects to free satellite data and produces visual analysis of a real event:

| Notebook | What it analyzes | Index used |
|----------|-----------------|------------|
| 01 - First Multispectral Win | Load satellite data, create RGB composites, compute NDVI | NDVI |
| 02 - Seasonal Comparison | Summer vs winter vegetation changes | NDVI |
| 03 - Time Series Animation | Full year of vegetation change as animated GIF | NDVI |
| 04 - Cloud Masking | Filter clouds using Sentinel-2's classification layer | SCL |
| 05 - Spectral Indices | Water, urban, and burn detection beyond NDVI | NDWI, NDBI, NBR |
| 06 - Wildfire Analysis | **LA Palisades Fire** (Jan 2025) burn severity | dNBR |
| 07 - Flood Detection | **Brazil floods** (May 2024) water extent mapping | NDWI |
| 08 - Drought Analysis | **California** 2019 (normal) vs 2021 (drought) | NDVI |
| 09 - Urban Expansion | **Ahmedabad, India** urban growth 2016-2024 | NDBI |
| 10 - Decade of Urban Growth | **Bangalore, India** year-by-year 2016-2025 | NDBI |

---

## Getting started

### Prerequisites

- Python 3.9+
- No API keys needed — all data is free via Microsoft Planetary Computer

### Installation

```bash
git clone https://github.com/darsh-shah4548/space-data-lab.git
cd space-data-lab
pip install -r requirements.txt
```

### Usage

```bash
jupyter notebook notebooks/
```

Open any notebook and run all cells. Each notebook is self-contained — it connects to the satellite data API, downloads imagery, processes it, and produces visualizations.

Start with `01_first_multispectral_win.ipynb` and work through in order, or jump to any notebook that interests you.

---

## Example outputs

**Wildfire burn severity classification (Palisades Fire):**
- Compares before/after satellite imagery
- Classifies every pixel from unburned to high severity
- Generates an automated burn severity report

**Flood detection (Brazil 2024):**
- Maps water extent before and during flooding
- Highlights newly inundated areas

**Urban growth tracking (Bangalore):**
- 10 annual snapshots showing year-over-year development
- Quantified urban coverage percentage per year

---

## How it works

Satellite images are not photographs — they are measurements of reflected energy across specific wavelength bands. Different materials (vegetation, water, soil, buildings) reflect light differently.

By combining bands into spectral indices, we can detect things invisible to the human eye:

| Index | Formula | Detects |
|-------|---------|---------|
| **NDVI** | (NIR - Red) / (NIR + Red) | Vegetation health |
| **NDWI** | (Green - NIR) / (Green + NIR) | Water bodies |
| **NDBI** | (SWIR - NIR) / (SWIR + NIR) | Built-up/urban areas |
| **NBR** | (NIR - SWIR2) / (NIR + SWIR2) | Burn severity |

---

## Project structure

```
space-data-lab/
├── README.md
├── requirements.txt
├── notebooks/
│   ├── 01_first_multispectral_win.ipynb
│   ├── 02_seasonal_comparison.ipynb
│   ├── 03_time_series_animation.ipynb
│   ├── 04_cloud_masking.ipynb
│   ├── 05_spectral_indices.ipynb
│   ├── 06_wildfire_analysis.ipynb
│   ├── 07_flood_analysis.ipynb
│   ├── 08_drought_analysis.ipynb
│   ├── 09_urban_expansion.ipynb
│   └── 10_multidecade_urban_growth.ipynb
├── outputs/
│   └── seasonal_animation.gif
└── src/
    └── stac_utils.py
```

---

## Tech stack

| Library | Purpose |
|---------|---------|
| `pystac-client` | Search satellite catalogs via STAC API |
| `planetary-computer` | Sign asset URLs for Microsoft Planetary Computer |
| `odc-stac` | Load STAC items into xarray |
| `xarray` / `numpy` | Multidimensional array processing |
| `matplotlib` | Visualization |

---

## Analyze your own location

Every notebook uses a simple bounding box to define the area of interest. To analyze a different location:

```python
# Change the bbox to your coordinates [min_lon, min_lat, max_lon, max_lat]
bbox = [-118.559, 34.029, -118.472, 34.107]  # Example: Los Angeles
```

Tip: Google Maps gives coordinates as lat, lon — but bbox needs lon, lat order.

---

## Philosophy

This project prioritizes **clarity over cleverness**, **interpretation over performance**, and **understanding over abstraction**.
