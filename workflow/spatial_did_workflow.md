# Spatial Difference-in-Differences (DiD) Workflow: Traeted and control Areas, Population Served Rea Vaya BRT Impact Analysis
This workflow describes the spatial analysis process used to evaluate the impact of the Rea Vaya Bus Rapid Transit (BRT) system on Johannesburg residents using a Difference-in-Differences (DiD) framework. The method involves spatial classification of treatment and control areas based on BRT stop buffers and population served, using ArcGIS and supplementary scripts.

## Step 1: Prepare Input Data
Required Datasets:
BRT stop locations (Phases 1A and 1B)
Transport Analysis Zones (TAZ) shapefile
WorldPop population raster (2000, 2014, 2019)
Household Travel Surveys (HTS) – 2000, 2014, 2019

Tools Used:
ArcGIS Pro 3.x
Spatial Analyst Extension
Python (ArcPy or standalone scripts)

## Step 2: Create Buffer Zones Around BRT Stops
Create 3 buffer layers around each BRT stop:

Buffer Size	Purpose
500 meters	Direct walk access zone
1 km	Moderate walk access zone
2 km	Extended access zone

ArcGIS Tool:
- Tool: Buffer (Analysis Tools > Proximity > Buffer)
- Parameters:
- Input: BRT stop shapefile
- Distance: 500m, 1000m, 2000m
- Dissolve: ALL
- Output: buffer_500m.shp, etc.




