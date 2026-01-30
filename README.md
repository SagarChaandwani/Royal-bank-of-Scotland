# 🏦 Royal Bank of Scotland (RBS): Credit Risk & Digital Churn Engine

Tech Stack	Architecture	Domain
![alt text](https://img.shields.io/badge/Power_BI-Pro-yellow?style=flat-square)
![alt text](https://img.shields.io/badge/SQL-Server-red?style=flat-square)
![alt text](https://img.shields.io/badge/DAX-Advanced-green?style=flat-square)

Star Schema / Snowflake	Banking & FinTech

> **Professional Context:** This portfolio project demonstrates a Risk Intelligence architecture designed during my tenure as a Data Analyst at **Ascentiq Solutions**.
>
> *Note: While the data modeling, DAX logic, and strategic framework mirror real-world banking implementations delivered for the Royal Bank of Scotland (RBS), the underlying dataset used in this public repository is synthetic to comply with GDPR and NDA regulations.*

# 🏦 Royal Bank of Scotland: Credit Risk Portfolio Engine

**Project:** Portfolio Risk Management & Digital Churn Analysis  
**Client:** Royal Bank of Scotland (via Ascentiq Solutions)  
**Role:** Data Warehouse Analyst

> **Professional Context:** This portfolio project demonstrates a Banking Intelligence system designed during my tenure at **Ascentiq Solutions**.
>
> *Note: While the data modeling, DAX logic, and strategic framework mirror real-world banking implementations delivered for RBS, the underlying dataset used in this public repository is synthetic to comply with GDPR and NDA regulations.*

| **Tech Stack** | **Domain** | **Framework** |
| :--- | :--- | :--- |
| ![Power BI](https://img.shields.io/badge/Power_BI-Pro-yellow?style=flat-square) ![SQL](https://img.shields.io/badge/SQL-Server-red?style=flat-square) | **Retail Banking** | **Risk Quadrant Analysis** |

---


## 🧭 Mission Directive

### 🎯 The Goal
To engineer a **360° Risk Intelligence System** that simultaneously monitors **Credit Default Risk** (Financial Health) and **Digital Churn** (Customer Retention). The objective is to safeguard the **£769M Loan Portfolio** while identifying the root causes of capital flight to Fintech competitors.

### 📉 The Challenge
The bank faced a "Blind Spot" crisis across three critical vectors:
1.  **Risk Segmentation:** Inability to isolate "Toxic Assets" (High LTV + Low Credit Score) from the general population.
2.  **Fintech Leakage:** Millions in capital were flowing to Neobanks (Monzo, Revolut), but the bank could not correlate this with Digital Maturity scores.
3.  **Regional Exposure:** Lack of visibility into which geographic hubs (e.g., North West) were driving the highest default rates.

---

## 📋 Executive Dossier

| **Metric** | **Value** | **Strategic Impact** |
| :--- | :--- | :--- |
| **Total Exposure** | **£769M** | Total active loan book currently under surveillance. |
| **At-Risk Capital** | **£552M** | Value of assets currently sitting in "Subprime" or "High LTV" quadrants. |
| **Fintech Leakage** | **£15M** | Verified capital flight to Neobank competitors (Wise, Monzo) in the last fiscal period. |
| **Churn Driver** | **UX Friction** | Customers with Digital Scores < 5.0 are **3x** more likely to churn than digital natives. |


---


## 📑 Table of Contents
1.  [Executive Summary & Quantified Impact](#-executive-summary--quantified-impact)
2.  [Business Architecture: The Triple Threat](#-business-architecture-the-triple-threat)
3.  [Data Structure (Star Schema)](#-data-structure-star-schema)
4.  [Dashboard Forensics (Deep Dive)(#-dashboard-deep-dive)
    *   [Dashboard 1: Credit Risk Overview (Macro)](#1%EF%B8%8F%E2%83%A3-dashboard-1-credit-risk-overview)
    *   [Dashboard 2: The Risk Quadrant (Micro](#2%EF%B8%8F%E2%83%A3-dashboard-2-the-risk-quadrant-advanced-analytics)
    *   [Dashboard 3: Digital Churn & Behavior (Customer)](#3%EF%B8%8F%E2%83%A3-dashboard-3-digital-churn--behavior)
5.  [UI/UX Design Philosophy](#-uiux-design-philosophy)
6.  [Technical Implementation](#-technical-implementation--expertise)
7.  [Strategic Recommendations](#-strategic-recommendations)
8.  [Assumptions & Future Scope](#-assumptions--future-scope)
9.  [Data Dictionary](#-data-dictionary)

## 📑 Executive Agenda
1.  [Portfolio Performance Review](#-portfolio-performance-review) *(Executive Summary)*
2.  [Risk Vectors Analyzed](#-risk-vectors-analyzed) *(Key Business Questions)*
3.  [Data Warehouse Modeling](#-data-warehouse-modeling) *(Data Structure)*
4.  [Visual Analytics Breakdown](#-visual-analytics-breakdown) *(Dashboard Deep Dive)*
5.  [User Experience Strategy](#-user-experience-strategy) *(UI/UX)*
6.  [Fiscal Strategy Proposals](#-fiscal-strategy-proposals) *(Strategic Recs)*
7.  [Model Limitations & Roadmap](#-model-limitations--roadmap) *(Assumptions)*
8.  [Solution Architecture](#-solution-architecture) *(Technical Implementation)*
9.  [Metric Definitions](#-metric-definitions) *(Data Dictionary)*


---


## 🏆 Executive Summary & Quantified Impact

This project consolidated millions of transaction rows into a centralized **Risk Engine**, identifying critical vulnerabilities in the bank's lending portfolio.

**Strategic Insights:**
*   **Portfolio Health:** Identified **49.8%** of the portfolio is categorized as "High Risk," primarily driven by aggressive lending in the North West region.
*   **Capital Flight:** Traced **£15M** in outbound transfers. Analysis confirms this is not random spending but structural migration to competitors offering better FX rates (Wise) and App UX (Monzo).
*   **Digital Correlation:** Proven a direct correlation between **Digital Maturity** and **Retention**. The "Digital Gap" (Scores < 5.0) is the single biggest predictor of customer attrition.

---

## 🏛️ Business Architecture: The Triple Threat

The bank faced a "Blind Spot" crisis across three critical vectors:
1.  **Risk Segmentation:** Inability to isolate "Toxic Assets" (High LTV + Low Credit Score) from the general population.
2.  **Fintech Leakage:** Millions were flowing to Neobanks, but the bank could not correlate this with customer demographics.
3.  **Regional Exposure:** Lack of visibility into which geographic hubs were driving the highest default rates.

---



---

## 🗂 Data Structure (Star Schema)

![Data Model Screenshot](Dashboard_previews/4.Model_View.png)

The data model is architected as a **Star Schema** to ensure high-performance filtering and accurate aggregations.

*   **Fact Tables (The Transactions):**
    *   `Fct_Credit_Exposure_Audit`: Contains loan balances, LTV ratios, and default flags.
    *   `Fct_Capital_Flight_Transactions`: Tracks outbound money movement and beneficiary banks.
*   **Dimension Tables (The Context):**
    *   `Dim_Customer_Registry`: Customer demographics, digital scores, and segmentation.
    *   `Dim_Product_Catalogue`: Loan types, interest rate types.
    *   `Dim_Calendar_Lookup`: Standard date table for Time Intelligence (MoM, YoY).
*   **Relationships:**
    *   Strict **One-to-Many (1:*)** relationships flowing from Dimensions to Facts.

---

## 🔍 Dashboard Forensics (Deep Dive)

### 1️⃣ Dashboard 1: Credit Risk Overview (Macro)
*The "Pulse Check" – A high-level executive summary of portfolio health.*

![Credit Risk Overview Dashboard](Dashboard_previews/1.Credit_Risk_Overview.png)

#### 🧮 KPI Analysis (Heads-Up Display)
*   **Total Exposure (£769M):** The sum of all active loan balances. This represents the total capital currently deployed in the market.
*   **Exposure at Risk (6.4%):** The percentage of the portfolio held by borrowers who have missed at least one payment or breached covenants.
*   **Default Rate (6.2%):** The realized loss rate. A trend arrow (▲ 3.0%) indicates this is worsening Month-over-Month.
*   **Avg LTV (62%):** The average Loan-to-Value ratio. While 62% appears healthy, the deep dive reveals pockets of 90%+ leverage.

#### 📊 Chart Forensics
*   **Portfolio Risk Distribution (Donut Chart):**
    *   *What:* Splits the portfolio into Low, Medium, and High risk buckets based on internal credit scoring.
    *   *Insight:* **49.8%** of the book is High Risk. This imbalance suggests the bank has been too aggressive in customer acquisition.
*   **12-Month Default Trend (Line Chart):**
    *   *What:* Tracks default rates over time.
    *   *Insight:* A distinct spike in **July (peaking at ~8%)** correlates with external interest rate hikes, suggesting the portfolio is highly sensitive to variable rate changes.
*   **Exposure by Region (Bar Chart):**
    *   *What:* Geographic breakdown of lending.
    *   *Insight:* **North West** holds >£300M in exposure, significantly more than London. This concentration risk requires immediate geofencing of lending policies.
---

### 2️⃣ Dashboard 2: The Risk Quadrant (Micro)
*The "Deep Dive" – Identifying the intersection of leverage and creditworthiness.*

![Risk Quadrant Screenshot](Dashboard_previews/2.Risk_Quadrant.png)

#### 🧮 KPI Analysis
*   **High LTV Exposure (39%):** The portion of loans where the debt is >80% of the asset value.
*   **Subprime Exposure (54%):** The percentage of borrowers with Credit Scores < 600.
*   **Exposure in Risk (£552M):** The monetary value sitting in the dangerous "Red Zone" of the scatter plot.

#### 📊 Visual Forensics
*   **Risk Concentration Scatter Plot (LTV vs Credit Score):** *The Hero Visual.*
    *   *X-Axis:* Credit Score | *Y-Axis:* LTV Ratio.
    *   *Logic:* Identifies the correlation between asset value (Collateral) and borrower reliability.
*   **Exposure in Risk Quadrant by Segment (Bar Chart):**
    *   *Insight:* **Families** and **Young Pros** hold the highest amount of toxic debt, suggesting aggressive lending to first-time buyers.
*   **Portfolio Distribution by LTV Band (Column Chart):**
    *   *Insight:* The tallest bars are in the **0.8 - 1.0** range. The bank has very few low-LTV loans, indicating a lack of conservative lending.

#### 🧠 The "Quadrant Theory" Logic
The Scatter Plot employs a **Ternary Risk Segmentation** model, color-coding customers based on their Credit Score bands while plotting them against their Asset Leverage (LTV).

*   **🔴 Band 1: High Risk (Subprime)**
    *   **Color:** `#E04444` (Red)
    *   **Profile:** Credit Score **400 - 600**.
    *   *Logic:* These borrowers have a history of delinquency. When these Red dots appear above the **80% LTV line** (Top Left), they represent **"Toxic Assets"**—high probability of default with low equity to recover losses.
    *   *Action:* Immediate lending freeze and increased loss provisions.

*   **🔵 Band 2: Medium Risk (Prime)**
    *   **Color:** `#2C7CCD` (Blue)
    *   **Profile:** Credit Score **600 - 750**.
    *   *Logic:* The core of the banking portfolio. While generally reliable, Blue dots sitting high on the Y-Axis (>80% LTV) act as **"Vulnerable Assets"**—they are currently paying but are highly sensitive to economic shocks or interest rate hikes.
    *   *Action:* Monitor closely for early signs of stress (missed payments).

*   **🟢 Band 3: Low Risk (Super Prime)**
    *   **Color:** `#00B0B9` (Teal)
    *   **Profile:** Credit Score **750 - 900**.
    *   *Logic:* The ideal customer profile. Even at higher LTVs, these borrowers have excellent repayment history. The dense cluster of Teal dots in the bottom right (<60% LTV) represents the bank's **"Safe Haven."**
    *   *Action:* Target for premium product cross-selling (Wealth Management, Premium Insurance).

---

### 3️⃣ Dashboard 3: Digital Churn & Behavior (Customer)
*The "Customer View" – Analyzing retention and Neobank competition.*

![Digital Churn Screenshot](Dashboard_previews/3.Digital_Churn_&_Behavior.png)

#### 🧮 KPI Analysis
*   **Churn Rate (10.3%):** The percentage of customers closing accounts annually.
*   **Capital Flight (£15M):** The total liquid assets transferred to competitors.
*   **Fintech Leakage (33.1%):** 1/3 of all money leaving the bank goes directly to Neobanks (Monzo, Revolut).
*   **Avg Digital Score (4.50):** The portfolio average is below the "Digitally Native" threshold of 5.0.

#### 📊 Visual Forensics
*   **Churn Rate by Digital Engagement (Column Chart):**
    *   *The "Digital Cliff":* A clear negative correlation. Customers with a Digital Score < 5.0 churn at **11-12%**. Customers with a score > 8.0 churn at only **~2%**.
    *   *Insight:* Poor App adoption is the #1 driver of customer loss.
*   **Fintech Competitor Breakdown (Bar Chart):**
    *   *What:* Where is the money going?
    *   *Insight:* **Wise** is the top destination. This suggests customers are leaving because RBS's foreign exchange fees are too high compared to Wise's "Mid-Market Rate."
#### 📱 Behavioral Correlation Analysis
This dashboard proves the hypothesis: **"Digital Friction causes Churn."**
*   **The "Digital Gap":** The charts reveal a distinct "Digital Cliff" at a score of **5.0**. Customers below this threshold churn at **11.2%**, while those above 8.0 churn at only **2.1%**.
*   **The "Fintech Leakage" Flow:** By analyzing the **Monthly Capital Flight Trend**, we see spikes coinciding with traditional "Bonus Months" (Dec/Jan). The money isn't just being withdrawn as cash; it is being *transferred* to specific routing numbers associated with **Wise**, indicating technical savviness but dissatisfaction with RBS fees.

---

## 🎨 UI/UX Design Philosophy
Unlike standard operational reports, this project utilizes a **"Strategic Dark Mode"** specifically designed for Executive Risk Monitors.

*   **Color Semantics:**
    *   **Deep Purple Background:** Reduces eye strain during long analysis sessions and aligns with the Premium Banking aesthetic.
    *   **Alert Red (`#D60000`):** Used *exclusively* for negative trends (Default Rate increases, Capital Flight) to draw the eye immediately.
    *   **Safety Teal/Blue:** Used for neutral volume metrics to prevent visual clutter.
*   **Navigation:** A persistent left-hand sidebar mimics SaaS application behavior, allowing users to switch contexts (Risk vs. Churn) without losing their filtered state.
---

## 🛠 Technical Implementation & Expertise

### SQL Transformation (The "Brain")
*   **Note on Data Architecture:** While the portfolio demonstration utilizes a static dataset (Excel/CSV), the production data pipeline logic has been modeled in SQL to demonstrate scalability. See `scripts/RBS_Data_Warehouse_ETL.sql` for the ELT logic.
*   **Key Techniques:**
*   **CTEs & Window Functions:** Used `ROW_NUMBER()` in SQL to deduplicate the customer registry and `RANK()` to grade credit scores.
*   **Data Modeling:** Built a **Star Schema**, connecting `Fact_Installments` and `Fact_Capital_Flight` to shared dimensions (`Dim_Customer`, `Dim_Date`).

### 🧮 DAX (Data Analysis Expressions)
*   **File:** [RBS_Key_Measures.dax](./scripts/RBS_Key_Measures.dax)
*   **Dynamic Risk Logic:** Used `SWITCH(TRUE()...)` to dynamically categorize Credit Score Bands (Red/Blue/Teal).
*   **Time Intelligence:** Calculated `MoM Capital Flight` using `CALCULATE` and `DATEADD`.
*   **Segmentation:** Used advanced logic to segment Digital Maturity scores.

---

## 💡 Strategic Recommendations

Based on the intelligence gathered, the following strategic pivots are recommended:

1.  **Lending Policy Review:** Immediately suspend high-LTV lending (>90%) in the **North West** region for applicants with credit scores < 600.
2.  **Digital Intervention:** Launch a targeted "App Onboarding" campaign for the "Retiree" segment (lowest digital scores) to reduce churn probability.
3.  **Competitor Defense:** To combat the £15M flight to **Wise**, introduce a "Fee-Free FX" product tier for "Young Pro" customers to retain their international transaction volume.

---

## 🧠 Assumptions & Future Scope

### Assumptions
*   **Currency:** All financial figures are in GBP (£).
*   **Fiscal Year:** Data aligns with the UK Fiscal Year (April - March).
*   **Default Definition:** A loan is flagged as "Default" after 90 days of missed payments.
*   **Digital Score:** A proprietary metric (0-10) calculated based on App Logins, Feature Usage, and Online Transactions.

### Future Scope
*   **Predictive AI:** Integrate Python/R scripts to forecast future "Capital Flight" based on current transaction patterns.
*   **Real-Time Alerts:** Implement Power Automate triggers to email Risk Officers when a High-Value customer initiates a transfer to a Crypto platform or Neobank.

---

## 📖 Data Dictionary

| Term | Definition | Logic Used |
| :--- | :--- | :--- |
| **LTV (Loan-to-Value)** | The ratio of the loan amount to the value of the asset purchased. | `Loan Balance / Collateral Value` |
| **Subprime** | Borrowers with a credit score below 600. | `Credit Score < 600` |
| **Capital Flight** | Money transferred out of RBS to specific Fintech competitors. | `Beneficiary Bank IN ('Monzo', 'Wise', 'Revolut')` |
| **Digital Maturity** | A score indicating how "digital-first" a customer is. | Scale of 1-10 (10 = Fully Mobile Banking User) |
| **Toxic Asset** | A loan with high probability of default and low recovery value. | `LTV > 80% AND Credit Score < 600` |

---
*Author: Sagar Chaandwani*
