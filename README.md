# 🎓 Education Loan Comparator — India

A zero-dependency, single-file web calculator that helps Indian students and families compare education loan repayment strategies, optimise Section 80E tax deductions, and evaluate whether taking the loan is better than self-funding.

Open `index.html` directly in any browser — no server, no build step, no npm.

---

## Features

### Three repayment scenarios compared side-by-side

| Scenario | Description |
|---|---|
| **Immediate EMI** | EMI starts from month 1; recalculated at each annual disbursement |
| **PSI + EMI** | Interest-only payments during moratorium, then full EMI |
| **Full Deferral** | No payment during moratorium; interest capitalises, then EMI on inflated principal |

### Staged annual disbursement model
The bank disburses the loan in annual tranches (one per academic year). Interest during moratorium is calculated only on the disbursed amount, not the full sanctioned amount — matching how Indian bank education loans actually work.

### Section 80E tax deduction (Old Regime)
- Interest paid is grouped by **Indian Financial Year (April–March)**
- The 8-year deduction window is counted in FYs from the first FY in which repayment begins
- Tax saving per FY = marginal tax on (taxable income) − marginal tax on (taxable income − interest paid)
- The 80E table updates live when you switch between repayment scenario tabs

### Net interest cost
$$\text{Net Interest Cost} = \text{Total Interest Paid} - \text{80E Tax Savings}$$

### Indian Income Tax (FY 2025-26)
- Old Regime and New Regime slabs
- Standard deduction (₹50,000 old / ₹75,000 new)
- 87A rebate, surcharge, and 4% health & education cess
- Auto-recommend the cheaper regime for your income

### Amortisation schedule with calendar dates
- Full month-by-month schedule for each scenario
- Calendar month/year labels (e.g. "May 2026") derived from the loan start date
- Phase tags: Moratorium vs Repayment
- Inline prepayment inputs — enter lump-sum prepayments in any month; EMI recalculates automatically

### Investment comparison
Shows the opportunity cost: what ₹X would grow to at your expected investment return rate over the same period (compound monthly).

### CSV export
Download the full amortisation schedule for any scenario as a CSV file with metadata header and calendar date column.

---

## Inputs

| Field | Default | Notes |
|---|---|---|
| Annual Gross Income | ₹1.5 Cr | Crore / Lac / Thousand selector |
| Loan Amount | ₹1.5 Cr | Crore / Lac / Thousand selector |
| Annual Interest Rate | 8.5% | Typical range 8–11% |
| Course Duration | 3 yrs | Moratorium = course + 1 yr |
| Repayment Tenure | auto | Auto-set to `max(1, 8 − moratorium years)`; overridable |
| Loan Start Month/Year | current month | Sets calendar labels in schedule |
| Tax Regime | Old (with 80E) | Auto / Old / New |
| Investment Return | 6% p.a. | Expected return on invested principal |

---

## How to use

1. Open `index.html` in a browser
2. Enter your loan amount, income, interest rate, course duration
3. Click **Calculate & Compare Scenarios →**
4. Review the three scenario cards ranked by net interest cost
5. Switch tabs (Immediate EMI / PSI + EMI / Full Deferral) to see the full amortisation schedule and updated 80E analysis
6. Optionally enter prepayments in any schedule row to see the impact
7. Export any schedule to CSV using the **⬇ Export CSV** button

---

## Net Interest Cost explained

1. **Total Interest** — sum of all monthly interest charges across the full loan term
2. **80E Tax Saving** — for each Financial Year in the 8-FY window starting from first repayment, the marginal tax saved by deducting that year's interest paid (Old Regime only)
3. **Net Cost** = Total Interest − 80E Tax Savings — what the loan actually costs after the government subsidises part via the 80E deduction

---

## Technical notes

- Pure HTML + CSS + vanilla JavaScript — no frameworks, no dependencies
- All logic in a single `<script>` block inside `index.html`
- Tax slabs: FY 2025-26 (Old & New Regime)
- Disbursement model: `P/numDisb` released at months 1, 13, 25 … (start of each academic year)
- Indian FY mapping: calendar month ≥ 4 → FY = calendar year; else FY = calendar year − 1
