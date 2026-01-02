# Space Data Lab

*A curiosity-driven introduction to analyzing data from space*

---

## Why this project exists

This repository is a **learning-first, low-pressure exploration** into analyzing data collected by satellites.

I started this project with:
- strong Python + data science skills
- **no prior background** in remote sensing, planetary science, or satellite imagery

The goal is **not** to rush toward machine learning or advanced models, but to:
> Understand what satellite images *actually represent* and how physical measurements become data we can analyze.

This repo documents that journey from first principles.

---

## Core idea (the mental model)

Satellite images are **not photographs**.

They are:
- measurements of **reflected or emitted energy**
- captured across **specific wavelength bands**
- stored as **numbers per pixel**

Different materials (vegetation, water, soil, buildings) interact with light differently.
By understanding *how* they absorb and reflect energy, we can infer surface properties and changes over time.

---

## What I've learned so far

### Notebook 01: First Multispectral Win
**Loading and visualizing satellite data for the first time**

- Connected to Microsoft Planetary Computer's STAC API
- Loaded Sentinel-2 imagery (Blue, Green, Red, NIR bands)
- Created true color (RGB) composites — what humans would see from space
- Computed **NDVI** (Normalized Difference Vegetation Index)

**Key insight:** NDVI = (NIR - Red) / (NIR + Red) reveals vegetation health invisible to the human eye. Healthy plants absorb red light for photosynthesis but strongly reflect near-infrared.

### Notebook 02: Seasonal Comparison
**Comparing summer vs winter imagery**

- Loaded the same location in July 2024 and January 2024
- Compared true color and NDVI side-by-side
- Created difference maps showing where vegetation changed most

**Key insight:** Agricultural fields show dramatic seasonal swings (NDVI 0.1 → 0.6), while urban areas and evergreen forests stay relatively stable year-round.

### Notebook 03: Time Series Animation
**Watching a full year of vegetation change**

- Loaded one image per month for all of 2024
- Created a time series graph showing the seasonal "pulse"
- Built an animated visualization cycling through the year
- Exported as a shareable GIF

**Key insight:** Vegetation follows a predictable seasonal cycle — dormant in winter, green-up in spring, peak in summer, senescence in fall. This pattern is the foundation for crop monitoring, drought detection, and climate studies.

---

## Repository structure

```
space-data-lab/
├── README.md
├── requirements.txt
│
├── notebooks/
│   ├── 01_first_multispectral_win.ipynb   # Load data, RGB, NDVI basics
│   ├── 02_seasonal_comparison.ipynb        # Summer vs winter comparison
│   └── 03_time_series_animation.ipynb      # Full year animation
│
├── outputs/
│   └── seasonal_animation.gif              # Exported animation
│
└── src/
    └── stac_utils.py                       # (Future) reusable helpers
```

---

## Tools & libraries used

| Library | Purpose |
|---------|---------|
| `pystac-client` | Search satellite catalogs via STAC API |
| `planetary-computer` | Sign secure asset URLs for Microsoft's data |
| `odc-stac` | Load STAC items directly into xarray |
| `xarray` | Labeled multi-dimensional arrays |
| `numpy` | Numerical operations |
| `matplotlib` | Visualization and animation |

---

## Key concepts learned

### Spectral Bands
Satellites don't see "colors" — they measure light intensity in specific wavelength ranges:

| Band | Wavelength | What it reveals |
|------|------------|-----------------|
| Blue (B02) | 490 nm | Water, atmosphere |
| Green (B03) | 560 nm | Vegetation vigor |
| Red (B04) | 665 nm | Chlorophyll absorption |
| NIR (B08) | 842 nm | Vegetation structure |

### NDVI (Normalized Difference Vegetation Index)
```
NDVI = (NIR - Red) / (NIR + Red)
```
- **0.6 to 1.0** — Dense, healthy vegetation
- **0.2 to 0.6** — Sparse or stressed vegetation
- **0.0 to 0.2** — Bare soil, rocks
- **-1.0 to 0.0** — Water, snow, clouds

### Bounding Box Format
```python
bbox = [min_longitude, min_latitude, max_longitude, max_latitude]
```
Note: Google Maps gives lat/lon, but bbox needs lon/lat order!

---

## Next possible directions

- [ ] Explore other spectral indices (NDWI for water, NDBI for urban areas)
- [ ] Apply cloud masking using QA bands
- [ ] Compare a drought year to a normal year
- [ ] Detect fire scars or flood impacts
- [ ] Apply the same workflow to Mars orbital data

---

## Why Earth data first?

Earth observation is used here as a **training ground**, not the final destination.

The same principles apply to:
- Mars orbiters
- lunar missions
- asteroid spectroscopy

Earth data is well-documented, forgiving, and rich in visual feedback. Once the intuition is built here, transitioning to planetary datasets becomes far more natural.

---

## Philosophy

This repository prioritizes:
- **clarity over cleverness**
- **interpretation over performance**
- **understanding over abstraction**

Any additions should preserve that philosophy.
