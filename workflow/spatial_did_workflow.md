## Step 1: Create Buffers Around BRT Stops

- Tool: Buffer
- Distances: 500m, 1km, 2km
- Dissolve: ALL
- Output: buffer_500m.shp, etc.

## Step 2: Calculate Population Served
- Tool: Zonal Statistics
- Input zones: TAZ polygons intersected with buffer
- Input raster: WorldPop 2019
- Output: Mean population served per TAZ
