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
- [Questions This Dashboard Answers](#-questions-this-dashboard-answers)
- [Key Business Insights](#-key-business-insights)
- [Recommendations](#-recommendations)
- [Skills Demonstrated](#-skills-demonstrated)
- [Author](#-author)

---

## 🧩 Introduction

Customer churn — when a customer stops doing business with a company — is one of the most expensive problems in subscription-based industries like telecom. Acquiring a new customer costs far more than keeping an existing one, so knowing **who is likely to leave and why** is a direct lever on revenue.

This project turns a raw telecom customer dataset into an interactive Power BI dashboard that surfaces churn patterns, flags high-risk customers, and quantifies the revenue at stake, giving business teams a self-service tool instead of a static spreadsheet.

## 🎯 What This Project Does

The dashboard takes 7,000+ customer records and transforms them into:

- A live view of **overall churn rate** and how it moves across customer segments
- A **risk score** for every customer, so the highest-risk accounts surface automatically
- Drill-down analysis (via a decomposition tree) into **why** a customer is likely to churn
- A clear picture of **revenue at risk**, not just customer counts

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
- **Attributes include:** demographics, contract type, internet service, payment method, tenure, monthly charges, and churn status

## 🔄 Project Workflow

1. **Data Collection** – CSV imported into Power BI and validated for completeness
2. **Data Cleaning** – handled in Power Query: data types corrected, blanks and duplicates resolved
3. **Data Modeling** – single-table model, all logic handled through DAX measures
4. **DAX Development** – KPI measures and a custom **Risk Score** built from tenure, charges, and churn status
5. **Dashboard Design** – KPI cards, charts, slicers, and a decomposition tree assembled into one view
6. **Testing & Validation** – functional testing, DAX validation, filter/cross-filter checks, performance testing

## 🖼 Dashboard Preview

### Full Dashboard View

The main view combines executive KPIs with segment-level churn analysis and a prioritized high-risk customer list.

![Customer Churn Analytics Dashboard](images/dashboard_overview.png)

**What's on it:**
- KPI cards — Churn Rate, Active Customers, Total Customers, Average Charges, Revenue at Risk, High-Risk Customers
- Contract Type churn breakdown
- Churn by Internet Service and Payment Method
- Customer Churn Distribution (donut)
- Top 10 High-Risk Customers table, ranked by risk score
- Root Cause Analysis decomposition tree
- Churn trend by Tenure and by Monthly Charges

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

## ❓ Questions This Dashboard Answers

The dashboard was designed around real business questions rather than just displaying numbers:

1. **What percentage of our customers are churning right now?**
2. **How much revenue is at risk from customers likely to leave?**
3. **Which contract type (month-to-month, one-year, two-year) has the highest churn?**
4. **Does internet service type (Fiber Optic vs. DSL) affect churn?**
5. **Which payment method is associated with the highest churn?**
6. **Who are the top 10 highest-risk customers we should contact first?**
7. **At what point in a customer's tenure is churn risk highest?**
8. **Does a customer's monthly charge level correlate with their likelihood to churn?**
9. **What is the root cause behind churn when we drill down by contract, service, and payment method together?**
10. **Which customer segments should retention campaigns prioritize first?**

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
