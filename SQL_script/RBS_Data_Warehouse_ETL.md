/*
===========================================================================
PROJECT:        RBS Credit Risk & Digital Churn Analysis
FILE:           RBS_Data_Warehouse_ETL.sql
AUTHOR:         Sagar Chaandwani
DESCRIPTION:    ETL Transformation Logic to build the Star Schema for Power BI.
                Techniques: CTEs, Window Functions, Categorization, Joins.
===========================================================================
*/

-- ========================================================================
-- 1. DIMENSION: Customer Registry
-- Objective: Deduplicate customer master data and calculate demographic bins.
-- ========================================================================
CREATE VIEW Dim_Customer_Registry AS
WITH Raw_Cust AS (
    SELECT 
        Customer_ID,
        Age,
        Region,
        Segment, -- Family, Retiree, Young Pro, etc.
        Digital_Maturity_Score, -- 1 to 10
        Nationality_Status,
        -- Window Function: Get the latest record per customer if duplicates exist
        ROW_NUMBER() OVER(PARTITION BY Customer_ID ORDER BY Last_Updated_Date DESC) as rn
    FROM Staging_Customer_DB
)
SELECT 
    Customer_ID,
    Age,
    -- Transformation: Age Binning
    CASE 
        WHEN Age < 25 THEN '18-24'
        WHEN Age < 35 THEN '25-34'
        WHEN Age < 50 THEN '35-49'
        ELSE '50+' 
    END AS Age_Bins,
    Region,
    Segment,
    Digital_Maturity_Score,
    -- Transformation: Digital Engagement Classification
    CASE 
        WHEN Digital_Maturity_Score >= 8 THEN 'Digitally Native'
        WHEN Digital_Maturity_Score >= 5 THEN 'Hybrid'
        ELSE 'Legacy' 
    END AS Digital_Profile,
    Nationality_Status
FROM Raw_Cust
WHERE rn = 1;




-- ========================================================================
-- 2. FACT: Credit Exposure Audit
-- Objective: Calculate LTV, Risk Bands, and Default Status for the Credit Portfolio.
-- ========================================================================



CREATE VIEW Fct_Credit_Exposure_Audit AS
WITH Loan_Calculations AS (
    SELECT 
        t.Loan_ID,
        t.Customer_ID,
        t.Product_ID,
        t.Loan_Balance,
        t.Collateral_Value,
        t.Credit_Score,
        t.Default_Status, -- 1 = Default, 0 = Active
        
        -- Logic: Calculate Loan-to-Value (LTV) Ratio
        (t.Loan_Balance / NULLIF(t.Collateral_Value, 0)) AS LTV_Ratio
    FROM Staging_Loan_Portfolio t
)
SELECT 
    lc.Loan_ID,
    lc.Customer_ID,
    lc.Product_ID,
    lc.Loan_Balance,
    lc.Credit_Score,
    
    -- Transformation: Credit Score Binning
    CASE 
        WHEN lc.Credit_Score < 580 THEN 'Subprime'
        WHEN lc.Credit_Score < 670 THEN 'Fair'
        WHEN lc.Credit_Score < 740 THEN 'Good'
        ELSE 'Excellent' 
    END AS Credit_Score_Bin,
    
    lc.LTV_Ratio,
    
    -- Transformation: LTV Risk Bands
    CASE 
        WHEN lc.LTV_Ratio > 0.90 THEN 'High Risk (>90%)'
        WHEN lc.LTV_Ratio > 0.75 THEN 'Medium Risk (75-90%)'
        ELSE 'Low Risk (<75%)' 
    END AS LTV_Band,

    -- Risk Quadrant Logic (High LTV + Low Credit Score)
    CASE 
        WHEN lc.LTV_Ratio > 0.85 AND lc.Credit_Score < 600 THEN 1 
        ELSE 0 
    END AS High_Risk_Flag,

    lc.Default_Status

FROM Loan_Calculations lc;




-- ========================================================================
-- 3. FACT: Capital Flight Transactions
-- Objective: Analyze money flowing out to Fintech competitors (Monzo, Revolut, etc.)
-- ========================================================================



CREATE VIEW Fct_Capital_Flight_Transactions AS
SELECT 
    txn.Transaction_ID,
    txn.Customer_ID,
    txn.Transaction_Date,
    txn.Amount,
    txn.Beneficiary_Bank, -- e.g., 'Monzo', 'Starling', 'Revolut'
    
    -- Logic: Flag "Capital Flight" if money moves to a Neobank
    CASE 
        WHEN txn.Beneficiary_Bank IN ('Monzo', 'Starling', 'Revolut', 'Wise') THEN 1 
        ELSE 0 
    END AS Is_Fintech_Leakage,

    -- Logic: Identify "Missed EMI" (Equated Monthly Installment)
    txn.Missed_EMI_Flag

FROM Staging_Transactions txn
WHERE txn.Transaction_Type = 'Outbound';