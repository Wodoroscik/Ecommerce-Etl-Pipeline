# Ecommerce-Etl-Pipeline
Automated ETL &amp; reporting pipeline for e-commerce. Built with n8n, PostgreSQL, SQL, and Google Sheets API.

## About the Project
An automated ETL pipeline developed for an e-commerce business to streamline sales reporting. The project replaces manual spreadsheet operations with a scheduled n8n workflow that extracts order data, models it in a relational database, and automatically generates formatted business reports.

*(Note: The codebase has been anonymized. Sensitive data and credentials have been replaced with generic placeholders).*

## Tech Stack
* **Orchestration:** n8n
* **Database:** PostgreSQL
* **Data Transformation:** SQL (CTEs, JOINs, Aggregations)
* **Scripting:** JavaScript (Data parsing, API payload construction)
* **Integrations:** REST APIs (WooCommerce, Google Sheets, Live Currency Exchange)

## Architecture & Technical Details
<img width="1877" height="708" alt="Screen Automated_Sales_Reporting_Pipeline" src="https://github.com/user-attachments/assets/2266122d-82f9-445d-9f1f-99296b60e80f" />
The pipeline is designed with data integrity and automated reporting in mind:

* **Idempotent Data Ingestion:** The daily sync (`WooCommerce_to_Postgres_ETL`) relies on strict `UPSERT` logic using unique Order IDs to prevent data duplication upon workflow re-triggers.## Files in this repo
* `Automated_Sales_Reporting_Pipeline.json` - The main reporting flow (Extracts from Postgres, processes via JS/SQL, pushes to Google Sheets).
* `WooCommerce_to_Postgres_ETL.json` - The daily data ingestion flow (WooCommerce to Postgres).
* `Manual_Order_Reprocessing_Tool.json` - A small internal tool I built for the Customer Support team to manually re-sync specific orders if needed.
* **In-Database Transformations:** Data modeling and KPI calculations (e.g., "New vs. Returning Customers", "Sales by Rep") are pushed down to PostgreSQL rather than being processed in-memory.
* **API-Driven Formatting:** The pipeline uses JavaScript to construct `batchUpdate` requests for the Google Sheets API, automating cell merging, conditional formatting, and data presentation.
* **Dynamic Currency Conversion:** Integrates real-time EUR/PLN exchange rates to accurately segment customers into predefined tiers (Corporate, Key Account, Growth, Select).

## Project Outcomes
* **Process Automation:** Eliminated approximately 4 hours per week of manual data extraction and spreadsheet formatting.
* **Data Reliability:** Reduced manual entry errors in financial reporting by implementing strict SQL modeling and automated UPSERT logic.
* **Reporting Latency:** Shifted from end-of-month manual reporting to on-demand, automated dashboards.
<img width="1920" height="824" alt="Google Sheets Dashboard" src="https://github.com/user-attachments/assets/0e7fc2c5-527c-423b-ba9c-0b4cbe70b2b8" />

## Repository Contents
* `Automated_Sales_Reporting_Pipeline.json` - Core reporting flow (Postgres extraction, JS/SQL processing, Google Sheets API push).
* `WooCommerce_to_Postgres_ETL.json` - Daily data ingestion workflow (WooCommerce to Postgres).
* `Manual_Order_Reprocessing_Tool.json` - An internal utility flow for customer support to manually re-sync specific records.
