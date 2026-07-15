# Customer-Churn-Analytics-PowerBI
# 📊 Customer Churn Analytics Dashboard

An interactive **Power BI dashboard** that analyzes telecom customer churn — uncovering who is leaving, why they're leaving, and how much revenue is at risk — so retention teams can act before it's too late.

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-2E74B5?style=flat)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=flat)
![Status](https://img.shields.io/badge/status-completed-brightgreen)

---

## 📑 Table of Contents

- [Introduction](#-introduction)
- [What This Project Does](#-what-this-project-does)
- [Objectives](#-objectives)
- [Tools & Technologies](#-tools--technologies)
- [Dataset](#-dataset)
- [Project Workflow](#-project-workflow)
- [Dashboard Preview](#-dashboard-preview)
- [Questions Answered by the Dashboard](#-questions-answered-by-the-dashboard)
  - [1. Customer Overview](#1-customer-overview)
  - [2. Revenue Analysis](#2-revenue-analysis)
  - [3. Customer Behavior](#3-customer-behavior)
  - [4. Contract Analysis](#4-contract-analysis)
  - [5. Internet Service Analysis](#5-internet-service-analysis)
  - [6. Payment Analysis](#6-payment-analysis)
  - [7. Customer Demographics](#7-customer-demographics)
  - [8. Customer Tenure](#8-customer-tenure)
  - [9. Billing Analysis](#9-billing-analysis)
  - [10. Root Cause Analysis](#10-root-cause-analysis)
  - [11. Dashboard & Reporting](#11-dashboard--reporting)
- [Key Business Insights](#-key-business-insights)
- [Recommendations](#-recommendations)
- [Skills Demonstrated](#-skills-demonstrated)
- [Author](#-author)

---

## 🧩 Introduction

Customer churn — when a customer stops doing business with a company — is one of the most expensive problems in subscription-based industries like telecom. Acquiring a new customer costs far more than retaining an existing one, so knowing **who is likely to leave, why, and what it will cost** is a direct lever on revenue.

This project turns a raw telecom customer dataset into an interactive Power BI dashboard that surfaces churn patterns, flags high-risk customers, and quantifies the revenue at stake — giving business teams a self-service analytics tool instead of a static spreadsheet.

## 🎯 What This Project Does

The dashboard takes 7,000+ customer records and transforms them into:

- A live view of **overall churn rate** and how it shifts across customer segments
- A calculated **Risk Score** for every customer, so the highest-risk accounts surface automatically
- Drill-down analysis (via a decomposition tree) into **why** a customer is likely to churn
- A clear picture of **revenue at risk**, not just customer counts
- Interactive **slicers** so any question below can be re-explored by gender, contract, payment method, or service type in seconds

## 🎯 Objectives

- Analyze churn patterns across the telecom customer base
- Identify high-risk customers who are most likely to churn
- Monitor key performance indicators (KPIs) related to retention and revenue
- Support data-driven business decisions with an interactive, self-service dashboard

## 🛠 Tools & Technologies

| Tool | Purpose |
|---|---|
| **Microsoft Power BI Desktop** | Dashboard design & visualization |
| **Power Query** | Data import, cleaning, and transformation |
| **DAX (Data Analysis Expressions)** | Calculated measures, KPIs, and the customer risk score |
| **Microsoft Excel** | Supporting data checks |

## 📂 Dataset

- **Source:** Telco Customer Churn dataset (Kaggle)
- **Size:** 7,032 customer records, 21 attributes
- **Attributes include:** gender, senior citizen status, partner/dependents, contract type, internet service, payment method, tenure, monthly charges, total charges, and churn status

## 🔄 Project Workflow

1. **Data Collection** – CSV imported into Power BI and validated for completeness
2. **Data Cleaning** – handled in Power Query: data types corrected, blanks and duplicates resolved
3. **Data Modeling** – single-table model, all logic handled through DAX measures
4. **DAX Development** – KPI measures and a custom **Risk Score** built from tenure, charges, and churn status
5. **Dashboard Design** – KPI cards, charts, slicers, and a decomposition tree assembled into one view
6. **Testing & Validation** – functional testing, DAX validation, filter/cross-filter checks, performance testing

## 🖼 Dashboard Preview

### Full Dashboard View

![Customer Churn Analytics Dashboard](images/dashboard_overview.png)

### Risk Score Logic (DAX)

The customer-level risk score combines tenure, monthly charges, and churn history into a single 0–100 score used to rank the "Top 10 High-Risk Customers" table.

![DAX Risk Score Measure and Power Query Editor](images/dax_measure_and_query_editor.png)

```dax
Risk Score =
VAR TenureScore  = IF(MAX(CustomerChurn[tenure]) < 12, 40, IF(MAX(CustomerChurn[tenure]) < 24, 20, 10))
VAR ChargeScore  = IF(MAX(CustomerChurn[MonthlyCharges]) > 70, 30, IF(MAX(CustomerChurn[MonthlyCharges]) > 30, 20, 10))
VAR ChurnScore   = IF(MAX(CustomerChurn[Churn]) = "Yes", 30, 0)
RETURN
DIVIDE(TenureScore + ChargeScore + ChurnScore, 100)
```

---

## ❓ Questions Answered by the Dashboard

The dashboard was built around real business questions, not just raw numbers. Every question below maps to a specific visual on the dashboard.

### 1. Customer Overview

**1. What is the total number of customers?**
The **Total Customers** KPI card shows the full base tracked in this analysis: **7,032 customers**.

**2. How many customers are currently active?**
The **Active Customers** card shows customers who have not churned — roughly **5,000 active customers** in the current snapshot.

**3. How many customers have churned?**
The remainder of the base — the customers captured by the **Churn Rate** and **Churn Distribution** visuals as "Yes" — represents the churned segment.

**4. What is the overall customer churn rate?**
The **Churn Rate** KPI card gives a single, always-visible answer: **26.58%** of customers have churned.

![KPI Summary Cards](images/kpi_summary_cards.png)

---

### 2. Revenue Analysis

**5. What is the average monthly charge per customer?**
The **Average Monthly Charges** KPI card tracks this directly, currently around **$64.80** per customer.

**6. What is the average total amount paid by customers?**
The **Average Total Charges** card reports the average lifetime billing per customer, around **$2.28K**.

**7. How much revenue is currently at risk due to customer churn?**
The **Revenue at Risk** KPI card converts churned/high-risk customers into a dollar figure — currently **~$12.60K** — so leadership sees churn as a revenue problem, not just a count.

![KPI Summary Cards](images/kpi_summary_cards.png)

---

### 3. Customer Behavior

**8. Which customers are most likely to churn?**
Customers with **short tenure, high monthly charges, and month-to-month contracts** carry the highest calculated Risk Score, and are the ones the dashboard prioritizes.

**9. Who are the Top 10 high-risk customers?**
The **Top 10 High-Risk Customers** table lists individual `customerID`s ranked by Risk Score and Risk Status (e.g., "High"), so retention teams have a ready-made call list.

**10. What is the Risk Score of each customer?**
Every customer has a Risk Score (0–100%) computed from the DAX measure shown above, combining tenure, monthly charges, and churn history into one number, visible directly in the high-risk table.

![Top 10 High-Risk Customers](images/top10_high_risk_customers.png)

---

### 4. Contract Analysis

**11. Which contract type has the highest churn rate?**
**Month-to-Month** contracts show by far the highest churn volume compared to One-Year and Two-Year plans.

**12. Are Month-to-Month customers more likely to churn than One-Year or Two-Year customers?**
Yes. The **Contract Type with Highest Customer Churn** chart shows Month-to-Month customers churning at a much higher rate, while Two-Year contract holders are the most stable segment — reinforcing that contract length itself is protective against churn.

![Contract Type Churn Analysis](images/contract_type_churn.png)

---

### 5. Internet Service Analysis

**13. Which internet service has the highest customer churn?**
**Fiber Optic** customers show the highest churn count among all internet service types.

**14. Does Fiber Optic service experience more churn than DSL?**
Yes. The **Churn by Internet Service** chart shows Fiber Optic churn substantially exceeding DSL churn, suggesting service quality, pricing, or competitive alternatives in the Fiber segment may be driving customers away.

![Internet Service Churn](images/internet_service_churn.png)

---

### 6. Payment Analysis

**15. Which payment method is associated with the highest customer churn?**
**Electronic Check** is associated with the highest churn among all payment methods tracked.

**16. Do customers using Electronic Check churn more frequently?**
Yes. The **Payment Method Distribution** chart shows Electronic Check users churning far more often than customers on Mailed Check, Bank Transfer, or Credit Card (automatic), pointing to payment friction or a less "sticky" billing relationship as a churn driver.

![Payment Method Churn](images/payment_method_churn.png)

---

### 7. Customer Demographics

**17. Does gender affect customer churn?**
The dashboard includes a **Gender** slicer, letting users filter every KPI and chart by gender to compare churn side-by-side; gender is not treated as a strong standalone driver in this analysis, but the filter is available for deeper exploration.

**18. Do senior citizens churn more than younger customers?**
A **Senior Citizen** slicer is available on the filter panel so this segment can be isolated and compared against the overall 26.58% churn rate.

**19. Does having a partner influence customer retention?**
A **Partner** slicer lets users compare churn for customers with vs. without a partner, testing whether household/relationship status affects retention.

**20. Do customers with dependents have lower churn?**
A **Dependents** slicer is included specifically to test this — filtering to "Yes"/"No" re-calculates every KPI live to compare the two groups.

![Demographic Filters Panel](images/demographic_filters_panel.png)

---

### 8. Customer Tenure

**21. Are new customers more likely to churn?**
Yes. The **Customer Churn Trend by Tenure** chart shows churn concentrated heavily in the earliest tenure months, dropping off sharply as tenure increases.

**22. How does customer tenure affect churn probability?**
Churn probability is highest in month 0–1 of tenure, falls quickly through the first year, and stays low and flat for long-tenured customers — tenure is one of the strongest protective factors in the dataset.

**23. Which tenure group experiences the highest churn?**
**Brand-new customers (tenure near 0 months)** show the sharpest churn spike, which is also reflected in the Risk Score formula giving new customers the highest tenure-based penalty.

![Churn Trend by Tenure](images/churn_trend_by_tenure.png)

---

### 9. Billing Analysis

**24. Do customers with higher monthly charges churn more often?**
Yes. The **Churn by Monthly Charges** chart shows churn concentrated in the mid-to-high charge bands, consistent with price sensitivity driving churn decisions.

**25. Is there a relationship between total charges and customer retention?**
Generally, customers with **higher total charges (a proxy for longer tenure and loyalty)** are less likely to churn, while customers with low total charges — typically newer, lower-commitment customers — churn more frequently.

![Churn by Monthly Charges](images/churn_by_monthly_charges.png)

---

### 10. Root Cause Analysis

**26. What are the primary factors contributing to customer churn?**
The three biggest factors identified are: **contract type (month-to-month)**, **internet service (Fiber Optic)**, and **payment method (Electronic Check)** — each independently associated with elevated churn.

**27. Which combination of customer attributes leads to the highest churn?**
Using the **Root Cause Analysis decomposition tree**, drilling from Contract → Internet Service → Payment Method surfaces the single highest-risk combination: **Month-to-Month contract customers**, which the tree automatically expands to as the top contributing path, and can be drilled further to combine with service and payment attributes.

![Root Cause Decomposition Tree](images/root_cause_decomposition_tree.png)

---

### 11. Dashboard & Reporting

**28. How do different filters affect business insights?**
Every KPI card and chart is fully cross-filtered — selecting any slicer (gender, contract, internet service, payment method, partner, senior citizen, dependents) instantly recalculates all visuals, letting users isolate any segment's churn behavior on demand.

**29. Can management analyze churn dynamically using slicers?**
Yes. The left-hand filter panel gives management a point-and-click way to slice the entire dashboard by any customer attribute without touching the underlying data or writing a single query.

**30. Can executives monitor KPIs through a single interactive dashboard?**
Yes. All executive-level KPIs — Churn Rate, Active/Total Customers, Average Charges, Revenue at Risk, and High-Risk Customer count — are consolidated on one screen for at-a-glance monitoring.

**31. What does the dashboard look like end-to-end, filters and all?**
The full assembled view — filters, KPIs, segment charts, the high-risk table, and the root cause tree — is shown together below.

![Full Dashboard with Filters](images/dashboard_overview.png)

---

## 💡 Key Business Insights

- **Month-to-month customers churn the most** compared to one-year and two-year contract holders
- **Fiber Optic users churn more** than DSL or customers with no internet service
- **Electronic Check payers show higher churn** than customers on automatic payment methods
- **Early-tenure customers are at the greatest risk** — churn risk drops sharply after the first year

## ✅ Recommendations

- Strengthen retention programs targeted at month-to-month customers
- Incentivize migration to longer-term contracts
- Enhance support quality for Fiber Optic customers
- Automate ongoing churn monitoring so at-risk customers are flagged early

## 🧠 Skills Demonstrated

- **Technical:** Power Query, DAX, Power BI dashboard design
- **Analytical:** churn analysis, root-cause investigation, KPI definition
- **Business:** translating raw data into a retention strategy stakeholders can act on

## 👤 Author

**Bhati Devamjitsinh K**
📧 bhatidevamjit1776@gmail.com

---

⭐ If you found this project useful, consider giving it a star!
