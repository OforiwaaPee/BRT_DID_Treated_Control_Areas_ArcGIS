# Spatial Difference-in-Differences (DiD) Workflow: Traeted and control Areas, Population Served Rea Vaya BRT Impact Analysis

This workflow describes the spatial analysis process used to evaluate the impact of the Rea Vaya Bus Rapid Transit (BRT) system on Johannesburg residents using a spatial Difference-in-Differences (DiD) framework. The method involves spatial classification of treatment and control areas based on BRT stop buffers and population served, using ArcGIS and supplementary Python scripts.

---

## Step 1: Prepare Input Data

### Required Datasets:
- BRT stop locations (Phases 1A and 1B)
- Transport Analysis Zones (TAZ) shapefile
- WorldPop population raster (2000, 2014, 2019)
- Household Travel Surveys (HTS) – 2000, 2014, 2019

### Tools Used:
- ArcGIS Pro 3.x
- Spatial Analyst Extension
- Python (ArcPy or standalone scripts)

---

## Step 2: Create Buffer Zones Around BRT Stops

Create 3 buffer layers around each BRT stop:

| Buffer Size | Purpose |
|-------------|---------|
| 500 meters  | Direct walk access zone |
| 1 km        | Moderate walk access zone |
| 2 km        | Extended access zone |

### ArcGIS Tool:
- Tool: **Buffer (Analysis Tools > Proximity > Buffer)**
- Input: BRT stop shapefile
- Distance: `500m`, `1000m`, `2000m`
- Dissolve: **ALL**
- Output: `buffer_500m.shp`, `buffer_1km.shp`, `buffer_2km.shp`

---

## Step 3: Calculate % of TAZ Population Within Each Buffer

### Steps:

1. **Intersect Buffers with TAZs**
   - Tool: **Intersect**
   - Inputs: Buffer shapefile and TAZ shapefile
   - Output: `Buffer_TAZ_Intersect.shp`

2. **Extract Population Within Buffers**
   - Tool: **Extract by Mask**
   - Input Raster: WorldPop for corresponding year
   - Mask: Each buffer zone
   - Output: Population raster within buffer

3. **Summarize Population by TAZ**
   - Tool: **Zonal Statistics as Table**
   - Zone Data: TAZs intersected with buffer
   - Value Raster: Extracted WorldPop
   - Statistic: **SUM**

4. **Join Population Tables**
   - Join extracted population back to TAZ attribute table

5. **Calculate % Population Served**
   - New Field: `pop_pct = (pop_buffer / pop_total) * 100`

---

## Step 4: Classify Treatment and Control Areas

### Classification Logic:
- **Treated**: TAZs with ≥50% of population served by a buffer
- **Control**: TAZs with ≤25% of population served
- **Partial/Excluded**: TAZs between 25% and 50%

### ArcGIS Tools:
Use **Field Calculator** or Python (`arcpy.CalculateField`) with an expression like:
*Python*

def classify(pct):
    if pct >= 50:
        return "Treated"
    elif pct <= 25:
        return "Control"
    else:
        return "Partial"

---

## **Step 5: Tag Year and BRT Phase**

Add two fields to your classified table:

- `Year`: 2000, 2014, or 2019
- `BRT_Phase_Exposure`:  
  - `2000`: Pre-BRT  
  - `2014`: Post-Phase 1A  
  - `2019`: Post-Phase 1B  

This supports a **staggered DiD framework**, where treatment varies over time and space.

---

## Step 6: Export Final Classification Table

Export a clean summary table at the TAZ level. It should include:

- `TAZ_ID`
- `Year`
- `BRT_Phase_Exposure`
- `Percent_Pop_Served`
- `Treatment_Status` (Treated / Control / Partial)

You’ll later join this table with your Household Travel Survey (HTS) microdata to construct a panel.

---

## Step 7: Link with HTS Microdata

Join the classified TAZ table to HTS datasets:

- Merge on `TAZ_ID` (or equivalent spatial field)
- Attach `Treatment_Status` and `BRT_Phase_Exposure` to each HTS observation (household, person, or trip level)
- Prepare a **long-format panel** for statistical DiD analysis

This step is often done in Python, R, or Stata depending on your modeling environment.

---

## Step 8: Create Final Maps and Visualizations

Using ArcGIS:

- Map buffer zones and overlaid TAZs
- Show **Treated vs Control areas** by year and phase
- Visualize percent population served

Export your maps as `.png` or `.pdf` and place them in a `maps/` folder in your GitHub repo.

---

## References

- **WorldPop Population Data**: [https://www.worldpop.org/](https://www.worldpop.org/)
- **ArcGIS Pro Tools**: [https://pro.arcgis.com/](https://pro.arcgis.com/)
- **Difference-in-Differences Methodology**: Urban Economics and Transport Geography literature

---
