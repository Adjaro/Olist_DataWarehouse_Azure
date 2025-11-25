# Data Catalog

## Overview
This document describes the data sources and schemas used in the Olist Data Warehouse project.

## Source Data (Kaggle Dataset)

### olist_customers_dataset
Customer information table.

| Column | Type | Description |
|--------|------|-------------|
| customer_id | string | Unique customer identifier |
| customer_unique_id | string | Unique identifier for customer across orders |
| customer_zip_code_prefix | string | First 5 digits of customer zip code |
| customer_city | string | Customer city name |
| customer_state | string | Customer state abbreviation |

### olist_orders_dataset
Order information table.

| Column | Type | Description |
|--------|------|-------------|
| order_id | string | Unique order identifier |
| customer_id | string | Reference to customer |
| order_status | string | Order status (delivered, shipped, etc.) |
| order_purchase_timestamp | datetime | Purchase timestamp |
| order_approved_at | datetime | Payment approval timestamp |
| order_delivered_carrier_date | datetime | Carrier delivery date |
| order_delivered_customer_date | datetime | Customer delivery date |
| order_estimated_delivery_date | datetime | Estimated delivery date |

### olist_order_items_dataset
Order items information table.

| Column | Type | Description |
|--------|------|-------------|
| order_id | string | Reference to order |
| order_item_id | int | Sequential item number in order |
| product_id | string | Reference to product |
| seller_id | string | Reference to seller |
| shipping_limit_date | datetime | Shipping deadline |
| price | float | Item price |
| freight_value | float | Freight cost |

### olist_products_dataset
Product information table.

| Column | Type | Description |
|--------|------|-------------|
| product_id | string | Unique product identifier |
| product_category_name | string | Product category (Portuguese) |
| product_name_length | int | Product name length |
| product_description_length | int | Product description length |
| product_photos_qty | int | Number of product photos |
| product_weight_g | int | Product weight in grams |
| product_length_cm | int | Product length in cm |
| product_height_cm | int | Product height in cm |
| product_width_cm | int | Product width in cm |

### olist_sellers_dataset
Seller information table.

| Column | Type | Description |
|--------|------|-------------|
| seller_id | string | Unique seller identifier |
| seller_zip_code_prefix | string | First 5 digits of seller zip code |
| seller_city | string | Seller city name |
| seller_state | string | Seller state abbreviation |

### olist_order_payments_dataset
Payment information table.

| Column | Type | Description |
|--------|------|-------------|
| order_id | string | Reference to order |
| payment_sequential | int | Sequential payment number |
| payment_type | string | Payment method |
| payment_installments | int | Number of installments |
| payment_value | float | Payment value |

### olist_order_reviews_dataset
Order reviews table.

| Column | Type | Description |
|--------|------|-------------|
| review_id | string | Unique review identifier |
| order_id | string | Reference to order |
| review_score | int | Rating from 1 to 5 |
| review_comment_title | string | Review title |
| review_comment_message | string | Review text |
| review_creation_date | datetime | Review creation date |
| review_answer_timestamp | datetime | Review answer timestamp |

### olist_geolocation_dataset
Geolocation information table.

| Column | Type | Description |
|--------|------|-------------|
| geolocation_zip_code_prefix | string | First 5 digits of zip code |
| geolocation_lat | float | Latitude |
| geolocation_lng | float | Longitude |
| geolocation_city | string | City name |
| geolocation_state | string | State abbreviation |

### product_category_name_translation
Product category translation table.

| Column | Type | Description |
|--------|------|-------------|
| product_category_name | string | Category name in Portuguese |
| product_category_name_english | string | Category name in English |

## Data Layers

### Bronze Layer
Raw data ingested from CSV files without transformations.

### Silver Layer
Cleaned and validated data with:
- Data type corrections
- Null handling
- Deduplication
- Basic transformations

### Gold Layer
Aggregated and business-ready data for analytics:
- Fact tables
- Dimension tables
- Calculated metrics
