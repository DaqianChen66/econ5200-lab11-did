# econ5200-lab11-did
# Difference-in-Differences: Parallel Trends, Staggered Adoption and the Forbidden Comparison

## Objective

In this lab, I studied how difference-in-differences can fail when parallel trends do not hold, treatment timing differs across groups, or standard errors ignore within-group correlation.

## Methodology

- Reproduced the Card and Krueger minimum-wage difference-in-differences estimate using the original data.
- Simulated a panel with different pre-treatment trends to study violations of the parallel trends assumption.
- Examined two-way fixed effects with staggered treatment adoption.
- Decomposed TWFE into clean and already-treated comparisons.
- Compared iid and state-clustered standard errors.
- Used `did_utils.py` to estimate ATT using not-yet-treated controls.
- Used AI to write a Goodman-Bacon decomposition and checked its output against my own calculations.
- Revised the AI prompt to handle missing outcomes using a balanced panel.

## Key Findings

- The Card and Krueger two-by-two DiD estimate was **2.75** full-time-equivalent employees, close to their published value of +2.76.
- In the parallel-trends example, the true treatment effect was zero, but DiD estimated **1.148** because the treated and control groups had different underlying trends. The pre-period slope difference was **0.194**.
- In the staggered-adoption example, all treatment effects were positive with a true mean effect of **6.71**, but TWFE estimated **-0.99**.
- The forbidden comparison received about **66.7%** of the TWFE weight and produced a negative two-by-two estimate.
- Adding a never-treated group moved the TWFE estimate to **2.67**, but it was still below the true mean effect of 6.71.
- The iid standard error was **8.6 times smaller** than the state-clustered standard error.
- After revising the AI prompt to use a balanced panel, the Goodman-Bacon decomposition matched my calculations exactly. Its weighted sum on the panel with missing outcomes was **2.6735**.

## Files

- `lab-ch11-diagnostic.ipynb` — main notebook with analysis and results
- `src/did_utils.py` — reusable difference-in-differences helper functions

## Main Takeaway

I learned that a DiD regression is only as credible as its research design. Parallel trends, valid comparison groups, treatment-effect heterogeneity, and the level of clustering all matter for causal interpretation.
