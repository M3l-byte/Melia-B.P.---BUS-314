**TECHNICAL SPECIFICATION — STAGE 3**

Walmart Inc. (WMT) — FY2025 Financial Ratio Analysis

| Spec Title | WMT FY2025 Financial Ratio Analysis — Technical Specification |
| :---- | :---- |
| **Created by** | Melia Belmes-Picache |
| **Updated by** | Melia Belmes-Picache |
| **Date Created** | April 15, 2026 |
| **Version** | 1.0 |
| **LLM Used** | Claude Sonnet 4.6 (Anthropic) |
| **Role** | Financial Analyst / FP\&A Analyst |
| **Audience** | CFO or Director of FP\&A |

**1\. Problem Statement**

Walmart Inc. (NYSE: WMT) is a publicly traded multinational retailer operating in mass-market retail, grocery, and e-commerce across 19 countries. This specification documents the analytical framework for computing 29 accounting and performance ratios from Walmart's FY2025 financial statements (fiscal year ended January 31, 2025), enabling management to assess financial health, operational efficiency, capital structure, and value creation relative to FY2024.

The analysis supports a CFO-level briefing with five objectives: evaluate return on capital and equity; measure asset productivity and operating margins; quantify leverage and coverage risk; assess short-term liquidity; and decompose ROE via Du Pont analysis. Results will feed directly into the Stage 4 AI prompt and final executive report.

**2\. Inputs (Known Variables)**

*All figures in USD millions. Sources: WMT FY2025 Form 10-K and Q4 FY2025 Earnings Release (Form 8-K, Exhibit 99.1), filed February 20, 2025\.*

**Balance Sheet Items (FY2025 \= current year; FY2024 \= start-of-year)**

| Variable | Named Range | FY2025 ($M) | FY2024 ($M) |
| ----- | ----- | ----- | ----- |
| Cash & cash equivalents | BAL\_cash\_FY25 / FY24 | 9,300 | 8,625 |
| Receivables, net | BAL\_receivables\_FY25 / FY24 | 8,796 | 7,933 |
| Inventories | BAL\_inventories\_FY25 / FY24 | 56,435 | 56,576 |
| Total Current Assets | BAL\_assets\_current\_FY25 / FY24 | 77,458 | 75,655 |
| Net PP\&E | BAL\_ppe\_net\_FY25 | 110,810 | 100,760 |
| Total Assets | BAL\_assets\_total\_FY25 / FY24 | 252,980 | 243,197 |
| Total Current Liabilities | BAL\_liabilities\_current\_FY25 / FY24 | 92,415 | 92,198 |
| Long-term debt | BAL\_debt\_long\_term\_FY25 / FY24 | 36,132 | 34,649 |
| Total Liabilities | BAL\_liabilities\_total\_FY25 | 160,362 | 157,748 |
| Shareholders' Equity (Walmart) | BAL\_equity\_shareholders\_FY25 / FY24 | 83,861 | 76,693 |

**Income Statement Items**

| Variable | Named Range | FY2025 ($M) |
| ----- | ----- | ----- |
| Net sales | INC\_sales | 680,985 |
| Cost of sales | INC\_cost\_goods\_sold | 511,753 |
| SG\&A expenses | INC\_sga | 139,884 |
| Depreciation & amort. | INC\_depreciation | 12,978 |
| Operating Income (EBIT) | INC\_ebit | 29,348 |
| Interest expense | INC\_interest\_expense | (2,728) |
| Income taxes | INC\_taxes | 6,152 |
| Net Income (Walmart) | INC\_net | 19,436 |
| Dividends paid | INC\_dividends | 6,640 |

**Cash Flow Statement Items**

| Variable | Named Range | FY2025 ($M) |
| ----- | ----- | ----- |
| Cash from operations | CASH\_operating | 36,400 |
| Capital expenditures | CASH\_capex | (23,740) |
| Cash from investing | CASH\_investments | (25,501) |
| Free Cash Flow | CASH\_free | 12,660 |

**Market / Analyst Inputs**

| Variable | Named Range | Value / Source |
| ----- | ----- | ----- |
| Share price (Jan 31, 2025\) | share\_price | $95.28 — market close, fiscal year-end |
| Shares outstanding (diluted) | shares\_outstanding | 8,081M — FY2025 10-K |
| Cost of capital (WACC) | cost\_capital | 7.60% — estimated; see §3 |
| Effective tax rate | tax\_rate | 23.38% — FY2025 effective rate, 10-K |

