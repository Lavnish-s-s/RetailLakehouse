# RetailLakehouse

A data engineering project implementing a medallion architecture for e-commerce data processing and analytics.

## Overview

This project builds a data lakehouse for retail/e-commerce data, transforming raw CSV data through bronze, silver, and gold layers to create clean, aggregated datasets suitable for analytics and dashboards.

## Architecture

The project follows the medallion architecture:

- **Bronze Layer**: Raw data ingestion and basic validation
- **Silver Layer**: Data cleansing, deduplication, and standardization
- **Gold Layer**: Business-ready aggregates and denormalized tables for reporting

## Data Pipeline

The pipeline processes raw CSV files through medallion layers in a series of notebooks:

1. **Ingest (Bronze)**
   - Read raw CSVs from `0_data/ecomm-raw-data/` (landing zone)
   - Store raw records in a persistent bronze layer (e.g., Delta Lake tables)
   - Apply basic schema enforcement and validation checks

2. **Clean & Standardize (Silver)**
   - Deduplicate and clean data (e.g., fix data types, handle missing values)
   - Join/enrich dimension tables (brands, categories, products, customers, dates)
   - Produce a standardized, query-ready dataset

3. **Aggregate & Serve (Gold)**
   - Build business-ready tables (facts + aggregates) for analytics and dashboards
   - Create denormalized tables for reporting use cases (e.g., sales by product/category)

Notebooks in `1_codes/project_ecommerce/` run the pipeline steps in the recommended order.

## Data Sources

The raw data includes:
- Brands
- Categories
- Customers
- Dates
- Order items (daily CSV files from 2025-08-01 to 2025-09-16+)
- Products

## Project Structure

```
0_data/
├── ecomm-raw-data/
│   ├── brands/
│   ├── category/
│   ├── customers/
│   ├── date/
│   ├── order_items/landing/  # Daily order item files
│   └── products/

1_codes/
└── project_ecommerce/
    ├── 1_setup/
    │   └── setup_catalog.ipynb  # Initial setup and catalog creation
    ├── 2_medallion_processing_dim/
    │   ├── 1_dim_bronze.ipynb   # Dimension bronze processing
    │   ├── 2_dim_silver.ipynb   # Dimension silver processing
    │   └── 3_dim_gold.ipynb     # Dimension gold processing
    └── 3_medallion_processing_fact/
        ├── 1_fact_bronze.ipynb  # Fact bronze processing
        ├── 2_fact_silver.ipynb  # Fact silver processing
        └── 3_fact_gold.ipynb    # Fact gold processing

2_genie_exploration/
└── questions.txt  # Exploration questions for data analysis

3_dashboard/
└── denormalise_table_query.txt  # Queries for dashboard denormalized tables

resources/  # Additional resources
```

## Technologies

- Python
- AWS S3
- DataBricks
- Pyspark 
- Data lakehouse principles

## Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/Lavnish-s-s/RetailLakehouse.git
   cd RetailLakehouse
   ```

2. Install dependencies (if any):
   ```bash
   pip install -r requirements.txt  # Create if needed
   ```

3. Run the setup notebook:
   - Open `1_codes/project_ecommerce/1_setup/setup_catalog.ipynb`
   - Execute cells to initialize the catalog and environment

## Usage

1. **Data Ingestion**: Run bronze layer notebooks to ingest raw data
2. **Data Processing**: Execute silver layer notebooks for cleansing
3. **Aggregation**: Run gold layer notebooks for final aggregates
4. **Exploration**: Refer to `2_genie_exploration/questions.txt` for analysis ideas
5. **Dashboard**: Use queries in `3_dashboard/denormalise_table_query.txt` for reporting

Execute notebooks in order:
- Dimensions: Bronze → Silver → Gold
- Facts: Bronze → Silver → Gold

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make changes and test
4. Submit a pull request

## Contact
**GitHub:** (https://github.com/Lavnish-s-s)  
**LinkedIn:** https://www.linkedin.com/in/lavnish-suvarna-8389081a7