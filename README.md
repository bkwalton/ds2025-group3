# Introduction
Group 3 project work for the final of ECON 6295 Data Science

Ayse Battal
Brad Kwalton
David (Zacchaeus) Taylor
Kathleen Hinman

# Project Overview
This project forecasts the 5- and 10-year house price appreciation in Orlando, FL neighborhoods using economic, demographic, and geographic data. The system is designed to support investment decisions by identifying high-ROI neighborhoods through VAR modeling.

# System Architecture
The pipeline consists of:
- Data ingestion from Zillow, ACS, and Google Maps API
- SQL-based database for structured storage
- Google Colab notebooks for data prep, modeling, and visualization
- Forecasting model using Vector Auto Regression (VAR) and Prophet Model
- Output reports in the form of tables, charts, and maps

# Notebook Descriptions
## definition.ipynb
- Purpose: Collects and defines initial data inputs, builds neighborhood boundaries, and initializes the database schema using DDL.
- Inputs: 
  - Zillow housing price data (CSV)
  - ACS/Census data via Census API
  - Orlando neighborhood GeoJSON
  - Census tract shapefiles
  - SQL DDL schema (ddl.txt)
- Outputs: 
  - Structured spatial and tabular datasets
  - Initialized database (orlando.db)

## model.ipynb
- Purpose: Trains and evaluates the forecast models (VAR and Prophet) on housing price data and economic variables, and generates 10-year forecasts by neighborhood.
- Inputs: 
  - SQL model queries (var.txt, prophet.txt)
  - orlando.db for historical data
- Outputs:
  - Forecasted home price data frames by neighborhood and year
  - Sorted ROI rankings for neighborhoods (2022–2030)

## update.ipynb
- Purpose: Provides functionality for updating the database with new price data and appending to existing tables using SQL DML.
- Inputs: SQL update script (update.txt)
- Outputs: Updated database rows for new time periods or new entries

# SQL Scripts
- DDL.txt: Creates database schema (tables for home prices, income, unemployment, geographies)
- DML.txt: Populates and updates database with clean data
- update.txt: Script to append or modify values in the existing tables
- var.txt / prophet.txt: SQL logic for selecting model training data

# Setup Instructions
- Run notebooks in Google Colab
- Required Python libraries: pandas, numpy, geopandas, matplotlib, statsmodels, census, us, sqlite3, dotenv
- Configure .env file with:
  - CENSUS_API key
  - Google Maps API key (if needed for distance features)
- Initialize database schema by running definition.ipynb

# Execution Instructions
Run Order:
- definition.ipynb
- model.ipynb
- update.ipynb

# Maintenance Guide
- Refresh Zillow and ACS data manually
- Update the database using update.ipynb
- Rerun forecasting notebook to update ROI projections

# Monitoring:
- Check for forecast drift (comparing predicted vs. actual for known years)
- Validate data completeness before rerunning models

# Known Issues
- Missing neighborhood-level data in some ACS and Zillow datasets
- Google Maps API requires billing setup
- Income/shooting data inconsistencies across years may reduce reliability in smaller tracts
