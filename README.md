# Agricultural Watershed Hydrology & Runoff Modeling (`pysheds`)

A practical Python geospatial pipeline using **USGS 3DEP Digital Elevation Models (DEMs)**, `pysheds`, `rioxarray`, and the **USDA-NRCS Curve Number (SCS-CN)** method to automate catchment delineation, surface runoff modeling, and stormwater retention evaluation.

---

## 🎯 What This Notebook Does & How to Reuse It

This notebook is a modular script for automating surface hydrology and watershed mapping. You can copy and re-apply this workflow whenever you need to:

* **Delineate a Catchment Area:** Snaps target coordinates (like an outfall or drainage basin) to active stream channels and outlines the upstream contributing hillslope.
* **Set Up NRCS Curve Number (SCS-CN) Calculations:** Assigns spatial Curve Numbers across an area to calculate surface runoff volumes (in Acre-Feet or Cubic Feet) for single design storms or annual rainfall totals.
* **Model Stormwater Retention & Infiltration:** Evaluates surface water volume draining toward a basin or Best Management Practice (BMP) structure.

### Practical Applications
This code can be adapted for two main project types:
1. **Track 2 Ag Order / Management Practice Plans (MPPs):** Calculating runoff volumes and peak flows to size treatment BMPs or verify on-site retention capacity for Regional Water Board compliance.
2. **Managed Aquifer Recharge (MAR) / ReNeM:** Estimating hillslope runoff yields feeding into an infiltration basin to model groundwater recharge volumes and pumping fee rebates.

---

## 🗺️ Visual Model Outputs & Maps

### 1. D8 Flow Accumulation & Stream Network (Log Scale)
Computes flow direction across the regional DEM and applies a logarithmic scale to highlight micro-channels and main drainage pathways.
![Flow Routing](flow_routing.png)

### 2. Automated Catchment Delineation (~150-Acre Bokariza-Drobac Basin)
Snaps target outfall coordinates to active stream channels and outlines the upstream contributing hillslope catchment.
![Watershed Delineation](Watershed_delineation.png)

### 3. Spatial Curve Number (SCS-CN) Raster Distribution
Maps spatial Curve Number values across elevation zones to simulate surface runoff potential and infiltration behavior.
![NRCS Curve Number](NRCS_Curve_Number.png)

---

## 🔬 Hydrologic & Technical Steps

1. **DEM Preparation & Reprojection:**
   * Ingests USGS 1/3 arc-second DEMs, reprojects to local metric coordinates (**UTM Zone 10N / EPSG:26910**), and standardizes pixel resolution to 10 meters.
2. **Hydrologic Routing (`pysheds`):**
   * Pre-processes terrain by filling single-cell pits and flat topography to enforce continuous downslope flow.
   * Calculates D8 flow direction and log-scaled flow accumulation networks.
3. **Automated Catchment Delineation:**
   * Snaps target outfall coordinates to active drainage channels and outlines contributing upstream hillslopes.
4. **SCS-CN Runoff Calculations:**
   * Generates spatial Curve Number (CN) rasters based on elevation, land cover, and soil hydrologic groups.
   * Quantifies runoff volume for single design storms (e.g., 2.5" event) and annual water-year totals (22" median precipitation).

---

## 📊 Data Preparation & Notes

* **Base Elevation Data:** Downloaded as raw USGS 1/3 arc-second DEM tiles from the USGS 3DEP National Map downloader.
* **Spatial Processing (QGIS / GDAL):**
  1. Reprojected from geographic coordinates (EPSG:4269) to local metric grid **UTM Zone 10N (EPSG:26910)**.
  2. Standardized pixel resolution to 10 meters.
  3. Assigned NoData values to empty edge pixels and saved as `pajaro_valley_utm10n.tif`.
* **Note on File Sizes:** The raw regional DEM is kept locally on disk due to GitHub file size limits (~401 MB). The Jupyter notebook handles dynamic spatial cropping (`pajaro_only_dem.tif`) during execution to keep file sizes manageable.

---

## 🛠️ Python Libraries & Tools

* **Language:** Python 3.x
* **Geospatial Libraries:** `pysheds`, `rioxarray`, `rasterio`, `pyproj`, `numpy`, `pandas`, `matplotlib`
* **GIS Interoperability:** QGIS, Google Earth Engine, USGS 3DEP Elevation Data

---

## 📁 Repository Files

* `Pajaro_pysheds2.ipynb` — Primary Jupyter Notebook containing the end-to-end Python script.
* `Pajaro_pysheds_pdf2.pdf` — Full technical project report and executed documentation.
* `flow_routing.png`, `Watershed_delineation.png`, `NRCS_Curve_Number.png` — Rendered map visualizations.
* `README.md` — Repository documentation and technical workflow summary.

---

## 👤 Author & Contact

**Gregory J. Wilson, M.S.**  
*Wilson Hydrologic Consulting*  
Specializing in agricultural water quality compliance, hydrologic modeling, and GIS spatial analytics.

## 🤖 Development & AI Assistance Note

Portions of this repository were developed with the assistance of AI coding and workflow tools (including Gemini and Python automation scripts) to accelerate code scaffolding, data wrangling logic, and README drafting. 

* **Human Verification:** All spatial routines, algorithmic implementations, and calculations (such as SCS-CN runoff equations and GIS flow routing) have been independently reviewed, tested, and validated by the author.
* **Responsibility:** The final architecture, data integrity, and technical accuracy remain solely the responsibility of the project author.
