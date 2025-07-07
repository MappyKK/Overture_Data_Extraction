# Overture Data Extraction Script for Propeterra

This is a script that extracts building data from Overture in a GeoJSON format for Propeterra

# Description & Importance

This is a Python and SQL script that extracts building data larger that 30m that fit a certain class of buildings from the Overture data provider for world buildings.

This Script was created using two strategies one fully tested strategy (gathering Overture data using Duckdb by utilizing divisions to split the data by countries) and one partially tested strategy (gathering Overture data by chunking)

# How it's Made

Coding Languages/Libraries: Python, SQL, DuckDB, GeoPandas, os 

Data Types Supported: GeoJSON, Parquet, other forms of spatial data such as shapefiles or geopackages should work

Projection Used: EPSG:4326 WGS 84



# Known Issues
