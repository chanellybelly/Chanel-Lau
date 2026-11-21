
# Stage 4: Market Data Memo

**Name:** Chanel Lau
**Scenario:** 31 — Turbine-Gearbox
**Market Data Date:** November 20, 2026

## 1. Purpose

The purpose of this memo is to replace the placeholder
inputs from Stage 3 with actual market data and evaluate
the accuracy and reliability of the FX hedging model.

## 2. Market Data Inputs

| Input | Value | Source | Observation Date |
|---|---:|---|---|
| FC_AMT | EUR 9,900,000 | Assigned Scenario 31 | Scenario-provided |
| S0_in | 1.0990 | European Central Bank | 11/20/2026 |
| F0_in | 1.1807 | Assigned bank quote | Scenario-provided |
| R_USD | 4.51% | U.S. Treasury | 11/20/2026 |
| R_FC | 2.995% | Germany 1-Year Government Bond Yield | 11/20/2026 |
| K_PUT | 1.0990 | Updated spot rate | 11/20/2026 |
| K_CALL | 1.0990 | Updated spot rate | 11/20/2026 |
| PREM_PUT | 0.0245 | Assigned Scenario 31 | Scenario-provided |
| PREM_CALL | 0.0448 | Assigned Scenario 31 | Scenario-provided |
| T_DAYS | 365 | Assigned Scenario 31 | Scenario-provided |

## 3. Market Data Sources

### EUR/USD Spot Rate

Source: European Central Bank

https://www.ecb.europa.eu/stats/policy_and_exchange_rates/euro_reference_exchange_rates/html/index.en.html

Retrieval timestamp: 5:20pm, November 20, 2026

The ECB daily reference rate was selected because it
provides a reliable and publicly available measure of
the EUR/USD exchange rate.

### USD Interest Rate

Source: U.S. Department of the Treasury

https://home.treasury.gov/resource-center/data-chart-center/interest-rates/TextView?field_tdr_date_value=2026&type=daily_treasury_yield_curve

Retrieval timestamp: 5:20pm, November 20, 2026

The one-year U.S. Treasury yield was selected because
its maturity aligns with the 365-day settlement period.

### EUR Interest Rate

Source: Investing.com — Germany 1-Year Government Bond Yield

https://uk.investing.com/rates-bonds/germany-1-year-bond-yield-historical-data

Retrieval timestamp: 5:20pm, November 20, 2026

The German one-year government bond yield was selected
because it is denominated in euros and matches the
settlement period of the receivable.

Both government bond yields serve as proxies for
borrowing and investment rates.

## 4. Assumptions

- The assigned bank forward quote of 1.1807 is retained.
- The put and call strikes are set equal to the updated
  spot rate.
- The original option premiums are retained because
  reliable market option quotes are not readily available.
- The model continues to use the ACT/360 convention.
- The receivable amount and settlement period remain
  unchanged.

## 5. Covered Interest Parity

F_CIP = S0 × (1 + R_USD × T/360)
           / (1 + R_FC × T/360)

The CIP-implied forward will be calculated and compared
with the assigned bank forward quote of 1.1807.

## 6. Workbook Population

Pending workbook update.

## 7. Parity and Sensitivity Checks

Pending workbook validation.

## 8. FX Hedging Lab Cross-Check

Pending comparison with the FX Hedging Lab.

## 9. Conclusion

To be completed after validating the workbook.
