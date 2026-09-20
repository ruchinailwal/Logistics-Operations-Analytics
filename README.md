# 📦 Logistics Operations Analytics

An end-to-end **analytics and automation** project on logistics operations data — combining a PostgreSQL database, SQL-based ETL, Excel exploratory analysis, an interactive **Power BI dashboard**, and **n8n workflow automation** to deliver actionable insights and automated reporting for logistics teams.

---

## 📌 Project Overview

Logistics operations generate constant streams of shipment, customer, and payment data. This project builds a complete pipeline — from raw CSVs to a governed database, to business-ready dashboards, to automated daily reports and delay alerts — to help operations and finance teams understand delivery performance, revenue collection, and where bottlenecks occur. The goal is to equip logistics teams with **data-driven visibility** into fulfillment and cash flow, backed by automation that surfaces issues without manual digging.

- **Project Type:** End-to-end Analytics + Automation
- **Contribution:** Individual
- **Tools Used:** PostgreSQL, SQL, Excel (PivotTables), Power BI, n8n, Postman

---

## 🗂️ Repository Structure

```
Logistics-Operations-Analytics/
│
├── dataset/                 # Source CSV files (customer, shipment, payment, employee, membership)
├── sql_etl/                 # SQL schema, ETL, and transformation scripts
├── powerbi_dashboard/       # Power BI dashboard file (.pbix)
├── n8n_automation/          # Automated reporting & issue-alert workflows
└── README.md
```

📄 **Excel Analysis Sheet:** [View on Google Sheets](https://docs.google.com/spreadsheets/d/1SF0s1mAmYPPLwHUs2NigRV_lPJDhJ1t1zH6xUJvnexA/edit?usp=sharing)

---

## 🗄️ Dataset Overview

Seven related datasets were combined into a relational PostgreSQL schema:

| Dataset | Description |
|---|---|
| **Customer** | Customer name, email, type, address, contact, membership reference |
| **Membership** | Membership start/end dates per customer |
| **Employee_Details** | Employee name, designation, branch, contact |
| **Shipment_Details** | Shipment content, domain, service type, weight, charges |
| **Status** | Current delivery status, sent date, delivery date |
| **Payment_Details** | Payment amount, mode, status, and date |
| **employee_manages_shipment** | Mapping of employees to the shipments they manage |

Total volume: **200 shipments**, **200 customers**, and their associated payments and delivery records.

---

## 🧹 Data Cleaning & Transformation (ETL)

- **Extract:** Bulk-loaded all 7 CSVs into PostgreSQL via `COPY`, validated row counts and previewed samples.
- **Standardize:** Proper-cased customer names, lowercased email addresses.
- **Enrich:** Derived `CustomerAge` from membership start date; added `PaymentCategory` (`High` / `Medium` / `Low`) based on amount thresholds; added `ShipmentEfficiency` as the weight-to-charge ratio.
- **Join & Load:** Merged shipment and status data into a `ShipmentStatus` table, and customer and payment data into a final `CustomerPayments` table, exported for Excel/Power BI use.

---

## 🔍 Exploratory Data Analysis & Key Insights

Analysis covered delivery performance, shipment characteristics, and payment behavior across customer segments, service types, and shipment domains.

### Shipment & Delivery Insights
- Overall delivery rate stands at **50%**, with 100 of 200 shipments still undelivered.
- **International shipments deliver at a higher rate (~56%)** than **domestic shipments (~46%)**, pointing to bottlenecks at the domestic hub rather than cross-border handling.
- Average shipment weight is **~522 units**, with Express and Regular service types showing distinct weight and efficiency profiles.
- Shipment volume is fairly evenly spread across content categories (Electronics, Automotive, Healthcare, Construction, etc.), with no single category dominating.

### Customer & Financial Insights
- Customer base splits roughly into **Retail (39%), Internal Goods (34%), and Wholesale (27%)**.
- Average membership duration is close to **11 years** across all customer types.
- Total payments received amount to **₹5M**, with a near-even **51% Paid vs. 49% Not Paid** split — indicating close to half of invoiced revenue is still outstanding.
- **100 payments remain pending**, averaging **₹47.45K** per payment, which is likely to affect cash flow and procurement timelines.
- Undelivered shipments frequently correlate with unresolved (not-paid) transactions, suggesting payment status may be gating dispatch or delivery in some cases.

---

## 📈 Power BI Dashboard

An interactive three-page dashboard was built to present findings in a business-friendly format:

**Page 1 — Customer Insights**
- Total Customers: **200** | Avg. Membership Duration: **10.98 yrs** | Total Payments Received: **₹5M**
- Visuals: Average Membership Duration by Customer Type, Membership Growth Over Time, Customer Type Distribution, Top 5 Customers by Payment Amount

**Page 2 — Shipment Overview**
- Total Shipments: **200** | Delivery Rate: **50%** | Avg. Shipment Weight: **522.02**
- Visuals: Shipments by Domain and Delivery Status, Average Shipment Weight by Service Type, Shipments by Content Type, Shipment Efficiency by Domain and Service Type

**Page 3 — Financial Health Monitor**
- Total Payments Received: **₹5M** | Pending Payments: **100** | Pending Amount: **₹5M** | Avg. Payment: **₹47.45K**
- Visuals: Monthly Payment Trend, Payment Amount by Status, Payment Amount by Customer Type, Payment Amount by Payment Mode, Payment Status by Customer Type

---

## 🤖 Workflow Automation (n8n)

- **Automated Daily Logistics Operations Summary** — runs on a schedule, queries PostgreSQL for the day's operational metrics, summarizes them via an LLM, and emails a formatted daily report (shipment counts, delivery rate, charges, pending payments, and observations) to the operations team.
- **Shipment and Payment Issue Explanation Automation** — an on-demand webhook (tested via Postman) that accepts a shipment ID, retrieves its status and payment details from PostgreSQL, and returns a plain-language explanation of why a shipment or payment is delayed.

---

## 💡 Business Recommendations

1. **Fix Domestic Bottlenecks** — Investigate hub congestion and processing delays driving the lower domestic delivery rate.
2. **Tighten Payment Collection** — With nearly half of payments outstanding, prioritize follow-up on high-value pending invoices to protect cash flow.
3. **Link Payment and Dispatch Workflows** — Where payment status is gating delivery, formalize a process to flag and resolve stuck shipments faster.
4. **Use Automation for Early Warning** — Extend the n8n issue-explanation workflow into proactive alerts so delays are caught before they escalate.
5. **Segment Strategy by Customer Type** — Tailor retention and collection efforts by customer type (Retail, Wholesale, Internal Goods) given their differing payment and membership patterns.

---

## ✅ Conclusion

This project turns raw logistics data into a governed database, a clear analytical narrative, and an automated reporting layer. By combining SQL-driven ETL, Excel/Power BI analysis, and n8n automation, it surfaces where delivery performance lags, where revenue is at risk, and how the two are connected — giving logistics and finance teams a foundation for faster, more informed operational decisions.
