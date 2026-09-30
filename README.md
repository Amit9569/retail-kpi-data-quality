# 🛡️ Retail KPI Dictionary & Data Quality Contract

## 📌 Project Overview

This project demonstrates how to transform an ambiguous retail business requirement into measurable KPIs and a testable data-quality agreement.

The project combines:

- KPI definition and governance
- Data profiling
- Data-quality validation
- Automated quality checks
- Business rules and thresholds
- Data-quality escalation procedures

The goal is to ensure that business dashboards and reports are built only on trustworthy and well-defined data.

---

## 🎯 Business Problem

Retail teams often calculate KPIs differently across reports.

For example:

- What exactly counts as an order?
- Should refunded orders be included?
- How should missing discounts be treated?
- What happens when an order contains an invalid quantity?
- Can sales KPIs be trusted when duplicate orders exist?

This project creates a standardized KPI dictionary and a data-quality contract to answer these questions.

---

## 🏢 Decision Owner

**Primary Decision Owner:** E-Commerce Operations Manager

### Supporting Stakeholders

- Finance Manager
- Pricing Manager
- Data/Pipeline Owner

---

## 📊 KPI Dictionary

| KPI | Definition |
|---|---|
| Total Orders | Count of distinct valid orders |
| Gross Order Value | Sum of quantity × unit price |
| Net Sales | Gross value after applying discounts |
| Units Sold | Total valid units sold |
| Average Order Value | Net Sales ÷ realized orders |
| Average Discount % | Weighted average discount |
| Paid Order Rate | Paid orders ÷ valid orders × 100 |
| Refund Rate | Refunded orders ÷ valid orders × 100 |

Each KPI is documented with:

- Formula
- Data grain
- Filters
- Business rules
- Decision owner
- Refresh cadence

---

## 🔍 Data Quality Framework

The dataset is evaluated across five major dimensions:

### 1. Completeness

Checks whether required fields contain valid values.

Examples:

- Order ID
- Order date
- City
- Quantity
- Payment status

### 2. Uniqueness

Checks whether `order_id` contains duplicate records.

### 3. Validity

Checks whether values follow expected business rules.

Examples:

- Quantity must be a positive integer.
- Unit price must be non-negative.
- Discount must be between 0% and 100%.
- Dates must be valid.

### 4. Consistency

Checks whether derived metrics can be reproduced correctly from source fields.

### 5. Freshness

Checks whether the dataset is updated within the agreed refresh window.

---

## 🚨 Data Quality Contract

The project defines explicit thresholds for each quality rule.

| Quality Rule | Threshold | Action |
|---|---:|---|
| Required fields | 100% | Block KPI publication |
| Duplicate Order IDs | 0 | Investigate source |
| Valid Dates | 100% | Block time-series KPIs |
| Valid Quantity | 100% | Block sales KPIs |
| Valid Unit Price | 100% | Block sales KPIs |
| Valid Discount | 100% | Block discount KPIs |
| Valid Categories/Statuses | 100% | Quarantine invalid values |
| Freshness | ≤ 1 business day | Escalate pipeline issue |

---

## 🧪 Automated Data Profiling

The project includes an executable Jupyter Notebook that performs automated validation using Python.

### Checks implemented

- Missing-value detection
- Duplicate detection
- Date parsing
- Quantity validation
- Price validation
- Discount validation
- Category validation
- Payment-status validation
- Consistency checks
- Freshness assessment
- Final quality-contract PASS/FAIL gate

---

## ⚠️ Current Data Quality Findings

The initial raw dataset does **not** pass the quality contract.

Issues detected include:

- Duplicate order IDs
- Invalid order dates
- Missing order dates
- Missing city values
- Non-numeric quantity
- Negative quantity
- Missing discount
- Discount greater than 100%
- Inconsistent categorical values

This demonstrates why data-quality validation should happen before KPI reporting.

---

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Jupyter Notebook
- Excel
- GitHub

---

## 📁 Project Structure

```text
retail-kpi-data-quality/
│
├── data/
│   ├── retail-orders-raw.csv
│   └── retail-data-dictionary.csv
│
├── notebooks/
│   └── Retail_Data_Profile_and_Quality_Contract.ipynb
│
├── documentation/
│   └── Retail_Data_Quality_Contract.md
│
├── outputs/
│   └── Retail_KPI_Dictionary_and_Data_Quality_Contract.xlsx
│
├── README.md
└── requirements.txt
