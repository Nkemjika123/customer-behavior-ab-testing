## Retail Sales & Customer Insights Experimentation Project

# A/B Testing Simulation

## Table of Contents
- [Project Overview](#project-overview)
- [Business Problem](#business-problem)
- [Experiment Objective](#experiment-objective)
- [Formal Hypothesis](#formal-hypothesis)
- [Primary KPI](#primary-kpi)
- [Audience Segmentation](#audience-segmentation)
- [Treatment Applied](#treatment-applied)
- [Experiment Setup](#experiment-setup)
- [Power BI Dashboard](#power-bi-dashboard)
- [SQL Analysis and Results](#sql-analysis-and-results)
- [Experiment Results](#experiment-results)
- [Result Interpretation](#result-interpretation)
- [Business Recommendation](#business-recommendation)
- [Conclusion](#conclusion)
- [Tools Used](#tools-used)
- [Author](#author)

---

## Project Overview
This project demonstrates how A/B testing can be simulated using a retail sales dataset to support data-driven business decisions.

Instead of only analyzing historical data, the goal is to design and evaluate an experiment that tests whether promotional strategies influence customer purchasing behavior.

This work transitions analytics from descriptive reporting to experimentation and decision-making.

---

## Business Problem
The retail business experiences inconsistent customer purchasing behavior:

- Some customers shop infrequently.
- Others stop purchasing after a short period.
- Revenue growth becomes unstable.
- Customer retention declines.

The business needs to test whether promotional strategies can improve engagement and spending.

---

## Experiment Objective
The experiment aims to determine whether promotional incentives can increase:

- Purchase frequency
- Quantity purchased
- Total revenue generated

Customers are divided into:

- **Group A — Control Group** (no promotional change)
- **Group B — Treatment Group** (receives promotion)

A successful test provides evidence for scaling promotional strategies.

---

## Formal Hypothesis

**Null Hypothesis (H₀):**  
There is no difference in purchasing behavior between customers who receive promotional treatment and those who do not.

**Alternative Hypothesis (H₁):**  
Customers receiving promotional treatment demonstrate higher purchase frequency and spending.

If improvement is observed in Group B, the null hypothesis is rejected.

---

## Primary KPI
The main KPI used is:

### Purchase Frequency per Customer

This measures how often customers make purchases within the test period.

This KPI is chosen because:
- Frequent purchases drive revenue growth.
- It reflects customer engagement.
- It measures repeat buying behavior.

---

## Audience Segmentation
Customers are segmented using **Age Group** and then randomly assigned into experiment groups.

### Group Definition
- Group A: Customers receiving standard experience.
- Group B: Customers assumed to receive promotional incentives.

Random assignment prevents bias and ensures fair comparison.

---

## Treatment Applied
The treatment applied to Group B simulates customers receiving:

- Targeted discounts
- Promotional offers
- Incentives encouraging repeat purchases

Group A receives no promotional change.

Since this uses historical data, the treatment is simulated rather than applied in real time.

---

## Experiment Setup
Steps performed:

1. Integrated transaction, product, store, and customer data.
2. Calculated customer metrics:
   - Purchase frequency
   - Quantity purchased
   - Revenue contribution
3. Randomly assigned customers into Groups A and B.
4. Compared group performance using Power BI visuals.

---

## Power BI Dashboard

An interactive Power BI dashboard was developed to visualize experiment performance and support business decision-making.

The dashboard enables stakeholders to quickly compare experiment outcomes between the control and treatment groups.

### Dashboard Features

The dashboard includes:

- KPI summary cards displaying total revenue, purchase frequency, and quantity purchased.
- Revenue comparison between Group A and Group B.
- Purchase frequency comparison across experiment groups.
- Quantity purchased comparison across groups.
- Interactive filters allowing exploration by customer attributes and product segments.

### Business Value of Dashboard

The dashboard allows decision-makers to:

- Quickly identify which group performs better.
- Monitor experiment KPIs visually.
- Support data-driven promotional decisions.
- Communicate experiment results clearly to non-technical stakeholders.

### Dashboard Preview

<img width="1113" height="664" alt="Screenshot 2026-02-12 125404" src="https://github.com/user-attachments/assets/a3bc6724-135c-4feb-ad8e-869b1b91891c" />

---

## SQL Analysis and Results

| Analysis Step | SQL Query | Result |
|---------------|----------|--------|
| A/B Testing | <pre>UPDATE customer_metrics
SET Experiment_Group =
    CASE
        WHEN RAND() < 0.5 THEN 'Group A'
        ELSE 'Group B'
    END;</pre> | <img width="596" alt="A/B Testing Result" src="https://github.com/user-attachments/assets/b786cf8d-784f-4e3f-8cbe-e05913ab839f" /> |
| Check group size | <pre>SELECT
    Experiment_Group,
    COUNT(*) AS Customers
FROM customer_metrics
GROUP BY Experiment_Group;</pre> | <img width="538" alt="Group Size Result" src="https://github.com/user-attachments/assets/d06d4150-c4e4-441c-93cf-6987d468a43e" /> |
| Compare purchase metrics | <pre>SELECT
    cm.Experiment_Group,
    AVG(cm.Purchase_Frequency) AS Avg_Frequency,
    AVG(cm.Total_Quantity) AS Avg_Quantity
FROM customer_metrics cm
GROUP BY cm.Experiment_Group;</pre> | <img width="702" alt="Purchase Metrics Result" src="https://github.com/user-attachments/assets/5120d18e-c0b5-4e1f-8736-fa8b68d034b8" /> |
| Revenue comparison | <pre>SELECT
    cm.Experiment_Group,
    SUM(t.Quantity * p.UnitPrice) AS Revenue
FROM transactions t
JOIN products p
    ON t.ProductID = p.ProductID
JOIN customer_metrics cm
    ON t.CustomerID = cm.CustomerID
GROUP BY cm.Experiment_Group;</pre> | <img width="766" alt="Revenue Result" src="https://github.com/user-attachments/assets/408d7d7b-9275-4c34-a757-dc19e4966a98" /> |


---

## Experiment Results

| Metric | Group A | Group B |
|---------|---------|---------|
| Customers | 101 | 99 |
| Avg Purchase Frequency | ~25 | ~25 |
| Avg Quantity Purchased | 74.75 | Slightly higher |
| Revenue Generated | 7.73M | 7.74M |
| Quantity Purchased | 7.4K | 7.5K |

### Total Revenue
15.48M across both groups.

Group B slightly outperformed Group A.

---

## Result Interpretation
The treatment group shows marginal improvement in purchasing behavior.

Revenue increased by approximately **0.13%** in Group B compared to Group A.

Although improvement is small, it suggests promotional strategies may positively influence customer behavior.

Further optimization is recommended.

---

## Business Recommendation
The business should:

- Refine promotional strategies
- Conduct further experiments
- Test stronger incentives
- Explore personalized offers

Small improvements scale significantly across large customer bases.

---

## Conclusion
This A/B testing simulation shows how experimentation helps businesses move beyond assumptions toward evidence-based decisions.

By comparing control and treatment groups, organizations can adopt strategies that improve retention, engagement, and profitability.

---

## Tools Used
- MySQL (Data preparation & aggregation)
- Power BI (Visualization & comparison)
- SQL (Customer metrics & experiment setup)
- Excel (Initial data inspection)

---

## Author
**Nkemjika Princess Onwubuche**  
Data Analyst | Mentor | Analytics Coach
