# Immediate Annuity Valuation & Reserve Model

![Excel](https://img.shields.io/badge/Built%20with-Microsoft%20Excel-217346?logo=microsoft-excel&logoColor=white)
![Actuarial](https://img.shields.io/badge/Domain-Actuarial%20Science-blue)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

📥 [**File**] https://d.docs.live.net/E4C07FCDD03F54CF/Documents/Annuity%20Valuation%20and%20Reserve%20Model.xlsx

An Excel-based actuarial model that prices a single-life immediate annuity and builds its duration-by-duration prospective reserve schedule, using a real published mortality table.

## Author
Ishita Narang

## Overview
This project builds a working actuarial model for an **immediate annuity in payment** — a pension-payout / annuity-certificate product. In exchange for a single premium (the Net Single Premium, or NSP), the insurer pays the annuitant a fixed income for as long as they are alive.

The model:
- Derives commutation functions (lx, Dx, Nx) from first principles
- Prices the annuity using the annuity-due factor (ax = Nx / Dx)
- Builds a full duration-by-duration prospective reserve schedule
- Tests sensitivity of the premium and reserve to the valuation interest rate

All calculations are formula-driven and linked to a single Assumptions tab, so changing any input (age, payment amount, interest rate) recalculates the entire model automatically.

## Key Findings
At the base case (annuitization age 60, annual payment of Rs. 120,000, valuation rate of 6%):

| Metric | Value |
|---|---|
| Annuity-due factor (ax₀) | 12.69 |
| Net Single Premium (NSP) | Rs. 1,523,170 |
| Reserve at duration 0 (V₀) | Rs. 1,523,170 (= NSP) |
| Reserve at duration 30 (age 90) | Rs. 506,390 (33.2% of V₀) |

**Interest rate sensitivity** (NSP at age 60):

| Scenario | Rate | NSP (Rs.) | Change vs Base |
|---|---|---|---|
| Low | 4% | 1,838,138 | +20.7% |
| Base | 6% | 1,523,170 | — |
| High | 8% | 1,294,074 | −15.0% |

**Interpretation:** The reserve is largest at outset (equal to the NSP) and runs off toward zero as the annuitant ages, since fewer years of expected payments remain. A higher valuation interest rate discounts future payments more heavily, lowering both the annuity factor and the NSP and therefore the reserve the insurer must hold at every duration. This sensitivity is one of the largest drivers of an annuity provider's pricing and reserving risk, which is why regulators typically prescribe the valuation rate rather than leaving it to insurer discretion.

## Policyholder Profile
The base-case policyholder assumptions used throughout the model:

| Item | Value |
|---|---|
| Age at annuitization (x₀) | 60 |
| Annual annuity payment | Rs. 120,000 (payable annually in advance) |
| Radix (l₂₀) | 100,000 |
| Base valuation interest rate | 6% |
| Low sensitivity scenario | 4% |
| High sensitivity scenario | 8% |

All input cells are editable, so the model can be re-run for any age between 20 and 115 or any payment amount.

## Methodology
1. **Mortality basis** — The [Indian Individual Annuitants' Mortality Table (2012-15)](https://www.actuariesindia.org), published by the Institute of Actuaries of India (IAI) and effective 1 April 2021. It's based on the pooled experience of 24 insurers from April 2012–March 2015 (graduated overall/combined qx rates, ages 20–115).
2. **Commutation functions** — Starting from the radix (l₂₀ = 100,000), survivors (lx) are propagated forward using qx/px. Each lx is discounted at the valuation rate to give Dx = lx × v^x, and Nx is the running total of Dx from age x to the oldest age in the table (115).
3. **Annuity valuation** — The annuity-due factor is ax = Nx / Dx, representing the present value per Re. 1 of a whole-life annuity-due (first payment immediate, then annually while the annuitant survives). NSP = Annual Payment × ax₀.
4. **Reserve schedule** — At each future duration t, the prospective reserve is V_t = Payment × a(x₀+t), i.e., the present value of annuity payments still expected for a survivor then aged (x₀+t). V₀ equals the NSP by construction, and the reserve runs off to zero as the annuitant approaches the table's oldest age.
5. **Sensitivity analysis** — Dx and Nx are rebuilt in parallel at a Low (4%) and High (8%) discount rate (lx is unchanged, since survivorship doesn't depend on the interest rate), so Base/Low/High results sit side by side.

**Sheets in the workbook:**
- **Cover & Instructions** — project objective, background, and build guide
- **Assumptions** — all editable inputs (policy profile, payment, interest rates)
- **Mortality Table** — published qx/px rates, ages 20–115
- **Commutation Functions** — lx, Dx, Nx built from the radix and valuation rate
- **Annuity Valuation** — ax and NSP at the base case, plus a comparison across ages 55–80
- **Reserve Schedule** — full duration-by-duration prospective reserve run-off
- **Sensitivity Analysis** — parallel Dx/Nx tables at Low, Base, and High interest rates
- **Dashboard** — chart data feeding the visualizations
- **chart** — reserve run-off curve, annuity factor by age, and NSP sensitivity bar chart
- **Summary** — one-page executive summary of inputs, results, and interpretation

## Visualizations

### Reserve Run-off by Duration
Reserve declines from the Net Single Premium toward zero as the annuitant ages and fewer years of expected payments remain.

![Reserve Run-off by Duration]<img width="196" height="107" alt="reserve runoff by duration" src="https://github.com/user-attachments/assets/b21aa86e-cdec-41c6-a826-74670def2f7b" />


### Annuity-due Factor (ax) by Age
The annuity factor falls as annuitization age increases, reflecting a shorter expected payment stream.

![Annuity-due Factor (ax) by Age]<img width="198" height="106" alt="annuity due factor by age" src="https://github.com/user-attachments/assets/27fd4845-a538-4abf-b3da-c9b1d49e58bb" />


### NSP Sensitivity to Valuation Rate
A higher valuation interest rate discounts future payments more heavily, lowering the Net Single Premium; a lower rate has the opposite effect.

![NSP Sensitivity to Valuation Rate]<img width="198" height="109" alt="NSP Senstivity to valuation Rate" src="https://github.com/user-attachments/assets/e09c1337-13a7-44f3-8b8a-c3c6693c4d2f" />


## What I Learned
- How to build commutation functions (lx, Dx, Nx) from a real published mortality table, rather than a simplified textbook example
- The mechanics of prospective reserving — why reserves are largest at policy inception and run off over time
- How sensitive annuity pricing and reserving is to the valuation interest rate, and why regulators tend to prescribe this rate rather than leaving it to insurer judgment
- How to structure a fully formula-linked Excel model so that a single change in the Assumptions tab flows through every downstream calculation and chart

## Limitations
- Uses a single, published mortality table (IALM 2012-15) rather than insurer-specific or updated experience data
- Assumes a level, single-life annuity-due with no guarantee period, joint-life option, or inflation indexation
- Valuation interest rate is treated as flat (not a full yield curve) and constant over time
- Does not model expenses, profit margins, or regulatory solvency margin requirements on top of the actuarial reserve
- No allowance for mortality improvement over time (static table only)

## Contact
ishita.narang05@gmail.com

---
