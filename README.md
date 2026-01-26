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

### Notebook 04: Cloud Masking
**Dealing with the biggest challenge in optical remote sensing**

- Used Sentinel-2's Scene Classification Layer (SCL) to identify clouds
- Applied masks to remove cloudy pixels from analysis
- Learned that ~67% of Earth is covered by clouds at any given time

**Key insight:** Quality satellite analysis requires filtering out clouds, shadows, and other atmospheric interference. The SCL band classifies each pixel into categories (vegetation, water, cloud, shadow, etc.).

### Notebook 05: Spectral Indices Beyond NDVI
**Expanding the toolkit**

- **NDWI** (Normalized Difference Water Index): Detects water bodies
- **NDBI** (Normalized Difference Built-up Index): Highlights urban areas
- **NBR** (Normalized Burn Ratio): Assesses fire damage

**Key insight:** The formula pattern `(Band_A - Band_B) / (Band_A + Band_B)` can be adapted to detect almost anything — just choose bands where your target reflects differently than its surroundings.

### Notebook 06: Wildfire Burn Severity (Palisades Fire)
**From "it looks burned" to "exactly how burned"**

- Analyzed the January 2025 Palisades Fire in Los Angeles
- Computed NBR before and after the fire
- Created dNBR (differenced NBR) to quantify burn severity
- Classified damage into actionable categories (unburned → high severity)

**Key insight:** True color shows "burned or not burned." Spectral indices reveal a *gradient* of severity — critical for emergency response, erosion control, and recovery planning.

### Notebook 07: Flood Detection (Brazil 2024)
**Mapping inundated areas with NDWI**

- Analyzed the May 2024 floods in Rio Grande do Sul, Brazil
- Used NDWI to distinguish water from land
- Compared normal conditions vs flood conditions
- Classified water extent changes

**Key insight:** Water strongly absorbs NIR while reflecting green light. NDWI exploits this to map water bodies and detect flooding, even when floodwater is muddy.

### Notebook 08: Drought Analysis (California)
**Detecting vegetation stress across years**

- Compared California's Central Valley: 2019 (normal) vs 2021 (drought)
- Same location, same season, different water years
- Classified vegetation stress levels from satellite data

**Key insight:** Drought isn't just "less rain" — it shows up as reduced NDVI across entire regions. Satellites can detect agricultural stress before it's visible on the ground.

### Notebook 09: Urban Expansion (NDBI)
**Watching cities grow**

- Used NDBI to map built-up areas in Ahmedabad, India
- Compared 2016 vs 2024 to see urban expansion
- Classified land into urban/non-urban categories

**Key insight:** Built-up areas reflect SWIR strongly and NIR weakly (opposite of vegetation). NDBI quantifies urbanization and can track city growth over time.

### Notebook 10: Multi-Decade Urban Growth (Landsat)
**30 years of change from space**

- Switched from Sentinel-2 (2015+) to Landsat (1984+) for historical data
- Analyzed Denver, Colorado across 1995, 2005, 2015, and 2024
- Handled different Landsat missions (5/7 vs 8/9) with different band numbering
- Created a 30-year urban growth visualization

**Key insight:** Sentinel-2 only goes back to 2015. For multi-decade analysis, Landsat provides 40+ years of consistent Earth observation data — though at coarser resolution (30m vs 10m).

---

## Repository structure

```
space-data-lab/
├── README.md
├── requirements.txt
│
├── notebooks/
│   ├── 01_first_multispectral_win.ipynb   # Load data, RGB, NDVI basics
│   ├── 02_seasonal_comparison.ipynb       # Summer vs winter comparison
│   ├── 03_time_series_animation.ipynb     # Full year animation
│   ├── 04_cloud_masking.ipynb             # Handling clouds in imagery
│   ├── 05_spectral_indices.ipynb          # NDWI, NDBI, NBR indices
│   ├── 06_wildfire_analysis.ipynb         # Palisades Fire burn severity
│   ├── 07_flood_analysis.ipynb            # Brazil flood detection
│   ├── 08_drought_analysis.ipynb          # California drought comparison
│   ├── 09_urban_expansion.ipynb           # NDBI urban growth (Sentinel-2)
│   └── 10_multidecade_urban_growth.ipynb  # 30-year Landsat analysis
│
├── outputs/
│   └── seasonal_animation.gif             # Exported animation
│
└── src/
    └── stac_utils.py                      # (Future) reusable helpers
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

### Spectral Indices
All follow the same pattern: `(Band_A - Band_B) / (Band_A + Band_B)`

| Index | Formula | What it detects |
|-------|---------|-----------------|
| **NDVI** | (NIR - Red) / (NIR + Red) | Vegetation health |
| **NDWI** | (Green - NIR) / (Green + NIR) | Water bodies |
| **NDBI** | (SWIR - NIR) / (SWIR + NIR) | Built-up/urban areas |
| **NBR** | (NIR - SWIR2) / (NIR + SWIR2) | Burn severity |

### NDVI Interpretation
- **0.6 to 1.0** — Dense, healthy vegetation
- **0.2 to 0.6** — Sparse or stressed vegetation
- **0.0 to 0.2** — Bare soil, rocks
- **-1.0 to 0.0** — Water, snow, clouds

### Satellite Missions Used

| Mission | Available | Resolution | Best for |
|---------|-----------|------------|----------|
| Sentinel-2 | 2015–present | 10m | Recent, detailed analysis |
| Landsat 8/9 | 2013–present | 30m | Recent historical |
| Landsat 5/7 | 1984–2013 | 30m | Multi-decade studies |

### Bounding Box Format
```python
bbox = [min_longitude, min_latitude, max_longitude, max_latitude]
```
Note: Google Maps gives lat/lon, but bbox needs lon/lat order!

---

## What's been covered

- [x] Explore other spectral indices (NDWI for water, NDBI for urban areas)
- [x] Apply cloud masking using QA bands
- [x] Compare a drought year to a normal year
- [x] Detect fire scars (Palisades Fire burn severity)
- [x] Detect flood impacts (Brazil 2024)
- [x] Multi-decade analysis using Landsat

## Next possible directions

- [ ] Apply the same workflow to Mars orbital data (HiRISE, CRISM)
- [ ] Explore radar data (SAR) for cloud-penetrating analysis
- [ ] Time series anomaly detection for early warning systems
- [ ] Machine learning classification of land cover types
- [ ] Combine multiple indices for composite analysis

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
