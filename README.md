# 🛡️ KYC & AML Compliance Analytics Dashboard

An end-to-end Power BI project that simulates a real-world **Know Your Customer (KYC)** and **Anti-Money Laundering (AML)** compliance monitoring system for a financial institution — covering customer onboarding risk, transaction monitoring, and AML case investigation.

---

## 📌 Project Overview

Financial institutions are legally required to monitor customers and transactions for money-laundering risk. This project builds a **compliance analytics dashboard** that brings together three core data domains:

- **Customer KYC profiles** (risk category, PEP status, onboarding/review dates)
- **Transaction monitoring** (amount, channel, beneficiary country, risk score, alerts)
- **AML case management** (investigations, SAR filings, case priority, outcomes)

The goal is to give a Compliance/AML team a single-pane-of-glass view of customer risk exposure, suspicious transaction activity, and investigation pipeline health — supporting faster regulatory decision-making.

---

## 🔄 End-to-End Workflow

```
Raw Data (Excel, 3 sheets, 1000 rows each)
        │
        ▼
Data Cleaning & Preparation (Power Query)
        │
        ▼
Data Modeling (Star Schema in Power BI)
        │
        ▼
DAX Measures & Calculated Columns
        │
        ▼
Exploratory Data Analysis (EDA)
        │
        ▼
Power BI Dashboard Design (2 report pages)
        │
        ▼
Insights, Validation & Documentation
```

1. **Collect** raw KYC, transaction, and AML case data
2. **Clean** and standardize each table in Power Query
3. **Model** relationships between Customers → Transactions → Cases
4. **Build measures** (counts, sums, % splits) using DAX
5. **Explore** the data to identify risk and alert patterns
6. **Visualize** findings in an interactive Power BI dashboard
7. **Document** findings, insights, and recommendations

---

## 🗂️ Data Source

The dataset is a synthetic/simulated KYC-AML dataset containing **3 related tables**, ~1,000 records each: 

| Sheet | Records | Description |
|---|---|---|
| `Customer_KYC` | 1,000 | Customer master data — onboarding, KYC status, risk rating, PEP flag |
| `Transaction_Monitoring` | 1,000 | Transaction-level data — amount, channel, country, risk score, alerts |
| `AML_Cases` | 1,000 | Case-level AML investigation data — alert type, status, SAR filing, outcome |

**Key fields by table:**

- **Customer_KYC:** `Customer_ID`, `Customer_Name`, `Country`, `Customer_Type`, `Risk_Category`, `KYC_Status`, `PEP_Status`, `Occupation`, `Annual_Income`, `Onboarding_Date`, `Last_KYC_Review_Date`
- **Transaction_Monitoring:** `Transaction_ID`, `Customer_ID`, `Transaction_Date`, `Amount`, `Currency`, `Transaction_Type`, `Transaction_Channel`, `Beneficiary_Country`, `Risk_Score`, `Alert_Flag`, `Alert_Status`
- **AML_Cases:** `Case_ID`, `Alert_ID`, `Customer_ID`, `Case_Open_Date`, `Alert_Type`, `Investigation_Status`, `SAR_Filed`, `Investigator_Name`, `Case_Priority`, `Resolution_Time_Days`, `Regulatory_Action`, `Case_Outcome`

`Customer_ID` is the common key linking all three tables.

---

## 🧹 Data Cleaning & Data Preparation

Performed using **Power Query Editor** in Power BI:

- Verified and corrected column data types (dates, numbers, text, currency)
- Removed duplicate `Customer_ID` / `Transaction_ID` / `Case_ID` entries
- Standardized categorical text values (e.g., trimming whitespace, consistent casing in `Risk_Category`, `KYC_Status`)
- Handled blanks/nulls in `PEP_Status`, `SAR_Filed`, `Alert_Flag`
- Converted date columns (`Onboarding_Date`, `Transaction_Date`, `Case_Open_Date`) to proper date format for time-intelligence
- Created relationships between tables on `Customer_ID` (one-to-many: Customer → Transactions, Customer → Cases)
- Added calculated columns where needed (e.g., Year/Month from date fields)
- Renamed columns/tables for clarity and consistent naming convention

