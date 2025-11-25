# Transformation Steps

## Overview
This document describes the data transformation steps applied at each layer of the data warehouse.

## Bronze Layer (Raw Data)
The Bronze layer contains raw data ingested from Kaggle CSV files without any transformations.

### Ingestion Process
1. Download CSV files from Kaggle
2. Upload to Azure Blob Storage (bronze container)
3. Maintain original file format and structure

### Files Ingested
- olist_customers_dataset.csv
- olist_orders_dataset.csv
- olist_order_items_dataset.csv
- olist_products_dataset.csv
- olist_sellers_dataset.csv
- olist_order_payments_dataset.csv
- olist_order_reviews_dataset.csv
- olist_geolocation_dataset.csv
- product_category_name_translation.csv

## Silver Layer (Cleaned Data)
The Silver layer contains cleaned and validated data.

### Transformation Steps

#### 1. Data Type Conversion
- Convert string dates to datetime format
- Convert numeric strings to appropriate numeric types
- Standardize boolean values

#### 2. Null Handling
- Identify null values in each column
- Apply appropriate null handling strategies:
  - Replace with default values
  - Forward/backward fill
  - Mark as unknown

#### 3. Deduplication
- Remove duplicate records based on primary keys
- Handle conflicting records

#### 4. Data Validation
- Validate referential integrity
- Check value ranges
- Verify data consistency

#### 5. Standardization
- Standardize text fields (uppercase/lowercase)
- Format phone numbers and zip codes
- Normalize special characters

## Gold Layer (Business-Ready Data)
The Gold layer contains aggregated and denormalized data optimized for analytics.

### Fact Tables

#### fact_orders
Aggregated order metrics:
- order_id
- customer_id
- order_date
- total_items
- total_value
- total_freight
- delivery_days
- review_score

#### fact_sales
Daily sales aggregations:
- date
- total_orders
- total_revenue
- total_items
- avg_order_value

### Dimension Tables

#### dim_customers
Customer dimension with:
- customer_id
- customer_city
- customer_state
- customer_region

#### dim_products
Product dimension with:
- product_id
- category_name_english
- product_weight_g
- product_dimensions

#### dim_sellers
Seller dimension with:
- seller_id
- seller_city
- seller_state
- seller_region

#### dim_date
Date dimension with:
- date_id
- date
- day_of_week
- month
- quarter
- year
- is_weekend
- is_holiday

### Calculated Metrics
- Average delivery time by state
- Customer lifetime value
- Seller performance metrics
- Product popularity scores
