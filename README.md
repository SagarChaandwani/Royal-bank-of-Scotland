# Royal Bank of Scotland: Credit Risk Portfolio Engine

**Project:** Portfolio Risk Management & Digital Churn Analysis  
**Client:** Royal Bank of Scotland (via Ascentiq Solutions)  
**Role:** Data Analyst

> **Professional Context:** This portfolio project demonstrates real-world banking analytics delivered during my tenure at **Ascentiq Solutions**.
>
> *Note: While the data modeling, DAX logic, and strategic framework mirror real-world banking implementations delivered for RBS, the underlying dataset used in this public repository is synthetic to comply with GDPR and NDA regulations.*

| **Tech Stack** | **Domain** | **Framework** |
| :--- | :--- | :--- |
| ![Power BI](https://img.shields.io/badge/Power_BI-Pro-yellow?style=flat-square) ![SQL](https://img.shields.io/badge/SQL-Server-red?style=flat-square) | **Retail Banking** | **Risk Quadrant Analysis** |

---


##  Executive Summary 

**The Problem:**

   RBS managed a £769M loan portfolio but lacked visibility into:
1. Which assets were becoming high-risk (“toxic”)
2. Why customers were moving capital to fintech competitors
3. How digital behaviour was influencing churn
This created blind spots across risk, retention, and regional exposure.

**The Solution:**

   I built a 360° Risk Intelligence System that unified:
1. Credit risk (LTV, credit score, defaults)
2. Digital engagement behaviour
3. Capital flight tracking to fintechs (Wise, Monzo, Revolut)

**The Impact:**

1. Identified £15M in active capital flight to fintech competitors
2. Exposed £300M+ in high-risk exposure concentrated in the North West
3. Proven customers with low digital engagement churn at 3× the rate
This enabled targeted intervention by senior risk and product stakeholders.

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
*Below is the Executive "Pulse Check" used by Senior Risk Officers to monitor the £769M portfolio.*

![Credit Risk Overview Dashboard](Dashboard_previews/1.Credit_Risk_Overview.png)

---

## 🔍 Key Insights (The Data Story)

### 1️⃣ The Hidden Competitor Isn’t a Bank
Tracking outbound transfers revealed that **33% of lost deposits** were flowing directly to **Wise** and **Revolut**.

*   **Insight:** Customers weren’t leaving for better interest rates — they were leaving for lower FX fees and better App UX.
*   **Evidence:** Capital flight spiked during holiday months (Dec/Jan), confirming usage for travel and international spend.
---

### 2️⃣ Dashboard 2: The Risk Quadrant 


![Risk Quadrant Screenshot](Dashboard_previews/2.Risk_Quadrant.png)

Using a **Risk Quadrant Model** (LTV vs. Credit Score), I segmented the full portfolio to find the intersection of leverage and reliability.

*   **Finding:** **49.8%** of the portfolio sat in the "High-Risk" quadrant.
*   **Root Cause:** Aggressive high-LTV lending (>90%) to "Young Professionals" in the North West, leaving assets highly exposed to interest rate shocks.
  
---

### 3️⃣ Dashboard 3: Digital Churn & Behavior (Customer)

![Digital Churn Screenshot](Dashboard_previews/3.Digital_Churn_&_Behavior.png)

I tested the hypothesis: *"Does a bad mobile app experience actually cause customers to leave?"*

*   **Result:**
    *   Digital Score < 5.0 → **11.2% Churn**
    *   Digital Score > 8.0 → **2.1% Churn**
*   **Conclusion:** Digital experience is not just an IT metric — it is a multi-million-pound retention lever.

---

## 💡 Strategic Recommendations
Based on these insights, I proposed the following actions which were presented to stakeholders:

1.  **Stop the Bleeding:** Launch a "Fee-Free FX" tier targeting Young Professionals to recapture the £15M Fintech leakage.
2.  **Geofence Lending Risk:** Cap new lending at **80% LTV** in the North West region until default rates stabilize.
3.  **Digital Intervention:** Introduce an "App Onboarding" program for low-engagement segments (e.g., Retirees) to reduce their churn probability.


---

## 🛠 Technical Implementation & Expertise

**1. Data Modeling (Star Schema)**
*   Engineered a robust SQL backend linking `Fact_Credit_Exposure` and `Fact_Capital_Flight` to shared dimensions (`Dim_Customer`, `Dim_Product`).
*   Ensured 1-to-Many relationships to support dynamic filtering by Region and Demographics.

**2. Advanced DAX**
*   **Dynamic Segmentation:** Used `SWITCH(TRUE())` logic to classify customers into Red/Amber/Green risk buckets dynamically.
*   **Churn Calculation:** Implemented time-intelligence functions to track rolling 12-month attrition rates.

**3. UX Design**
*   **Dark Mode Interface:** Designed specifically for Risk Analysts who view screens for long periods.
*   **Alert-Based Semantics:** Used `#D60000` (Red) *only* for negative trends to draw immediate executive attention to problem areas.


---

## 👔 Why This Project Matters
This case study demonstrates my ability to:
*   **Translate** complex banking data into executive-level decisions.
*   **Balance** risk management with commercial growth.
*   **Influence** stakeholders using clear, evidence-based storytelling.

---
*Created by: Sagar Chaandwani*
