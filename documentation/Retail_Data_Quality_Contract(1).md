# Retail Orders — Data Quality Contract

## 1. Purpose
This contract defines when retail-order data is trustworthy enough for KPI reporting.

**Decision owner:** E-commerce Operations Manager  
**Supporting owners:** Finance Manager, Pricing Manager, Data/Pipeline Owner  
**Refresh target:** Daily

## 2. KPI publication rule
Order-level and sales KPIs are published only when all blocking quality rules pass. A failed blocking rule requires remediation and rerun of the profile before publication.

## 3. Quality rules

| ID | Dimension | Threshold | Action on failure |
|---|---|---|---|
| Q-01 | Completeness | 100% for required fields | Block KPI publication; fix source |
| Q-02 | Discount completeness | ≤5% missing; missing = 0 only after approval | Hold pricing KPIs |
| Q-03 | Uniqueness | 0 duplicate order IDs | Block order KPIs |
| Q-04 | Date validity | 100% parseable and in allowed range | Block time-series KPIs |
| Q-05 | Numeric validity | 100% positive integer quantity and non-negative price | Block sales/volume KPIs |
| Q-06 | Discount validity | 100% in 0–100 | Block net-sales/discount KPIs |
| Q-07 | Domain validity | 100% approved categorical values | Quarantine invalid values |
| Q-08 | Freshness | ≤1 business day behind expected refresh | Escalate to pipeline owner |
| Q-09 | Consistency | 100% reproducible derived metrics | Stop publication and reconcile |

## 4. Current sample status
**FAIL — do not treat the current raw file as production-ready.**

Observed issues include duplicate order ID `RT-1004`, an invalid date (`2026-13-10`), a missing order date, a missing city, non-numeric quantity (`two`), negative quantity (`-1`), missing discount, and discount `105%`.

## 5. Escalation
1. Data/Pipeline Owner: structural, parsing, duplicate, and freshness failures.
2. Finance/Pricing Owner: business treatment of missing discounts and payment-state interpretation.
3. E-commerce Operations Manager: final decision to release or hold KPI reporting.

## 6. Evidence
- `Retail_KPI_Dictionary_and_Data_Quality_Contract.xlsx`
- `Retail_Data_Profile_and_Quality_Contract.ipynb`