**3\. Assumptions & Constraints**

* All figures in USD millions unless noted.

* Effective tax rate of 23.38% taken directly from FY2025 10-K income tax disclosure; statutory 21% rate was not used.

* WACC estimated at 7.60% using a simplified approach (beta \~0.55, risk-free rate \~4.3%, Walmart capital structure). Should be replaced with a full bottom-up WACC build for production use.

* Share price of $95.28 reflects the NASDAQ closing price on January 31, 2025 — the final trading day of the fiscal year.

* Depreciation sourced from Cash Flow Statement adjustments ($12,978M); includes amortization. A standalone depreciation line from the PP\&E schedule would be more precise.

* Start-of-year denominator values use the FY2024 ending Balance Sheet as the beginning of FY2025.

* Interest expense entered as −$2,728M per the Income Statement; ABS() applied in TIE and Cash Coverage formulas.

* Long-term debt in leverage ratios refers to non-current LT debt ($36,132M); current portion ($3,447M) is excluded.

* No off-balance-sheet items beyond ASC 842 lease obligations, which are on-balance-sheet and included in total liabilities.

* After-tax operating income (ATOI) \= INC\_ebit × (1 − tax\_rate), consistent with academic convention.

**4\. Calculation Flow**

Ratios are computed in the following sequence so all dependencies resolve before first use.

**Step 1 — Derived Inputs**

market\_capitalization  \= share\_price × shares\_outstanding  →  $769,958M

currentYear\_ATOI  \= INC\_ebit × (1 − tax\_rate)  →  $22,486M

currentYear\_daily\_sales  \= INC\_sales / 365  →  $1,866M/day

currentYear\_working\_capital  \= BAL\_assets\_current\_FY25 − BAL\_liabilities\_current\_FY25  →  −$14,957M

startYear\_total\_capitalization  \= startYear\_long\_term\_debt \+ startYear\_equity  →  $111,342M

avg\_equity  \= AVERAGE(startYear\_equity, currentYear\_equity)  →  $80,277M

avg\_total\_assets  \= AVERAGE(startYear\_total\_assets, currentYear\_total\_assets)  →  $248,089M

avg\_total\_capitalization  \= AVERAGE(startYear\_total\_cap, currentYear\_total\_cap)  →  $115,668M

**Step 2 — Performance Ratios**

ratio\_MVA  \= market\_capitalization − currentYear\_equity

ratio\_market\_to\_book  \= market\_capitalization / currentYear\_equity

ratio\_EVA  \= currentYear\_ATOI − (cost\_capital × startYear\_total\_capitalization)

**Step 3 — Profitability Ratios**

ratio\_ROA\_start  \= currentYear\_ATOI / startYear\_total\_assets

ratio\_ROC\_start  \= currentYear\_ATOI / startYear\_total\_capitalization

ratio\_ROE\_start  \= INC\_net / startYear\_equity   (repeat with avg denominators)

**Step 4 — Efficiency Ratios**

ratio\_asset\_turnover  \= INC\_sales / startYear\_total\_assets

ratio\_receivables\_turnover  \= INC\_sales / startYear\_receivables  →  Avg Collection Period \= 365 / turnover

ratio\_inventory\_turnover  \= INC\_cost\_goods\_sold / startYear\_inventories  →  Days in Inventory \= 365 / turnover

margins  \= INC\_net | INC\_ebit | gross\_profit  / INC\_sales

**Step 5 — Leverage Ratios**

ratio\_lt\_debt\_ratio  \= BAL\_debt\_long\_term / (BAL\_debt\_long\_term \+ BAL\_equity\_shareholders)

ratio\_debt\_equity  \= BAL\_debt\_long\_term / BAL\_equity\_shareholders

ratio\_total\_debt  \= (BAL\_assets\_total − BAL\_equity\_shareholders) / BAL\_assets\_total

ratio\_times\_interest\_earned  \= INC\_ebit / ABS(INC\_interest\_expense)

ratio\_cash\_coverage  \= (INC\_ebit \+ INC\_depreciation) / ABS(INC\_interest\_expense)

ratio\_debt\_burden  \= (INC\_ebit \+ INC\_interest\_expense) / INC\_ebit

ratio\_leverage  \= BAL\_assets\_total / BAL\_equity\_shareholders

