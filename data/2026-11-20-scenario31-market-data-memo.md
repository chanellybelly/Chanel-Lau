
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

Using the updated market inputs and the ACT/360
convention, the CIP-implied forward rate was calculated.

F_CIP = S0 × (1 + R_USD × T/360)
           / (1 + R_FC × T/360)

| Calculation | Result |
|---|---:|
| CIP-implied forward rate | 1.1154 |
| Assigned bank forward rate | 1.1807 |
| Quoted minus implied forward | 0.0653 |
| Money-market vs. forward USD difference | -$646,632.42 |

The parity comparison displays "REVIEW MARKET ASSUMPTIONS"
because the assigned forward rate exceeds the implied
forward rate. This difference may reflect differences in
market observation dates, interest rate proxies, and
bank pricing. The assigned forward quote was retained.

## 6. Workbook Population

The Stage 3 workbook was updated using the selected
market data. The spot rate, USD interest rate, EUR
interest rate, and option strike prices were updated.

The assigned receivable amount, settlement period,
forward quote, and option premiums remained unchanged.

| Hedge Calculation | Updated Result |
|---|---:|
| Forward hedge | $11,688,930.00 |
| Money-market hedge | $11,042,297.58 |
| Gross put-protected proceeds | $10,880,100.00 |
| Financed put premium | $253,640.94 |
| Net put proceeds | $10,626,459.06 |

The updated workbook was saved as model.xlsx.

## 7. Parity and Sensitivity Checks

The sensitivity table was recalculated using 11
exchange rate scenarios ranging from -5% to +5%
of the updated spot rate.

| Validation Check | Result |
|---|---|
| 11 scenarios | PASS |
| Endpoints -5% / +5% | PASS |
| Forward remains fixed | PASS |
| Money-market hedge remains fixed | PASS |
| Put rises above strike | PASS |

The forward and money-market hedge proceeds remained
constant across all scenarios. The put option provided
downside protection while allowing the company to
benefit from favorable exchange rate movements.

## 8. FX Hedging Lab Cross-Check

The updated workbook results were compared with the
FX Hedging Lab using the same scenario inputs.

The forward hedge, money-market hedge, and put option
results were consistent with the workbook calculations.

No significant calculation discrepancies were identified
during the comparison.

## 9. Conclusion

The workbook was successfully populated with updated
market inputs. The hedge calculations were reviewed,
and all five sensitivity checks passed.

The difference between the assigned forward quote and
the CIP-implied forward rate was identified and
documented rather than adjusted.

The updated model provides a foundation for evaluating
the alternative hedging strategies in Stage 5.
