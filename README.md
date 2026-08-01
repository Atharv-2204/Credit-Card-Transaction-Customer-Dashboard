# 💳 Credit Card Transaction & Customer Report — Power BI

A 2-page Power BI dashboard connected live to a PostgreSQL database, analysing credit card transaction patterns and customer profiles — built to demonstrate not just report design, but the full data refresh lifecycle from database to dashboard.

---

## 📊 Dashboard Preview

> *Add screenshots of both pages — Win+Shift+S while the report is open in Power BI Desktop*

![CC Transaction Page](screenshots/01_cc_transaction.png)
![CC Customer Page](screenshots/02_cc_customer.png)

---

## 🎯 Project Objective

To build a live-connected BI reporting solution — not a static, one-time report — that answers two core business questions:
1. **Transaction behavior** — What do spending patterns look like across categories, time, and transaction types?
2. **Customer profile** — Who are the customers behind the transactions, and how do their demographics relate to spending behavior?

A key goal of this project was to go beyond dashboard *design* and understand how BI tools behave in a **real, evolving data environment** — where new records get added to the source database after the report is built, and the dashboard must reflect those changes on demand.

---

## 🗄️ Data Architecture

Unlike a typical Power BI project built on a static CSV import, this dashboard connects **live to a PostgreSQL database**, replicating how BI tools are used in real workplace environments.

### Setup process

1. **Created a dedicated PostgreSQL database** named `ccdb` in pgAdmin 4.
2. **Designed two relational tables** within `ccdb`:
   - `cc_detail` — credit card transaction-level data
   - `cust_detail` — customer profile and demographic data
3. **Imported the source datasets** into these tables using PostgreSQL's Import/Export tool:
   - `credit_card.csv` → loaded into `cc_detail`
   - `customer.csv` → loaded into `cust_detail`
4. **Connected Power BI directly to the PostgreSQL server** (rather than importing a flat file), so the report queries the live database tables `public.cc_detail` and `public.cust_detail` on every refresh.
5. **Built both dashboard pages** — CC Transaction and CC Customer — entirely on this live connection.

### Testing the real-world refresh workflow

To verify the dashboard behaves correctly as source data changes over time — a common real-world requirement — an additional validation step was carried out after the initial dashboard build:

- New transaction and customer records were added directly into the database (`cc_add.csv` and `cust_add.csv`, appended into `cc_detail` and `cust_detail` respectively)
- The Power BI report was refreshed using the **Refresh** button (no rebuild, no re-import)
- The dashboard updated automatically to reflect the newly added records, confirming the live database connection was functioning correctly

This step was intentionally included to build practical understanding of **how BI dashboards behave in production environments**, where source data is continuously updated and reports must stay current without manual rework — a workflow that static CSV-based projects don't demonstrate.

---

## 📁 Report Structure

| Page | Focus | Visual count |
|---|---|---|
| **CC Transaction** | Spend trends over time, transaction category breakdown, top merchants/categories via treemaps | 17 visuals |
| **CC Customer** | Customer demographics, spend-by-customer-segment, geographic and behavioral breakdowns | 18 visuals |

---

## 🛠️ Power BI Skills Demonstrated

| Skill | Where it's used |
|---|---|
| Live database connectivity | Direct PostgreSQL server connection (not flat-file import) |
| Data refresh workflow | Verified end-to-end: new DB records → Power BI Refresh → updated visuals |
| Combo charts | Line + stacked column for transaction trend analysis |
| Treemaps | Hierarchical breakdown of spend/customer categories (7 total across both pages) |
| Card visuals & KPIs | Key summary metrics on both pages |
| Slicers | Interactive filtering across transaction and customer views |
| Table visuals | Detailed transaction and customer-level views |
| Relational data modeling | Two related tables (`cc_detail`, `cust_detail`) modeled and joined within Power BI |

---

## 🚀 How to Reproduce This Project

1. Install **PostgreSQL** and **pgAdmin 4**
2. Create a database named `ccdb`
3. Create two tables: `cc_detail` and `cust_detail`
4. Import `credit_card.csv` into `cc_detail` and `customer.csv` into `cust_detail` via pgAdmin's Import/Export tool
5. Open **Power BI Desktop** → Get Data → PostgreSQL database → connect to `ccdb`
6. Open `Credit_Card_Report.pbix` (included in this repo) and set the data source credentials to point to your local `ccdb` instance
7. Click **Refresh** to pull live data

---

## 💡 What I Learned

- How to connect Power BI directly to a PostgreSQL database rather than relying on static file imports — a fundamentally different (and more production-realistic) workflow.
- The practical difference between building a dashboard once versus maintaining one — by deliberately adding new data to the source tables after the initial build and confirming the Refresh mechanism correctly pulled it through.
- How treemaps can effectively communicate hierarchical spend and customer segmentation data where standard bar charts would be less intuitive.
- The importance of designing a relational data model (`cc_detail` and `cust_detail` as separate, related tables) rather than flattening everything into a single wide table — mirroring how real transactional systems are structured.

---

## 🙋 About

Built by **[Your Name]** as part of a data analyst portfolio project.

- 🔗 LinkedIn: [your-linkedin-url]
- 📧 Email: your@email.com

---

*If you found this useful, please ⭐ star the repository!*