**Step 6 — Liquidity Ratios**

ratio\_nwc\_to\_assets  \= currentYear\_working\_capital / BAL\_assets\_total

ratio\_current  \= BAL\_assets\_current / BAL\_liabilities\_current

ratio\_quick  \= (BAL\_assets\_current − BAL\_inventories) / BAL\_liabilities\_current

ratio\_cash  \= BAL\_cash / BAL\_liabilities\_current

**Step 7 — Du Pont Decomposition**

dupont\_ROA  \= dupont\_asset\_turnover × dupont\_op\_margin

dupont\_ROE  \= dupont\_leverage × dupont\_asset\_turnover × dupont\_op\_margin × dupont\_debt\_burden × dupont\_tax\_burden

*Validation: Du Pont ROE (25.30%) matches direct ROE (25.34%) within 4 bps — confirming decomposition integrity. Du Pont ROA (12.07%) intentionally diverges from direct ROA (9.25%) because it uses EBIT-based operating margin rather than after-tax operating income; this is a known design choice documented in §6.*

**5\. Outputs**

| Ratio | Named Range | FY2025 | Formula (Named-Range Notation) |
| ----- | ----- | ----- | ----- |
| **Performance Ratios** |  |  |  |
| Market Value Added (MVA) | ratio\_MVA | $686,097M | market\_capitalization − currentYear\_equity |
| Market-to-Book | ratio\_market\_to\_book | 9.18× | market\_capitalization / currentYear\_equity |
| Economic Value Added (EVA) | ratio\_EVA | $14,024M | currentYear\_ATOI − (cost\_capital × startYear\_total\_capitalization) |
| **Profitability — Start-of-Year** |  |  |  |
| ROA (start-of-year) | ratio\_ROA\_start | 9.25% | currentYear\_ATOI / startYear\_total\_assets |
| ROC (start-of-year) | ratio\_ROC\_start | 20.20% | currentYear\_ATOI / startYear\_total\_capitalization |
| ROE (start-of-year) | ratio\_ROE\_start | 25.34% | INC\_net / startYear\_equity |
| **Profitability — Average Denominators** |  |  |  |
| ROA (average) | ratio\_ROA\_avg | 9.06% | currentYear\_ATOI / avg\_total\_assets |
| ROC (average) | ratio\_ROC\_avg | 19.44% | currentYear\_ATOI / avg\_total\_capitalization |
| ROE (average) | ratio\_ROE\_avg | 24.21% | INC\_net / avg\_equity |
| **Efficiency Ratios** |  |  |  |
| Asset Turnover | ratio\_asset\_turnover | 2.80× | INC\_sales / startYear\_total\_assets |
| Receivables Turnover | ratio\_receivables\_turnover | 85.84× | INC\_sales / startYear\_receivables |
| Avg Collection Period (days) | ratio\_avg\_collection\_period | 4.3 days | 365 / ratio\_receivables\_turnover |
| Inventory Turnover | ratio\_inventory\_turnover | 9.05× | INC\_cost\_goods\_sold / startYear\_inventories |
| Days in Inventory | ratio\_days\_in\_inventory | 40.4 days | 365 / ratio\_inventory\_turnover |
| Net Profit Margin | ratio\_profit\_margin | 2.85% | INC\_net / INC\_sales |
| Operating Profit Margin | ratio\_operating\_profit\_margin | 4.31% | INC\_ebit / INC\_sales |
| Gross Profit Margin | ratio\_gross\_margin | 24.85% | (INC\_sales − INC\_cost\_goods\_sold) / INC\_sales |
| **Leverage Ratios** |  |  |  |
| Long-Term Debt Ratio | ratio\_lt\_debt\_ratio | 30.11% | BAL\_debt\_long\_term / (BAL\_debt\_long\_term \+ BAL\_equity\_shareholders) |
| Debt-to-Equity Ratio | ratio\_debt\_equity | 0.43× | BAL\_debt\_long\_term / BAL\_equity\_shareholders |
| Total Debt Ratio | ratio\_total\_debt | 66.85% | (BAL\_assets\_total − BAL\_equity\_shareholders) / BAL\_assets\_total |
| Times Interest Earned | ratio\_times\_interest\_earned | 10.76× | INC\_ebit / ABS(INC\_interest\_expense) |
| Cash Coverage | ratio\_cash\_coverage | 15.52× | (INC\_ebit \+ INC\_depreciation) / ABS(INC\_interest\_expense) |
| Debt Burden | ratio\_debt\_burden | 0.907× | (INC\_ebit \+ INC\_interest\_expense) / INC\_ebit |
| Leverage Ratio | ratio\_leverage | 3.02× | BAL\_assets\_total / BAL\_equity\_shareholders |
| **Liquidity Ratios** |  |  |  |
| NWC-to-Assets | ratio\_nwc\_to\_assets | −5.91% | currentYear\_working\_capital\_net / BAL\_assets\_total |
| Current Ratio | ratio\_current | 0.84× | BAL\_assets\_current / BAL\_liabilities\_current |
| Quick Ratio | ratio\_quick | 0.23× | (BAL\_assets\_current − BAL\_inventories) / BAL\_liabilities\_current |
| Cash Ratio | ratio\_cash | 0.10× | BAL\_cash / BAL\_liabilities\_current |
| **Du Pont Decomposition** |  |  |  |
| Du Pont ROA | dupont\_ROA | 12.07% | dupont\_asset\_turnover × dupont\_op\_margin |
| Du Pont ROE | dupont\_ROE | 25.30% | dupont\_leverage × dupont\_asset\_turnover × dupont\_op\_margin × dupont\_debt\_burden × dupont\_tax\_burden |

