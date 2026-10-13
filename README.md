# El-Sharnouby Group (LEO MODA): Business Analysis & Sales Forecast

**HVIA Task 02 · Internship project**

An end-to-end analysis of a modeled dataset for a fashion & textile group (production, wholesale, retail and online). The project explores the data, finds the main profit problem, forecasts monthly sales with simple seasonal methods, and tests a pricing what-if.

**Live dashboard:** https://diana9940.github.io/sharnouby/dashboard.html

## Key questions & answers

| Question | Answer |
|---|---|
| Where does the money come from? | Wholesale is **85.3%** of revenue but only **65.7%** of gross profit, at an **11.9%** margin. Retail (37.0%) and Online (34.9%) earn far more per EGP sold. |
| Why is wholesale margin so thin? | Margin falls from **40.5%** (no discount) to **4.0%** (38% discount). Wholesale units per invoice line stay flat (**~31.6**) from a 28% to a 38% discount, so deeper discounts do not buy bigger orders in this data. |
| What happens next? | A seasonal forecast of net sales for **Oct-2026 → Mar-2027**: ~**71.7M EGP** in total, with a **Dec-2026 peak of ~16.2M EGP**. |
| What if wholesale discounts were capped at 30%? | 28,078 wholesale lines (60%) are discounted above 30%. Capping them lifts their gross profit from **17.9M to 34.0M EGP** at the same volume. Profit stays higher unless more than **~47%** of that volume is lost. |

## Other findings

- **Sales:** 421.3M EGP net sales and 64.9M gross profit over Oct-2023 → Sep-2026 (180,000 invoice lines). December is the peak month (14.6M in 2024, 15.6M in 2025); February is the weakest (~8.7M). Alexandria (123M) and Cairo (74M) lead by governorate.
- **Returns:** Online 7.7%, Retail 3.5%, Wholesale 1.8%. About 29% of returns are quality-related; "Size / fit" is the top reason.
- **Customers:** 83.5% of retail buyers order more than once (5.6 orders on average). The top 20% of customers generate 59% of retail revenue.
- **Marketing (ROAS):** Google 10.3, TikTok 4.9, Meta 4.4, Influencer 1.1. WhatsApp/CRM shows ~67, which is most likely attribution of sales from existing customers rather than real incremental impact.
- **Production & quality:** The five lines are similar (~82% efficiency). Bottlenecks are mostly in Sewing (134 orders) and Finishing (109). Defect losses are spread almost evenly across 8 defect types (top 3 = 40%), so there is no single 80/20 fix.
- **Suppliers:** SUP04 (60%) and SUP09 (65%) deliver late far more often than the others (~26–33%).

## Forecast method

Monthly net sales were split into **Wholesale** and **Retail + Online** (36 months of history). Three simple methods were compared on a **6-month hold-out (Apr–Sep 2026)** that the models never saw:

| Method | Wholesale MAPE | Retail + Online MAPE |
|---|---|---|
| Moving Average (3 months) | 17.2% | 19.0% |
| **Seasonal Naive × Growth** (selected) | **3.5%** | **2.4%** |
| Seasonal Index + Trend | 3.5% | 4.6% |

*Seasonal Naive × Growth* = the same month last year × the year-over-year growth rate. The forecast is shown as a range (± the backtest error), not a single number.

## What's inside

```
├── Sharnouby_Analysis_and_Forecast.ipynb   # EDA, forecast, what-if, Power BI export
├── dashboard.html                          # interactive 3-page dashboard (Executive / Discount problem / Forecast)
└── screenshots/                            # dashboard screenshots
```

The dashboard is a single self-contained HTML file (pre-aggregated data, no server needed). Open it in any browser.

## How to run

1. Place the project CSV files in a `data/` folder (the raw data is **not** included in this repo).
2. Install the requirements: `pip install pandas numpy matplotlib seaborn jupyter`
3. Open the notebook and set the data path in the first cell, or run:
   ```bash
   DATA_DIR=data jupyter notebook Sharnouby_Analysis_and_Forecast.ipynb
   ```
4. Run all cells. The notebook creates `charts/` and `powerbi_data/` (clean fact/dimension tables for Power BI).

## Limitations

- The data is **modeled (synthetic)**. Its seasonality is cleaner than real-world data, so the forecast error would be higher in practice.
- 2023 covers only 3 months and 2026 only 9 months, so year-over-year comparisons use matching months.
- The what-if assumes the affected lines are re-priced at the cap and nothing else changes. Real price elasticity is not available in the data, so several volume-loss scenarios are shown.
- Missing values in `Return_Date`, `Defect_Type` and `Primary_Bottleneck` are intentional (no return / defect / bottleneck) and were kept.

## Tools

Python (pandas, NumPy, matplotlib, seaborn), Jupyter, and a single-file HTML/JavaScript dashboard.
I used AI tools as an assistant while building this project, and I reviewed and validated the results myself.
