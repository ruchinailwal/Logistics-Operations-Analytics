# 📦 Logistics Operations Analytics

An end-to-end analytics project focused on analyzing logistics operations, shipment performance, customer activity, and payment trends using **PostgreSQL, SQL, Excel, Power BI, and n8n**.

## Overview

Raw operational data is loaded into a **7-table PostgreSQL database**, transformed using SQL ETL, analyzed through Excel/Google Sheets, and visualized through a **3-page Power BI dashboard**. n8n workflows automate daily reporting and on-demand shipment/payment explanations using the Groq API.

## Tech Stack

**PostgreSQL · SQL · Excel · Google Sheets · Power BI · n8n · Groq API · Postman**

## Project Workflow

Raw CSV Data → PostgreSQL Database → SQL ETL & Transformation → Excel / Google Sheets EDA → Power BI Dashboard → n8n Automation + Groq API

## Database

### Core Tables

- `customer`
- `membership`
- `employee_details`
- `employee_manages_shipment`
- `shipment_details`
- `status`
- `payment_details`

### Derived Tables

- `shipmentstatus`
- `customerpayments`

## Excel / Google Sheets Analysis

Performed exploratory data analysis and KPI analysis covering:

- Payment modes and categories
- Shipment efficiency
- Delivery time
- Shipment weight
- Customer type
- Customer domain
- Membership performance

📊 **[View Excel / Google Sheets Analysis](https://docs.google.com/spreadsheets/d/1SF0s1mAmYPPLwHUs2NigRV_lPJDhJ1t1zH6xUJvnexA/edit?usp=sharing)**

## Power BI Dashboard

The 3-page report covers:

- **Customer Insights** — customer and membership performance
- **Shipment Overview** — delivery rate, weight, efficiency, and service performance
- **Financial Health Monitor** — revenue, payments, pending amounts, and payment modes

## n8n Automation

### Automated Daily Logistics Summary

PostgreSQL → Groq API → Automated Email Report

### Shipment & Payment Explanation

Webhook → PostgreSQL → Groq API → Plain-English Response

## Key Insights

- **50% delivery rate** — 100 of 200 shipments delivered
- **₹9.49M total revenue**, with approximately **₹5M in pending payments**
- **54.5% domestic** and **45.5% international** shipments
- Express shipments had a higher average weight than regular shipments (**569 vs. 473**)
- **9% of memberships were active** (18 active), while **91% were expired** (182 expired)

## Repository Structure

- `dataset/` — Raw source CSV files
- `sql_etl/` — PostgreSQL ETL scripts
- `excel/` — Excel / Google Sheets analysis
- `powerbi_dashboard/` — Power BI report and exports
- `n8n_automation/` — n8n workflow JSON files
- `README.md` — Project documentation