- <img width="1918" height="977" alt="Screenshot 2026-06-21 110803" src="https://github.com/user-attachments/assets/d235efcb-baf3-42a5-9795-7b632789344b" />

---

## 🔍 Exploratory Data Analysis (EDA)

Initial analysis (in Excel/Power Query) before dashboard build, to understand:

- Distribution of customers across `Risk_Category` (Low / Medium / High)
- Proportion of **PEP vs Non-PEP** customers
- KYC status breakdown (Pending / Completed / Expired)
- Transaction volume and value by `Transaction_Type` and `Beneficiary_Country`
- Alert frequency by `Alert_Type` (Structuring, Sanctions Match, High Value Transaction, Unusual Activity)
- AML investigation status spread (Open / Under Review / Closed)
- Case priority distribution (Low / Medium / High)
- Correlation between high-risk customers and SAR filings

---

## 📊 Power BI Dashboard

Built as a **2-page interactive report** with a dark, glass-panel themed UI and global slicers for filtering.

### Page 1 — KYC & AML Compliance Overview
- KPI cards: Total Customers, High Risk Customers, Total Transactions, Open AML Cases, Suspicious Transactions, Pending KYC, Completed KYC, SAR Filed
- Slicers: `Country`, `Risk_Category`, `KYC_Status`, `Case_Priority`, `Transaction_Type`
- Customer Risk Distribution (bar chart)
- Country-wise Transactions (horizontal bar chart)
- PEP vs Non-PEP Customers (donut chart)
- Transaction Amount by Type (column chart)
- Sum of Amount by Year (line chart)
- KYC Compliance Status — Pending / Expired / Completed (donut chart)

### Page 2 — AML Investigation & Alerts
- AML Investigation Status (Closed / Under Review / Open) — donut chart
- High Priority Cases by `Case_Priority` (bar chart)
- Alert Type Distribution — Unusual Activity, High Value Transaction, Sanctions Match, Structuring (column chart)

**Interactivity:** cross-filtering slicers, drill-through-ready visuals, tooltips, and KPI cards that respond dynamically to filter selections.

---

## 🔑 Key Insights

- A large share of customers fall into the **Low risk category**, but a significant minority are flagged **High Risk**, requiring enhanced due diligence
- **PEP customers** make up close to half of the customer base (~45.8%), indicating a need for stronger enhanced due diligence (EDD) processes
- **KYC compliance gaps** exist — a notable portion of records are still `Pending` or `Expired`, posing regulatory risk
- **UAE, USA, and UK** are the top beneficiary countries by transaction value, suggesting concentrated cross-border monitoring needs
- Nearly **55% of AML cases remain open or under review**, indicating investigation backlog/throughput risk
- **Structuring** and **Unusual Activity** are the most common alert types, consistent with typical money-laundering typologies
- Case priority is fairly evenly split across Low/Medium/High, suggesting triage rules may need refinement to better surface true high-risk cases

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Microsoft Excel** | Raw data storage, initial structuring |
| **Power Query (M Language)** | Data cleaning, transformation, shaping |
| **Power BI Desktop** | Data modeling, DAX measures, dashboard design |
| **DAX** | KPI calculations, % splits, time intelligence |
| **Power BI Service** *(optional)* | Publishing & sharing the report |

---

## 📁 Repository Structure

```
KYC-AML-Compliance-Analytics/
│
├── README.md
│
├── 01_Raw_Data/
│   └── KYC_AML_Compliance_Analytics_1000Rows.xlsx
│
├── 02_Cleaned_Data/
│   ├── Customer_KYC_Cleaned.xlsx
│   ├── Transaction_Monitoring_Cleaned.xlsx
│   └── AML_Cases_Cleaned.xlsx
│
├── 03_PowerBI_File/
│   └── KYC_AML_Compliance_Analytics.pbix
│
├── 04_Dashboard_Preview/
│   ├── Dashboard_Page1_Overview.png
│   └── Dashboard_Page2_AML_Investigation.png
│
└── 05_Documentation/
    └── Project_Summary.pdf
```

---

## 📑 Excel Structuring

The source workbook is organized into **3 normalized sheets** acting as fact/dimension-style tables:

