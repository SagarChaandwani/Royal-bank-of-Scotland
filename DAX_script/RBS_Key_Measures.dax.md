/* 
=========================================================================
PROJECT: Royal Bank of Scotland - Risk & Churn Dashboard
AUTHOR: Sagar Chaandwani
DESCRIPTION: DAX Measures for Credit Risk, LTV Analysis, and Digital Churn.
=========================================================================
*/

/* -----------------------------------------------------------------------
   1. CREDIT RISK & EXPOSURE METRICS
   ----------------------------------------------------------------------- */

-- Total Exposure (£)
Total Exposure = 
SUM('Fct_Credit_Exposure_Audit'[Loan_Balance])



-- Exposure at Risk (Subprime + High LTV)
Exposure at Risk = 
CALCULATE(
    [Total Exposure],
    'Fct_Credit_Exposure_Audit'[High_Risk_Flag] = 1
)



-- Default Rate %
Default Rate = 
DIVIDE(
    CALCULATE(COUNTROWS('Fct_Credit_Exposure_Audit'), 'Fct_Credit_Exposure_Audit'[Default_Status] = "Default"),
    COUNTROWS('Fct_Credit_Exposure_Audit'),
    0
)




-- Average Loan-to-Value (LTV)
Avg LTV = 
AVERAGE('Fct_Credit_Exposure_Audit'[LTV_Ratio])




-- High LTV Exposure %
High LTV Exposure % = 
DIVIDE(
    CALCULATE([Total Exposure], 'Fct_Credit_Exposure_Audit'[LTV_Band] = "High Risk (>90%)"),
    [Total Exposure],
    0
)




/* -----------------------------------------------------------------------
   2. CAPITAL FLIGHT & CHURN METRICS
   ----------------------------------------------------------------------- */



-- Total Capital Flight (Money moved to Fintechs)
Capital Flight (£) = 
CALCULATE(
    SUM('Fct_Capital_Flight_Transactions'[Amount]),
    'Fct_Capital_Flight_Transactions'[Is_Fintech_Leakage] = 1
)



-- Churn Rate %
Churn Rate = 
DIVIDE(
    DISTINCTCOUNT('Fct_Capital_Flight_Transactions'[Customer_ID]), -- Assuming transaction implies churn risk
    COUNTROWS('Dim_Customer_Registry'),
    0
)



-- Fintech Leakage % (Share of Wallet lost)
Fintech Leakage = 
DIVIDE(
    [Capital Flight (£)],
    SUM('Fct_Capital_Flight_Transactions'[Amount]),
    0
)



-- Average Digital Score
Avg Digital Score = 
AVERAGE('Dim_Customer_Registry'[Digital_Maturity_Score])



/* -----------------------------------------------------------------------
   3. DYNAMIC FORMATTING & ICONS
   Used for KPI Cards to show Up/Down Arrows
   ----------------------------------------------------------------------- */


-- Logic: If Default Rate increased vs last month, show Red Up Arrow
Risk Trend Icon = 
VAR CurrentRate = [Default Rate]
VAR PrevRate = CALCULATE([Default Rate], DATEADD('Dim_Calendar_Lookup'[Date], -1, MONTH))
RETURN
    SWITCH(TRUE(),
        CurrentRate > PrevRate, "▲", -- Bad (Risk went up)
        CurrentRate < PrevRate, "▼", -- Good (Risk went down)
        "-"
    )




-- Conditional Formatting Color (Hex Codes)
Risk Trend Color = 
VAR CurrentRate = [Default Rate]
VAR PrevRate = CALCULATE([Default Rate], DATEADD('Dim_Calendar_Lookup'[Date], -1, MONTH))
RETURN
    IF(CurrentRate > PrevRate, "#D60000", "#339933") -- Red if Risk Incr, Green if Decr
