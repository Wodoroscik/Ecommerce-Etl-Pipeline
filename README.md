# Ecommerce-Etl-Pipeline
Automated ETL &amp; reporting pipeline for e-commerce. Built with n8n, PostgreSQL, SQL, and Google Sheets API.

## What is this?
This is a real-world ETL pipeline I built to automate sales reporting for an e-commerce business. It completely replaces hours of manual Excel data crunching with an automated flow that pulls order data, models it in a database, and generates ready-to-read business reports.

*(Note: The code in this repository has been fully anonymized. Sensitive data, real product names, and credentials have been replaced with generic placeholders due to NDA).*

## The Tech Stack
* **n8n** - Workflow automation and orchestration
* **PostgreSQL** - Central database for storing and querying data
* **SQL** - Doing the heavy lifting for data transformation (CTEs, JOINs, aggregations)
* **JavaScript** - Data parsing and building Google Sheets API payloads
* **REST APIs** - WooCommerce, Google Sheets, Live Currency Exchange

## How it works under the hood
I focused on building a reliable system rather than just moving raw data from point A to B. Here is what makes it tick:

* **Smart Database Loading (No Duplicates):** The daily sync (`WooCommerce_to_Postgres_ETL`) uses strict `UPSERT` logic based on unique Order IDs. If a workflow triggers twice, it updates existing records instead of duplicating them.
* **SQL does the heavy lifting:** Instead of filtering data in-memory within n8n, the pipeline uses PostgreSQL to calculate business KPIs (e.g., "New vs. Returning Customers", "Sales by Rep").
* **Dynamic Spreadsheet Formatting:** The pipeline doesn't just dump raw data into a sheet. It uses JavaScript to send `batchUpdate` requests to the Google Sheets API—automatically merging cells, applying custom colors, and formatting currencies so the business team gets a finished, styled product.
* **Live Currency Conversion:** It pulls real-time EUR/PLN exchange rates to segment customers into tiers (Corporate, Key Account, Growth, Select) based on their actual value.

## Files in this repo
* `Automated_Sales_Reporting_Pipeline.json` - The main reporting flow (Extracts from Postgres, processes via JS/SQL, pushes to Google Sheets).
* `WooCommerce_to_Postgres_ETL.json` - The daily data ingestion flow (WooCommerce to Postgres).
* `Manual_Order_Reprocessing_Tool.json` - A small internal tool I built for the Customer Support team to manually re-sync specific orders if needed.
