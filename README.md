# Overture Data Extraction Script for Propeterra

This is a script that extracts building data from Overture in a GeoJSON format for Propeterra

# Description & Importance

This is a Python and SQL script that extracts building data larger that 30m that fit a certain class of buildings from the Overture data provider for world buildings.

This Script was created using two strategies one fully tested strategy (gathering Overture data using Duckdb by utilizing divisions to split the data by countries) and one partially tested strategy (gathering Overture data by chunking)

# How it's Made

Coding Languages/Libraries: Python, SQL, DuckDB, GeoPandas, os 

Data Types Supported: GeoJSON, Parquet, other forms of spatial data such as shapefiles or geopackages should work

Projection Used: EPSG:4326 WGS 84

Data Layers used: 

Divisions Area Layer (Administrative Boundaries)

    s3://overturemaps-us-west-2/release/2025-06-25.0/theme=divisions/type=division_area/*.parquet

Buildings Layer

    s3://overturemaps-us-west-2/release/2025-06-25.0/theme=buildings/type=building/*.parquet

# Gathering data through DuckDB script (Fully Tested):

Time to run: 13.9 hours

Utilizes the Divisions Area Layer to clip each building to their corresponding countries by using a bounding box without specifically giving the output layer a country code field

Looped through a dictionary of country codes (two-letter ISO 3166-1 standard) with their corresponding country names to extract data for each target country.

# Gathering Data through Chunking (Partially tested):

Estimated time to run: 8-12+ hours at least

## Step 1:

Downloads GeoJSON data of buildings into 10 by 10 degree chunks (Could speed up the process by using the Parquet data format)

The Chunking process is run 4 times for each hemisphere (NE, NW, SE, SW)

## Step 2:

Spatial Join the Divisions Area Layer with each building chunk

The Spatial Join process is run 4 times for each hemisphere (NE, NW, SE, SW)

## Step 3: 

Select buildings by their country code and export data using a dictionary of country codes (two-letter ISO 3166-1 standard) with their corresponding country names

# Known Issues

Gathering Data through Chunking is only partially tested on a small subset.

Script may have issues with relative paths

Will need to create output directories/folders before running
