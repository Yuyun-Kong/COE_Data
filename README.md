# COE Data Pipeline and Car Recommendation Project

## Overview
This project develops a data pipeline and analytical system to assist car buyers in Singapore in selecting suitable vehicles based on Certificate of Entitlement (COE) premiums and carbon emission bands. By consolidating historical COE bidding data (2010-2025) with a curated car reference list categorized by carbon emission bands, this system provides actionable car model recommendations aligned with user preferences for emissions and COE categories. It also highlights historically favorable quarters and months to make cost-effective purchases.

## Problem Statement
Car buyers often face difficulty manually analyzing extensive COE premium datasets and matching them with vehicle emission categories to make informed purchasing decisions. This project addresses these challenges by automating data extraction, transformation, and integration to offer clear car recommendations and timing insights based on historical trends.

## Features
- Extraction and transformation of historical COE data using API and PDF scraping
- Integration of COE bidding results with Carbon Emissions-based Vehicle Scheme (CEVS) band data
- Star schema relational database design in PostgreSQL for efficient querying and reporting
- Comprehensive data validation, cleaning, and aggregation workflows
- Analytical insights identifying low COE premium periods and low emission vehicle options
- Overcoming challenges such as slow scraping runtimes, inconsistent PDF formatting, and incomplete data

## Data Sources
- **COE Bidding Results Dataset:** Historical records of COE bidding exercises from Jan 2010 to Aug 2025 via official government API
- **CEVS Revised Bands PDF:** Emission band classifications for car models in Singapore scraped from NCCS PDF documentation

## Methodology
### ETL Process
- **API-based Extraction:** 
  - Securely fetch JSON data using Python requests and dotenv for credentials management
  - Normalize nested JSON to tabular form via `pandas.json_normalize`
  - Filter relevant vehicle categories (A, B, and E) and convert data types for consistency
- **PDF Scraping:** 
  - Parse CEVS PDF using `pdfplumber` with regex-based text processing to extract emission bands and car models
  - Clean and validate extracted data, handling missing or corrupted entries
- **Data Loading:** 
  - Create dimension and fact tables following star schema best practices
  - Load transformed data into PostgreSQL with `psycopg2` and SQLAlchemy
- **Database Schema:** 
  - Fact table `fact_coe_monthly` aggregates monthly COE bidding results
  - Dimension tables for date, category, car reference, and emission bands enable detailed querying

### Analytical Queries
- Identify COE categories with the lowest historical premiums
- List low carbon emission vehicle models within COE categories
- Determine quarters and months with favorable COE premiums for bidding
- Analyze seasonal fluctuations and demand-to-supply ratios across years

## Technology Stack
- Python (pandas, requests, pdfplumber, regex, dotenv, psycopg2, SQLAlchemy)
- PostgreSQL database with star schema design
- Jupyter Notebook for ETL execution and analysis

## Usage
1. Clone this repository.
2. Ensure Python 3.x and PostgreSQL are installed.
3. Install required Python libraries (pandas, requests, pdfplumber, etc.).
4. Configure environment variables for API access keys in a `.env` file.
5. Run the Jupyter notebook `COE Data Pipeline Source code.ipynb` to:
   - Extract and clean COE bidding data and car emission data
   - Load processed data into PostgreSQL database
   - Execute SQL queries for car recommendations and COE premium analysis
6. Query the database or extend analyses as needed.

## Challenges & Solutions
- **Long scraping runtime:** Switched from dynamic web scraping to efficient PDF scraping, reducing data extraction time from ~25 minutes to ~15 seconds.
- **Incomplete data in PDF:** Applied data validation and supplemented missing data from reputable external sources.
- **Irregular PDF formatting:** Developed regex parsing rules and cleaning steps to reliably segment car models, emission bands, and categories.

## Limitations
- Car model reference list is non-exhaustive (77 models).
- COE premium recommendations are based on historical data and do not reflect real-time prices.
- User preferences, financing, and detailed car specifications are outside the scope of this project.

## Future Work
- Expand the car reference dataset and include more vehicle features and user customization.
- Automate data pipeline scheduling with cron or Apache Airflow.
- Migrate infrastructure to cloud platforms for scalability (AWS, GCP, Azure).
- Develop interactive dashboards using Tableau, Power BI, or Streamlit.


```python

```
