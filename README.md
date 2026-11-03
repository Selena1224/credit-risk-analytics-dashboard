# Credit Risk Analytics & Decision Support

🌐 **[View Interactive Project Website](https://selena1224.github.io/credit-risk-analytics-dashboard/)**

📊 **[Download Full Power BI Dashboard](Deliverables/Credit_Risk_Dashboard.pbix)**

📑 **[View Management Presentation](Deliverables/Credit_Risk_Management_Presentation.pptx)**

---

**The question isn't just who looks risky. It's where a lender should spend more review time—and whether that extra review is worth it.**

I used **Python, machine learning, and Power BI** to analyze **425 historical borrowers**, compare predictive models, and develop a decision-support dashboard. My conclusion: **target review effort, measure the trade-offs, and validate the approach before changing lending policy.**

**425** historical borrowers · **211** labeled high risk (49.6%) · **85** holdout test cases · **10** new borrowers scored

## Three findings that matter for lending decisions

### 1. Similar loan volumes concealed very different risk concentrations

| Loan purpose | Borrowers | High-risk labels | High-risk rate |
|---|---:|---:|---:|
| **New Car** | 104 | **65** | **62.5%** |
| Small Appliance | 105 | 42 | 40.0% |

**Nearly the same volume, but 23 more high-risk classifications for New Car.** Instead of restricting every segment, **investigate New Car first**. A high rate from a tiny sample is not automatically a higher priority.

### 2. Longer customer relationships did not mean lower risk

Borrowers with **0–12 months** of relationship history had a **22.7%** high-risk rate; those with **more than 48 months** had a **74.2%** rate. The association was statistically significant (**chi-square p < 0.001**).

**Implication:** Customer tenure should not be treated as a shortcut for creditworthiness. This is an association, not evidence of causation.

### 3. A simple savings rule would miss the bigger picture

High-risk labels appeared in **26.5%** of borrowers with positive checking but no savings (**n=49**) and **56.0%** of borrowers with both balances positive (**n=125**).

**Implication:** A single balance cutoff would be misleading; review should consider multiple financial indicators and repayment capacity.

## The model's mistakes matter more than its accuracy

I compared **Logistic Regression** and **Random Forest**, including an overfitting-controlled forest. Although Random Forest performed better on one holdout split, Logistic Regression had stronger **five-fold cross-validation** results and was chosen as the model for further evaluation.

| Logistic Regression: holdout results | Outcome |
|---|---:|
| Correct classifications | **54 of 85 (63.5%)** |
| High-risk cases correctly identified | **26 of 42 (61.9% recall)** |
| High-risk cases missed | **16** |
| Lower-risk cases incorrectly flagged | **15** |

**The real question:** How much risk might be missed, and how many other borrowers might face unnecessary review? With these results, **automatic lending decisions are not justified**.

### One threshold change, a different workload

The Power BI dashboard simulates an additional-review queue using **10 new borrowers**:

| Risk-score threshold | Flagged for review |
|---|---:|
| **45%** | **5 of 10** |
| **50%** | **4 of 10** |
| **60%** | **3 of 10** |

One borrower scored **48.4%**: flagged at 45%, not flagged at 50%. **Moving the threshold changes the queue; it does not establish the safest lending policy.**

## Recommendation: a 90-day shadow pilot

**Test the review process without changing actual lending decisions.**

- **Days 1–30 — Validate:** Check model errors, data quality, and fairness.
- **Days 31–60 — Shadow-test:** Record suggested review routes and workload alongside existing decisions.
- **Days 61–90 — Evaluate:** Assess missed risk, unnecessary reviews, staff effort, and borrower impact; **continue, revise, or stop**.

**Goal:** Concentrate underwriting attention where it may add value while avoiding extra friction elsewhere.

## Explore the work

**Final deliverables:** [Power BI Dashboard](Deliverables/Credit_Risk_Dashboard.pbix) · [Management Presentation](Deliverables/Credit_Risk_Management_Presentation.pptx)

**Python workflow:** [01 · Understand](01_Data_Understanding.ipynb) → [02 · Clean](02_Data_Cleaning.ipynb) → [03 · Explore](03_Exploratory_Data_Analysis.ipynb) → [04 · Test Patterns](04_Advanced_Analysis.ipynb) → [05 · Model & Export](05_Credit_Risk_Modeling.ipynb)

**Data:** [Source workbook](Data/Credit_Risk_Data.xlsx) · [Dashboard-ready datasets](Dashboard_Data/)

**Tools:** Python, pandas, scikit-learn, SciPy, Matplotlib, Seaborn, Power BI. To reproduce the analysis, open the notebooks from the repository root, run them in numbered order, and ensure `Data/Credit_Risk_Data.xlsx` is present. Open the `.pbix` file in Power BI Desktop.

---

**Scope:** Historical *credit-risk labels are not observed defaults*. This dataset does not measure actual repayments, profitability, or the impact of alternative loan terms. Real lending deployment would require outcome-based validation, affordability and fairness assessments, and human oversight.
