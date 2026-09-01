# AstroSage Call Center Performance Analysis – Project README

## 📌 Project Overview
This project performs a comprehensive data-driven analysis of AstroSage's call center operations, using a raw dataset of **28,027 session records** and **35 attributes** (expanded to **62 columns** after cleaning and feature engineering). The analysis focuses on **operational efficiency**, **customer satisfaction (CSAT)**, **agent performance**, and **strategic investment planning** to optimize a **₹1 crore budget**.

The goal was to identify actionable insights, build an executive dashboard, and recommend data-backed investments across **hiring**, **training**, and **technology upgrades**.

---

## 🎯 Objectives
- **Clean and preprocess** inconsistent, missing, and unstructured data.
- **Engineer features** to enable temporal and behavioral analysis.
- **Answer 14 objective questions** (e.g., call volume, CSAT drivers, repeat caller rate).
- **Answer 10 subjective questions** (e.g., investment allocation, risk mitigation, workload balancing).
- **Build an interactive dashboard** with slicers for dynamic filtering.
- **Develop a ₹1 crore investment strategy** with What-IF scenario projections.

---

## 📂 Dataset Description
| Aspect | Details |
|--------|---------|
| **Raw Records** | 28,027 sessions |
| **Original Columns** | 35 (e.g., `_id`, `user`, `chatStatus`, `guruName`, `consultationType`, `amount`, `rating`, etc.) |
| **Cleaned Columns** | 62 (35 original + 19 cleaned + 7 derived) |
| **Time Period** | December 1, 2023 – January 3, 2024 |
| **Platforms** | AstroSage (`app`) and Gurucool (`gurucool`) |
| **Consultation Types** | Call, Chat, Complementary, Public Live Call |

---

## 🛠️ Data Cleaning & Feature Engineering

### Phase 1 – Null/Missing Value Handling
- Context-aware replacements using nested `IF` formulas.
- Example: `chatStatus` missing for call records → replaced with `"Call_Not_Applicable"`.
- Numeric blanks (e.g., `chatSeconds`, `amount`) → replaced with `0`.

### Phase 2 – Guru Name Standardization
- Latest name selected based on `createdAT` per `gid`.
- Variations standardized (e.g., `Dr Balkrisna` → `Astro Dr Balkrisna`).
- Manual conflict resolution using business rules.

### Phase 3 – Feature Engineering (7 new columns)
| Column | Formula / Logic | Purpose |
|--------|----------------|---------|
| `Session_Date` | `=TEXT(createdAT,"yyyy-mm-dd")` | Daily grouping |
| `Session_Month` | `=TEXT(createdAT,"MMMM")` | Monthly trends |
| `Session_Year` | `=TEXT(createdAT,"YYYY")` | Annual filtering |
| `Session_Hour` | `=HOUR(createdAT)` | Time-slot analysis |
| `Time_Slot` | `=IF(Hour<5,"Late Night", IF(Hour<12,"Morning", IF(Hour<17,"Afternoon", IF(Hour<22,"Evening","Night"))))` | Peak period identification |
| `Actual_Duration` | Unified duration for calls/chats | Standardized engagement metric |
| `Repeat_Caller` | `=COUNTIFS(uid, current_uid, createdAT, "<"&current_time) > 0` | Identifies returning users |

### Phase 4 – Data Transfer
- Used `VLOOKUP` with `MATCH` for dynamic column mapping from raw sheet to cleaned sheet.
- Formula: `=VLOOKUP($A2, data!$A$1:$BI$28028, MATCH('Cleaned data'!B$1, data!$A$1:$BI$1, 0), FALSE)`

---

## 📊 Key Analysis & Results

### Objective Questions (14)
| Question | Key Finding |
|----------|-------------|
| **Q1** | Total tables: 1 |
| **Q2** | Total attributes: 35 original → 62 after cleaning |
| **Q3** | Cleaning applied – null handling, standardization, 7 features added |
| **Q4** | Avg daily calls: 250.24; Peak: Dec 10 (430 calls) |
| **Q5** | Highest month: Dec 2023 (8,090 calls); Lowest: Jan 2024 (418 calls) |
| **Q6** | Total Dec operational cost: ₹93,786.16 |
| **Q7** | Avg calls/agent/day: 1.88 (vs industry 40-60) |
| **Q8** | Repeat callers: 56.6% (4,735 of 8,363 calls) |
| **Q9** | Total sales: ₹2,14,065.90 (Call: 78.7%, Chat: 21.3%) |
| **Q10** | Top user: 33832 (113 calls); Top guru: Astro Shalini (1,060 calls) |
| **Q11** | Duration-CSAT correlation: 0.000059 (no relationship) |
| **Q12** | Highest CSAT: Astro Pujaa Rai & Tarot Mystical (7.5/8); Lowest: Tarot Rittika (0.0/8) |
| **Q13** | Avg CSAT: Dec 2.95 → Jan 2.68 |
| **Q14** | Categorical columns: 16 text, 11 numeric, 4 date/time, 5 logical, 6 derived |

