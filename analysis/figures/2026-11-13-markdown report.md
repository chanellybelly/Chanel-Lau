# FX Hedging Stage 3 — Build Audit Analysis

**Scenario:** 31 — Turbine-Gearbox  
**Date:** November 13, 2026  
**Source specification:** `capabilities/fx-hedging/spec.md`  
**Workbook:** `capabilities/fx-hedging/model.xlsx`

## 1. Purpose and scope

I reviewed the Stage 3 Excel workbook against my Stage 2 specification for a U.S. manufacturer expecting to receive **EUR 9,900,000 in 365 days**. The workbook compares a forward contract, a money-market hedge, and a currency put option. I reviewed the displayed inputs, calculations, scenario table, chart, and validation results. The review below distinguishes numerical checks from presentation issues and from assumptions that will require market verification in Stage 4.

**Review limitation:** The observations below are based on the workbook values and worksheet screenshots reviewed in ChatGPT, alongside independent recalculation of the core outputs. The workbook's displayed PASS indicators are not a substitute for independently testing every Excel formula and named-range reference. Market-rate placeholders have not been verified against live quotations.

## 2. Core calculation checks

| Test | Expected calculation | Result | Assessment |
|---|---|---:|---|
| Forward hedge | 9,900,000 × 1.1807 | **$11,688,930.00** | PASS — matches Stage 2 specification |
| Money-market hedge | [9,900,000 / (1 + 0.035 × 365/360)] × 1.10 × (1 + 0.053 × 365/360) | **$11,081,931.59** | PASS — matches displayed result |
| Put option, base case S_T = 1.10 | 9,900,000 × max(1.10, 1.10) − 9,900,000 × 0.0245 × (1 + 0.053 × 365/360) | **$10,634,416.31** | PASS — matches displayed result |
| Sensitivity | 11 rates, from −5% to +5% of 1.10 | 1.0450–1.1550 | PASS on displayed table; forward and money-market results remain constant |

## 3. Audit findings and follow-up

### Finding 1 — Currency label on euro borrowing amount

- **Area tested:** Money Market Hedge worksheet.
- **Evidence:** The row labeled “Borrow euros today” displayed **$9,560,726.98**, even though the formula computes the present value of the **EUR** receivable.
- **Assessment:** **Presentation/units issue**, not a numerical calculation error. Independent recalculation gives approximately **EUR 9,560,726.98**.
- **Action:** Format this cell with the **€** symbol, keeping the existing formula unchanged.
- **Status:** Identified in reviewed screenshot; correction should be confirmed in the committed workbook.

### Finding 2 — Quoted forward differs from interest-rate-parity forward

- **Area tested:** Money Market Hedge worksheet / market assumptions.
- **Evidence:** Quoted forward = **1.1807 USD/EUR**; interest-rate-parity forward = **1.119387 USD/EUR** (approximately **1.1194**). The workbook flags **REVIEW MARKET ASSUMPTIONS**. The money-market USD settlement is about **$606,998.41** lower than forward proceeds.
- **Assessment:** **Assumption-reconciliation finding**, not proof of a formula error. The spot rate (1.10), U.S. rate (5.30%), and euro rate (3.50%) are expressly provisional inputs from Stage 2, and may not be consistent with the assigned forward rate.
- **Action:** Preserve the review flag and explain the mismatch. Collect and cite date-consistent spot and rate observations in Stage 4; do not force the workbook values to agree by changing the assigned scenario forward rate.
- **Status:** Open pending Stage 4 market verification.

### Finding 3 — Truncated legend descriptions

- **Area tested:** Legend & Workbook Guide worksheet.
- **Evidence:** Several entries in the “Meaning” column were visually cut off in the reviewed screenshot (for example, the description of a placeholder).
- **Assessment:** **Readability/presentation issue**. It could make model conventions unclear to a reviewer but does not change formulas.
- **Action:** Enable Wrap Text and adjust row heights or column widths so every description is readable.
- **Status:** Identified in reviewed screenshot; correction should be confirmed in the committed workbook.

## 4. Other validation observations

- The Inputs worksheet displays ten expected input names, and its six visible input checks report **PASS**. The input values match the Stage 2 specification, including designated placeholders. **Confirm actual named-range definitions in Excel's Formulas → Name Manager**; a text label on a worksheet is not itself proof of a defined name.
- The Forward Hedge worksheet shows a **PASS** result for the **$11,688,930** reference calculation.
- The Sensitivity worksheet displays eleven rates (−5% to +5%), constant forward and money-market proceeds, and increasing net put proceeds above the strike. Its five displayed checks read **PASS**.
- The Option Hedge worksheet shows the put premium financing cost of **$255,583.69**, and a net put receipt of **$10,634,416.31**, consistent with the specified simple-interest ACT/360 convention.
- The call option is presented as a separate reference payoff, not as the primary hedge for the EUR receivable; this agrees with the specification.

## 5. Conclusion and remaining actions

The calculations independently checked above agree with my Stage 2 formulas, and the sensitivity table follows the required scenario pattern. The audit identified two presentation issues and one market-assumption reconciliation issue. Before final Stage 3 submission, I should confirm that the euro symbol and legend formatting have been corrected and that the ten actual named ranges exist and refer to the correct input cells. The quoted/implied forward difference should remain transparently flagged for Stage 4 data verification. These findings do not, on their own, demonstrate a broken hedging formula.

## 6. AI assistance disclosure

I used ChatGPT to help generate the initial Excel model, independently recalculate selected outputs, review screenshots of its worksheets, and draft this audit. I am responsible for checking the workbook in Excel, confirming the observations and corrections, and recording the AI prompts and my decisions in `prompt-log.md`.
