# BRT_DID_Treated_Control_Areas_ArcGIS

# Spatial DiD Analysis of the Rea Vaya BRT System

This repository contains the spatial analysis workflow used to assess the population served by the Rea Vaya BRT system in Johannesburg using a Difference-in-Differences (DiD) framework.

## Repository Structure

- `workflow/` – Step-by-step documentation of ArcGIS processes (e.g. buffer classification, treatment assignment)
- `scripts/` – Python scripts for calculating percent population served and assigning treatment
- `maps/` – Final visualizations exported from ArcGIS
- `data_samples/` – Lightweight sample data (TAZ, buffers, population) for reproducibility

## Tools Used
- ArcGIS Pro 3.x
- Python 3 (ArcPy)
- WorldPop raster population data
