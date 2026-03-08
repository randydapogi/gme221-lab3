# GmE 221 – Laboratory Exercise 3

## Overview

This laboratory extends Laboratory 2 from planar (2D) spatial analysis to true three-dimensional computational modeling.

Unlike simple extrusion, this exercise constructs LineString geometries whose coordinates include a Z value (x, y, z). Z is derived by sampling elevation values from a DEM raster.

---

## Environment Setup

- Python 3.x
- PostgreSQL with PostGIS
- geopandas rasterio shapely numpy pyproj sqlalchemy psycopg2-binary flask flask-cors

## How to Run

1. Activate the virtual environment
2. Run `python analysis.py`

---

## Outputs

---

## Reflection

### Interpreting Hybrid IO

1. Why are roads retrieved from PostGIS instead of file?

- Storing the roads vector data in a PostGIS database has the advantage of having the data indexed geospatially for better performance in querying the data. It also serves to store data in a centralized location.

2. Why is the DEM loaded directly from a raster file?

- Since raster files tend to be much larger than vector files the general approach for handling raster files is to store raster as a file and store the raster metadata and file path in a database for cataloging.

3. How does hybrid IO reflect real-world GIS architecture?

- Real-world GIS architecture retrieves spatial datasets from different sources. Streaming data from different sources and applying computations and manipulations of those data are the modern way of working with GIS applications.

4. Is spatial analysis occurring at this stage?

- At this stage, we are not yet performing spatial analysis. We are only reading data and information from the source. We have not yet generated new data, insight or analysis from the input datasets.