*The model also produces: a color-coded inputs/outputs layer (yellow \= raw inputs, blue \= assumptions, green \= cross-sheet links, gray \= computed outputs); named-range formula documentation column alongside each ratio; and a Du Pont component breakdown showing each multiplicative driver.*

**6\. Model Review — What Worked & What to Improve**

**What Worked Well**

* All 29 ratios computed with zero formula errors after LibreOffice recalculation — no \#REF\!, \#DIV/0\!, or \#NAME? errors in the delivered file.

* Named-range convention makes every formula self-documenting: startYear\_equity, ratio\_ROA\_start, dupont\_leverage can be read as plain English without reference to cell addresses.

* Dual-denominator approach (start-of-year and average) produces the expected pattern: start-of-year ROA (9.25%) is slightly higher than average ROA (9.06%), reflecting asset growth during the year.

* Du Pont ROE (25.30%) matches directly computed ROE (25.34%) within 4 basis points, confirming the five-factor decomposition is internally consistent.

* Color coding applied consistently throughout all five tabs, making the input layer immediately distinguishable from formula outputs.

**What to Improve**

* Du Pont ROA (12.07%) diverges from direct ROA (9.25%) because the Du Pont path uses EBIT-based operating margin, not after-tax operating income. A rigorous version would apply the tax burden factor within the ROA decomposition — or use a consistent income concept throughout all paths.

* Depreciation ($12,978M) is taken from the Cash Flow adjustments line and bundles amortization. Isolating pure depreciation from the PP\&E rollforward schedule would improve Cash Coverage precision.

* Model total assets ($252,980M) differ slightly from the 10-K reported figure ($252,399M) due to minor reclassification differences in summing individual line items. A reconciliation check row should be added.

* WACC (7.60%) is a simplified estimate. A full bottom-up build — CAPM for cost of equity, after-tax cost of debt from the 10-K, market-value weights — would make EVA ($14,024M) more defensible for a CFO audience.

* Single-year scope limits trend interpretation. Adding FY2023 as a second prior year would enable a three-period view of margin compression, asset growth, and leverage trajectory.

* No peer benchmarking. A second ratios tab comparing Walmart to Target (TGT) and Costco (COST) on key efficiency and margin ratios would substantially increase the CFO memo's analytical value.

**7\. Limitations & Next Steps**

This specification does not incorporate industry peer comparisons, multi-year trend analysis beyond FY2024 vs. FY2025, or off-balance-sheet items beyond those required by ASC 842\. WACC is an approximation. Ratio interpretation — including commentary on what each figure implies for Walmart's competitive position and capital allocation — is reserved for Stage 4\.

The Stage 4 final analysis will use this specification as the direct input to a structured AI prompt. Named ranges defined here will serve as exact variable names, enabling the AI to generate auditable formulas, interpret results in context, and produce a polished executive-ready analysis for the CFO.

*Source: Walmart Inc. FY2025 Form 10-K and Q4 Earnings Release (Form 8-K), filed with the SEC on or around February 20, 2025\. EDGAR: https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany\&CIK=0000104169\&type=10-K*