# Business Requirements Document (BRD)
## Project: Bank Loan Risk Analysis

---

### 1. Business Problem
The lending business needed to identify patterns that signal a customer's potential difficulty in meeting loan installment obligations, in order to reduce default risk and improve loan approval decision-making.

### 2. Business Objective
Enable the lending/credit risk team to make more informed decisions on:
- Loan approval vs. denial
- Adjusting loan amounts for risk-flagged applicants
- Applying higher interest rates to riskier applicant segments

### 3. Scope
Analysis of loan application data (current and previous applications) covering applicant demographics, income, credit amount, family/employment status, and loan outcome status. Four possible loan outcomes were in scope: Approved, Cancelled, Refused, Unused Offer. Excludes predictive/ML-based credit scoring — this is a descriptive/diagnostic risk analysis.

### 4. Stakeholders
- Credit/Risk assessment team (primary stakeholder)
- Loan approval/underwriting team
- Business leadership (consumers of risk-segment findings for policy decisions)

### 5. Key Business Requirements
| ID | Requirement | Priority |
|----|-------------|----------|
| BR-1 | Identify and handle missing/null data appropriately before analysis | Must have |
| BR-2 | Detect outliers in key numerical fields (income, annuity, credit) | Must have |
| BR-3 | Assess class imbalance in loan default outcomes (target variable) | Must have |
| BR-4 | Segment applicant behavior by demographic/status variables (family status, income type, housing type, education) | Should have |
| BR-5 | Identify correlations between financial variables to flag risk-related relationships | Should have |

### 6. Data Requirements
Loan application dataset (application_data) and prior loan history dataset (previous_application), containing applicant income, credit amount, annuity, family status, education, housing type, employment type, and loan outcome/target fields.

### 7. Data Preparation Notes (as performed)
- Missing data identified using COUNTA and null-percentage formulas; columns with more than 35% (application data) / 30% (previous application data) missing values were excluded as low-value for analysis
- Outliers identified using IQR method (Q1, Q3, Upper/Lower Limit formulas) on key numeric fields — flagged via scatter plots on Income and Annuity by Target
- Duplicate rows and irrelevant columns removed
- Tool used: Microsoft Excel 2021

### 8. Key Findings Delivered to Stakeholders
- **Class imbalance:** Loan default (Target = 1) accounts for only 2,304 cases vs. 25,014 non-default cases — a significant imbalance that must be accounted for in any risk model or policy decision
- **Descriptive stats (Total Income):** Mean ₹1,82,906, Median ₹1,57,500 — right-skewed by high-income outliers (max ₹11.7 crore)
- **Descriptive stats (Annuity):** Mean ₹28,001, Median ₹26,145
- **Contract type imbalance:** Consumer loans (22,280) far outnumber Cash loans (12,917) and Revolving loans (2,802)
- **Family status:** Married applicants represent the largest applicant segment (18,247) and also the largest share of both approved and defaulted loans (16,810 non-default, 1,437 default)
- **Housing type:** Applicants living in House/Apartment (24,054) dominate loan applications over other housing categories
- **Correlation analysis:** Strong positive correlation between Annuity, Application Amount, Credit Amount, and Goods Price (0.82–0.99 range), indicating these move together as expected
- **Higher loan-uptake profile identified:** Married, Educated, Strong Work Experience, Previously Approved Clients
- **Lower loan-uptake profile identified:** Unemployed, Youth, Less Work Experience, Previously Unapproved Clients

### 9. Business Recommendation
- Any credit-risk scoring or approval policy must account for the significant class imbalance in default outcomes (2,304 vs 25,014) — raw approval-rate comparisons without this adjustment will be misleading
- Prioritize deeper due diligence on applicant segments showing lower repayment correlation (Unemployed, Youth, limited work experience, previously unapproved) before extending standard terms
- Consumer loan applicants represent the largest volume segment and should be the primary focus for risk-policy refinement given their scale
- Use the identified high-uptake profile (Married, Educated, Employed, Previously Approved) as a baseline for streamlined approval processing, while flagging deviations for manual review

### 10. Out of Scope
Predictive credit-scoring model development; real-time fraud detection; year-over-year default trend comparison (single-period dataset analysis).
