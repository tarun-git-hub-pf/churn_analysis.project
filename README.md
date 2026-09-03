# customer-churn-analysis
SQL + Python pipeline for customer churn analysis data extraction, cleaning, feature engineering, and visualization using SQLite and pandas.

## Overview

This project extracts customer, subscription, and support data from a SQLite database, cleans and merges it into a single dataset, engineers a churn flag from cancellation records, and analyzes churn patterns using key business metrics and visualizations.

## Tools Used

- **Python**: pandas, numpy
- **Database**: SQLite (via `sqlite3`)
- **Visualization**: Matplotlib, Seaborn

## Data Source

The dataset is stored in a SQLite database (`customer_churn.db`) with three tables:
- `db_customer` - customer demographic and contact information
- `db_subscription` - subscription plan, contract type, billing, and cancellation details
- `db_support` - customer complaints, escalations, and satisfaction scores

## What This Project Does

**1. Data Extraction**
Connects to the SQLite database, dynamically reads all tables, and loads each into a separate pandas DataFrame.

**2. Data Cleaning**
- Renamed and standardized column names
- Dropped irrelevant columns (e.g. interests, pincode)
- Converted date columns to proper datetime format
- Standardized inconsistent categorical values (e.g. gender labels)
- Filled missing country values using a state-to-country mapping derived from existing records
- Removed duplicate support records per customer, keeping the most recent complaint

**3. Feature Engineering**
- Created a binary `churn_flag` based on whether a cancellation date exists
- Merged customer, subscription, and support tables into a single analysis-ready dataset
- Bucketed customers into churn risk categories (Low / Medium / High) based on churn score
- Calculated customer tenure in days (from subscription start to cancellation or current date)

**4. Business Metrics Calculated**
- Overall churn rate and retention rate
- Churn rate by subscription plan type
- Average Revenue Per User (ARPU)
- Average customer tenure
- Revenue at risk from churned customers
- Escalation rate
- Average complaints per user
- Correlation between escalations and churn

**5. Data Visualization**
- Monthly churn trend (line chart)
- Churn rate by plan type (bar chart)
- Churn rate by state (bar chart)
- Churn rate by gender (bar chart)
- Correlation heatmap across encoded features
- Pairplot for feature relationships
- Multi-dimensional comparison (plan type vs. monthly charges, split by gender and churn risk)
- Pivot tables summarizing churn and revenue by plan type

## Files in This Repository

- `Churn_analysis.ipynb` - main analysis notebook
- `customer_churn.db` - SQLite database used as the data source
- `exported_churn_data.csv` — cleaned and merged dataset exported from the notebook

## How to Run

1. Clone this repository
2. Install dependencies:
