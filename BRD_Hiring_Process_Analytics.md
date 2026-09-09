# Business Requirements Document (BRD)
## Project: Hiring Process Analytics

---

### 1. Business Problem
The hiring department needed visibility into recruitment trends — hiring split by gender, salary distribution, department-wise workforce concentration, and job role (post tier) demand — to support workforce planning and recruitment strategy decisions.

### 2. Business Objective
Enable HR/hiring stakeholders to make data-driven decisions on:
- Salary benchmarking for incoming hires
- Departmental workforce planning
- Role-wise (post tier) hiring priorities

### 3. Scope
Analysis of historical hiring records covering: gender of hires, salary offered, department, and post tier (job role), for the purpose of workforce and recruitment reporting. Excludes forecasting/predictive modeling — this is a descriptive/diagnostic analysis.

### 4. Stakeholders
- Hiring / HR department (primary stakeholder)
- Workforce planning team
- Department heads (secondary — consumers of department-wise findings)

### 5. Key Business Requirements
| ID | Requirement | Priority |
|----|-------------|----------|
| BR-1 | Report on total male vs female hires | Must have |
| BR-2 | Report average salary offered company-wide | Must have |
| BR-3 | Salary class-interval (range) breakdown to identify where most offers cluster | Should have |
| BR-4 | Department-wise workforce proportion (visual) | Must have |
| BR-5 | Post-tier (role) wise vacancy/opening count | Must have |

### 6. Data Requirements
Employee hiring dataset containing: gender, hire status, salary, department, and post tier fields. Data required cleaning — missing values, outliers (salary), and duplicates needed to be handled before analysis (see Data Preparation Notes).

### 7. Data Preparation Notes (as performed)
- Raw data duplicated before modification to preserve original dataset
- Checked for blanks/NULLs; imputed numerical fields with mean (no outliers) or median (where outliers existed)
- Outliers detected and replaced with column median
- Categorical blanks filled with the mode (highest-count category)
- Duplicate rows removed
- Irrelevant columns dropped
- Tool used: Microsoft Excel

### 8. Key Findings Delivered to Stakeholders
- **Gender split:** 2,563 males vs 1,855 females hired
- **Average salary offered:** ₹49,983 (after outlier removal — salaries below ₹1,000 and above ₹1,00,000 excluded)
- **Salary concentration:** highest post volume falls in the ₹41,807–₹46,907 range (406 posts); among hired employees specifically, concentration peaks in the ₹42,307–₹54,107 range (315 hires)
- **Department distribution:** Operations is the largest department at 1,843 employees (~39% of total workforce), followed by Service (1,332, ~28%) and Sales (485, ~10%)
- **Role demand:** Post tier "c9" has the highest number of openings — 1,792, accounting for ~25% of total vacancies

### 9. Business Recommendation
- Use the ₹42,307–₹54,107 salary band as the primary benchmark range when setting offers for standard roles, since this is where actual hiring concentration sits
- Prioritize recruitment resourcing toward Operations and Service departments given their disproportionate share of workforce and likely ongoing backfill needs
- Treat post tier "c9" as a standing high-priority recruitment category given it accounts for a quarter of all vacancies
- Investigate regional/role-based drivers behind the gender hiring gap if diversity targets are a stated company priority

### 10. Out of Scope
Root-cause investigation into gender hiring disparity beyond descriptive observation; predictive salary modeling; year-over-year trend comparison (single-period dataset).
