# Business Requirements Document (BRD)
## Project: Operational Analytics & Metric Spike Investigation

---

### 1. Business Problem
Operations, support, and marketing teams needed a reliable way to track throughput, user engagement, retention, growth, and email performance — and to quickly investigate and explain sudden changes ("spikes" or dips) in these metrics, such as drops in daily engagement or unusual shifts in activity.

### 2. Business Objective
Enable operational and product teams to:
- Monitor day-to-day and week-to-week operational health through consistent metrics
- Detect and explain metric anomalies before they escalate into larger business problems
- Support decisions on automation, workflow improvement, and customer engagement strategy

### 3. Scope
Analysis covers two data domains: (1) Job Data — job review throughput, language distribution, duplicate detection; and (2) User/Event Data — weekly user engagement, user growth, retention, engagement per device, and email engagement metrics. Excludes root-cause automation or alerting system design — this is a diagnostic/reporting analysis.

### 4. Stakeholders
- Operations team (job throughput, review volume)
- Product/Growth team (user engagement, retention, growth)
- Marketing team (email engagement metrics)

### 5. Key Business Requirements
| ID | Requirement | Priority |
|----|-------------|----------|
| BR-1 | Track job review throughput (per hour/day) and smooth short-term noise via rolling average | Must have |
| BR-2 | Report language-share distribution for reviewed content | Should have |
| BR-3 | Detect and flag duplicate records that could distort metrics | Must have |
| BR-4 | Track weekly user engagement and cumulative user growth | Must have |
| BR-5 | Measure weekly retention of sign-up cohorts | Should have |
| BR-6 | Measure engagement per device to guide platform investment | Should have |
| BR-7 | Track email engagement (open rate, click rate) to support marketing decisions | Must have |

### 6. Data Requirements
Job review data (job_id, date, language) and user event data (user_id, occurred_at, event_type, event_name, device) sourced via SQL (MySQL Workbench), with visualization performed in Microsoft Excel.

### 7. Data Preparation / Method Notes (as performed)
- Data loaded into a MySQL database using CREATE DB, table creation, and INSERT INTO
- Throughput calculated using distinct vs. non-distinct job_id counts, divided across the reporting period
- 7-day rolling average computed using window functions (ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)
- Duplicate detection performed using ROW_NUMBER() partitioned by job_id, filtering WHERE row_num > 1
- Weekly engagement/growth computed using EXTRACT, WEEK, GROUP BY, and cumulative SUM/OVER window functions
- Email engagement segmented using CASE/WHEN logic across sent, opened, and clicked event categories

### 8. Key Findings Delivered to Stakeholders
- **Job throughput:** 0.0083 jobs reviewed per hour (distinct) vs. 0.0111 (non-distinct) — the gap itself signaled duplicate records requiring cleanup
- **7-day rolling average adopted over daily metric** specifically because daily figures are too volatile for trend reporting; rolling average smooths short-term noise for more stable operational monitoring
- **Language distribution anomaly:** Persian showed a disproportionate 37.5% share vs. ~12.5% for other languages — investigated and traced to duplicate rows (job_id = 23 appeared twice), demonstrating direct business impact of unresolved duplicates on reporting accuracy
- **User growth:** 9,381 cumulative active users tracked from week 1 of 2013 to week 35 of 2014
- **Peak weekly engagement:** Week 31 recorded the highest engagement at 1,685 active users — a spike worth flagging for stakeholder review
- **Email engagement:** 33.58% open rate, 14.79% click rate — interpreted as roughly 1 in 3 sent emails opened, and only 1 in 7 opened emails resulting in a click-through, indicating room to improve subject-line quality and content targeting

### 9. Business Recommendation
- Standardize on 7-day rolling averages (not daily snapshots) for throughput and engagement reporting to avoid reacting to noise rather than genuine trend shifts
- Implement a duplicate-detection check as a standing step before any metric reporting cycle — the Persian-language anomaly demonstrates how a small number of duplicate rows can materially distort findings and risk poor business decisions
- Marketing should revise email subject lines and content strategy given the relatively low click-through rate (14.79%) following open, since this is where the funnel is currently leaking engagement
- Continue tracking engagement per device to guide where platform/UX investment should be prioritized
- Flag week-over-week spikes (such as Week 31) for proactive stakeholder review rather than only reactive investigation after a decline

### 10. Out of Scope
Automated anomaly-detection/alerting systems; root-cause attribution beyond descriptive investigation; cross-year trend forecasting.