- `Customer_KYC` → Customer dimension (1 row per customer)
- `Transaction_Monitoring` → Transaction fact table (many rows per customer)
- `AML_Cases` → AML case fact table (many rows per customer)

All three are joined via the shared `Customer_ID` key, enabling a clean **star-schema-style model** in Power BI.

---

## 📥 Raw / Converted Data

- Original raw data provided as a single file with 3 sheets, ~1,000 rows per sheet
  
 <img width="1912" height="936" alt="Screenshot 2026-06-21 154813" src="https://github.com/user-attachments/assets/af095cbb-75bc-4bd2-a31a-dd5f557894af" />

  
- No external conversion was required; data was Excel-native and imported directly into Power Query

- <img width="1918" height="977" alt="Screenshot 2026-06-21 110803" src="https://github.com/user-attachments/assets/d235efcb-baf3-42a5-9795-7b632789344b" />


- Data types (dates, currency, categorical text) were converted/standardized inside Power Query rather than in the source file, to preserve the original raw extract

---

## ✅ Structured & Cleaned Data

After cleaning, all 3 tables were:
- Type-cast correctly (dates as Date, Amount/Income as Decimal Number, IDs as Text)
- Free of duplicate keys
- Standardized in category labels (Risk_Category, KYC_Status, Alert_Type, etc.)
- Linked via relationships in the Power BI data model

- 

---

## 📈 Power BI

- Built using **Power BI Desktop**
- Data model: Star schema with `Customer_KYC` as the central dimension table
- DAX measures created for all KPI cards, percentage breakdowns, and dynamic slicer-driven totals
- Custom dark theme with hexagon-pattern background panels for a SOC/compliance-style aesthetic
- Two report pages, fully cross-filterable via top slicer bar

---

## 🖼️ Dashboard Preview

**Page 1 — KYC & AML Compliance Analytics Overview**
> KPI cards, customer risk distribution, country-wise transactions, PEP split, transaction amount by type, yearly trend, KYC compliance status

<img width="962" height="543" alt="Screenshot 2026-06-21 152502" src="https://github.com/user-attachments/assets/781a9764-8ac4-4c6d-a9b9-6b9ed582d861" />



**Page 2 — AML Investigation & Alerts**
> AML investigation status, high priority cases, alert type distribution

<img width="952" height="547" alt="Screenshot 2026-06-21 152523" src="https://github.com/user-attachments/assets/60f22852-6c4e-42dd-868d-61ac34e18108" />


---

## ⭐ Project Highlights

- Simulates a realistic **regulatory compliance analytics use case** (KYC/AML) relevant to banking, fintech, and financial-crime risk roles
- Demonstrates **end-to-end BI workflow**: raw data → cleaning → modeling → DAX → dashboard → insights
- Multi-table relational data model (3 linked tables) instead of a single flat file
- Dashboard designed with **UX/visual storytelling** in mind (KPI hierarchy, color-coded risk indicators, intuitive slicers)
- Insights are framed around **actionable compliance decisions**, not just chart description

---

## 🚀 Future Enhancements

- Add **drill-through pages** for individual customer or case-level investigation views
- Incorporate **time-intelligence trend analysis** (month-over-month alert volume, YoY risk migration)
- Add **predictive risk scoring** using historical case outcomes (ML integration)
- Build **row-level security (RLS)** so investigators only see assigned cases
- Automate **data refresh** via Power BI Service / scheduled gateway
- Add a **SAR filing turnaround time** metric and SLA breach tracking
- Integrate **sanctions list screening** results as an additional data source

---

## ⚠️ Disclaimer

This project uses **synthetic/simulated data** generated for educational and portfolio purposes only. It does **not** represent real customers, real financial institutions, or real AML case data. The dashboard is not intended for, and must not be used in, actual regulatory compliance, AML investigation, or financial decision-making.

---

## 📄 License

This project is released under the **MIT License**. You are free to use, modify, and distribute this project with attribution, provided it is not used to make claims about real financial institutions or individuals.

---

## 👤 Author

**[J Sai Abhinay]**

KYC Analyst | Data Analyst | Power BI 

📧 Email: jsaiabhinay51@gmail.com

🔗 LinkedIn: https://www.linkedin.com/in/jujare-sai-abhinay-71a2b1363/ 


---