### Subjective Questions (10)
| Question | Key Recommendation |
|----------|---------------------|
| **Q1** | Invest 50% Training, 35% Technology, 15% Seasonal Hiring |
| **Q2** | Risks: Over-hiring, training retention, tech dependency → mitigated via pilot programs, phased rollout |
| **Q3** | AstroSage vs Gurucool: Volume (10.97x higher) & Revenue (₹36,626 more) but Gurucool has higher CSAT (4.24 vs 3.50) |
| **Q4** | Peak periods: Morning (44.9% calls) – stagger shifts, dynamic queuing, callback options |
| **Q5** | Prioritize: Reduce repeat calls (AI IVR), fix bottom gurus (training), rebalance workload, replicate Gurucool model |
| **Q6** | Key CSAT drivers: Agent skill (not duration), top performer methods, workload balance, time slot, first-contact resolution |
| **Q7** | Workload: 19 overloaded agents, 5 HIGH RISK → redistribute to 112 balanced agents |
| **Q8** | Technologies: AI IVR, real-time load monitor, post-call follow-up, CSAT prediction analytics, integrated CRM |
| **Q9** | Dashboard KPIs: Total Calls, Revenue, CSAT, Repeat Rate, Agent Load, Platform Comparison |
| **Q10** | ₹1 crore allocation: Training (₹50L), Technology (₹35L), Hiring (₹15L) – projected CSAT 4.0, repeat rate 37%, revenue ₹2.37L |

---

## 📈 Dashboard Design
An **interactive Excel dashboard** was built with:
- **KPI Banner**: 7 critical metrics (Total Calls, Revenue, CSAT, Repeat Rate, etc.)
- **Charts**: Daily trend line, guru performance bars, platform pies, time-slot distribution
- **Slicers**: Region, Month, Consultation Type, Website – all connected to pivot tables
- **Conditional Formatting**: Red/Amber/Green for CSAT thresholds

---

## 🧮 Key Formulas Used
| Function | Purpose | Example |
|----------|---------|---------|
| `COUNTIFS` | Conditional counting | Calls per time slot |
| `AVERAGEIFS` | Conditional averaging | CSAT by platform |
| `CORREL` | Correlation analysis | Duration vs CSAT |
| `VLOOKUP` + `MATCH` | Dynamic data transfer | Raw → Cleaned mapping |
| `IF` / `AND` | Workload classification | Overloaded/Balanced/Underutilized |
| `What-IF Scenario Manager` | Investment projections | CSAT, revenue forecasting |

---

## 📁 Repository Structure
```
AstroSage-Analysis/
├── data/
│   ├── raw_data.xlsx
│   └── cleaned_data.xlsx
├── dashboards/
│   └── call_center_dashboard.xlsx
├── scripts/
│   ├── data_cleaning.R / .py
│   └── analysis_queries.sql
├── reports/
│   ├── objective_answers.md
│   └── subjective_answers.md
├── README.md
└── LICENSE
```

---

## 🚀 How to Reproduce
1. **Clone the repository**
2. **Open the Excel workbook** containing raw data.
3. **Run cleaning scripts** (or use the provided cleaned sheet).
4. **Refresh pivot tables** in the dashboard sheet.
5. **Interact with slicers** to explore different segments.

---

## 📚 Tools & Technologies
- **Microsoft Excel** (Primary tool) – Power Query, PivotTables, Formulas
- **What-IF Analysis** – Scenario Manager
- **Visualization** – Excel charts (line, bar, pie, scatter)
- **Statistical Functions** – CORREL, AVERAGEIFS, COUNTIFS

---

## 👥 Contributors
- **Analyst**: Anusha Shankar
- **Project Duration**: June 2026 - July 2026
- **Domain**: Call Center Analytics / Business Intelligence

---

## 📝 License
This project is for educational and demonstration purposes. Data is anonymized and used with permission.

---

**Key Takeaway:** This project demonstrates how rigorous data cleaning, feature engineering, and statistical analysis can transform raw operational data into actionable business intelligence, directly guiding a ₹1 crore investment strategy with measurable ROI.
