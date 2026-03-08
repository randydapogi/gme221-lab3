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

### 3D Elevation Sampling and LINESTRINGZ Construction

1. Why densification is necessary?

- Densification is necessary to increase the resolution of elevation data when reconstructing the road segments with elevation data. Without densification the resolution of the elevation data of the road segments will just be dependent on the vertices of the road segments which are typically few and far between. With Densification we can control the resolution of sampling the elevation data to a fixed distance interval.

2. Why CRS alignment must happen before sampling

- We need to make sure that the CRS of the road segments and the DEM file aligns before sampling so that the elevation data that we collect for the point in our road segment is the exact elevation data that is stored in the DEM.

3. What it means that geometry now contains Z values (not symbolic extrusion)

- Having Z value in a geospatial data geometry means that we can map the spatial data not only in relation to the latitude and logitude of the earth but also in relation to its height from the sea level.

### Export 3D GeoJSON

1. What is preserved when you export 3D geometry to GeoJSON?

- When we exported the 3D geometry to GeoJSON the geometry data with Z axis is preserved.

2. What is lost or not formally expressed?

- The CRS information of the geometry is lost.

3. Why does GeoJSON still label the geometry as "LineString" even when Z exists? What does this tell you about the difference between data content and data standard?

- GeoJSON format was designed to render spatial data to web browsers with the required field for coordinates being the latitude and longitude with elevation being an optional field. This tells us that spatial data can be represented in different data contents or format from the standards set in OGR.

4. How does this affect visualization in QGIS 3D View? Does QGIS treat this as true 3D geometry or as 2.5D visualization?

- Since GeoJSON only contains x,y,z of the geometry, QGIS treats the geojson of roads as a 2.5D visualization rather than a 3D geometry.

5. If you had to preserve 3D semantics more explicitly, what alternative output formats would you consider?

- Storing the roads_3d_gdf dataframe to a PostGIS database, a Shapefile or a GeoPackage would have stored the CRS information of the roads data.
