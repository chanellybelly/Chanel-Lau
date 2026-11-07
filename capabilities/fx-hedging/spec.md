# FX Hedging Model Specification

## 1. Problem Statement

The purpose of this model is to understand how a U.S. wind-turbine gearbox manufacturer can manage the risks that come with changes in foreign exchange rates. In this situation, the company has invoiced a Spanish renewable-power developer for EUR 9,900,000 and expects to receive the payment in 365 days. Since the payment will be made in euros, the company will eventually need to convert the money into U.S. dollars.

One of the main concerns is that exchange rates can change over time. If the euro weakens against the U.S. dollar before the payment is received, the company could end up receiving fewer U.S. dollars than expected. This could negatively affect its cash flows and profitability.

To help manage this risk, the model will compare three different hedging strategies: a forward contract, a money-market hedge, and a currency put option. Each strategy offers a different way to protect the company's cash flows while considering the potential benefits and costs.

The model will calculate how much the company could receive in U.S. dollars under each strategy and examine how the results change under different exchange rates. By comparing these strategies, the company can better understand which approach may be the most beneficial based on its financial needs and level of risk.

**Scenario Details:**
- Scenario: 31 — Turbine-Gearbox
- Company: U.S. wind-turbine gearbox manufacturer
- Customer: Spanish renewable-power developer
- Foreign currency receivable: EUR 9,900,000
- Settlement period: 365 days (12 months)
- Settlement date: 365 days after the valuation date
- Indicative forward exchange rate: 1.1807 USD/EUR
- Put option premium: USD 0.0245 per EUR
- Call option premium: USD 0.0448 per EUR
- Put and call strike prices: Equal to the spot exchange rate



## 2. Inputs: Named-Range Contract

The Excel model will use ten main inputs to calculate and compare the different hedging strategies. These inputs are based on Scenario 31, which involves a EUR 9,900,000 receivable due in 365 days.

Some information, including the foreign currency amount, forward rate, and option premiums, has already been provided in the assigned scenario. Other values, such as the current spot exchange rate and interest rates, will use indicative placeholders until actual market data is collected in Stage 4.

| Named Range | Description | Value | Unit | Stage 4 Data Source |
|---|---|---|---|---|
| `FC_AMT` | Amount the company expects to receive | 9,900,000 | EUR | Assigned Scenario 31 |
| `S0_in` | Current spot exchange rate | 1.10 (placeholder) | USD/EUR | EUR/USD market spot quote |
| `F0_in` | Forward exchange rate | 1.1807 | USD/EUR | Assigned Scenario 31; verify against market quotes |
| `R_USD` | U.S. interest rate | 5.30% (placeholder) | Annual %, ACT/360 | Federal Reserve H.15 |
| `R_FC` | Euro interest rate | 3.50% (placeholder) | Annual %, ACT/360 | European Central Bank |
| `K_PUT` | Put option strike price | 1.10 (placeholder, equal to spot) | USD/EUR | Assigned strike-at-spot rule; verify spot |
| `K_CALL` | Call option strike price | 1.10 (placeholder, equal to spot) | USD/EUR | Assigned strike-at-spot rule; verify spot |
| `PREM_PUT` | Put option premium | 0.0245 | USD per EUR | Assigned Scenario 31; verify market quote |
| `PREM_CALL` | Call option premium | 0.0448 | USD per EUR | Assigned Scenario 31; verify market quote |
| `T_DAYS` | Number of days until settlement | 365 | Days | Assigned Scenario 31 |

**Note:** The spot rate of 1.10 and the interest rates of 5.30% and 3.50% are illustrative placeholders, not verified market quotes. The put and call strikes will always equal the current spot rate. Market-based inputs will be updated with verified sources in Stage 4, while the assigned EUR amount and settlement period will remain unchanged.



## 3. Tab Architecture

The Excel workbook will be organized into different worksheets to make the model easier to understand and use. Each worksheet will have its own purpose, allowing users to enter information, review calculations, and compare the results of the hedging strategies.

| Worksheet | Purpose |
|---|---|
| Cover | Provides a short overview of the FX hedging model and explains its purpose. |
| Legend/Key | Explains the meaning of input cells, calculated outputs, named ranges, and colors used in the workbook. |
| Inputs | Contains the ten required inputs, including exchange rates, interest rates, option premiums, and settlement information. |
| Forward Hedge | Calculates the amount of U.S. dollars the company would receive by using a forward contract. |
| Money Market Hedge | Shows the borrowing, currency conversion, and investment calculations used to hedge the foreign currency receivable. |
| Option Hedge | Calculates the results of using a currency put option, including the cost of the premium. |
| Sensitivity | Compares how each hedging strategy performs under different future exchange rates. |
| Notes & Assumptions | Explains the assumptions, calculation methods, and sources used throughout the model. |

The worksheets will be connected through named ranges so that changes made in the Inputs tab will automatically update the calculations. This will help keep the model consistent and make it easier to check for mistakes.

The workbook will also separate user inputs from calculated results to reduce the risk of accidentally changing formulas.




## 4. Assumptions & Constraints

The model will use several assumptions to keep the calculations consistent and make it easier to compare the three hedging strategies.

- **Exchange Rates:** All exchange rates will be shown as USD per EUR. This means the model will calculate how many U.S. dollars the company receives for each euro.
- **Interest Rates:** The U.S. and euro interest rates will be annualized and calculated using the ACT/360 convention. This means the actual number of days until settlement will be divided by 360 when calculating interest.
- **Market Data:** The foreign currency receivable of EUR 9,900,000, 365-day settlement period, indicative forward rate of 1.1807, and option premiums are based on the assigned Scenario 31. The spot exchange rate and U.S. and euro interest rates will initially use illustrative placeholders until verified market data is collected in Stage 4. Both option strike prices will be set equal to the spot exchange rate.
- **Transaction Costs:** The model will assume there are no additional transaction fees or borrowing costs beyond the rates and option premiums already included.
- **Option Premiums:** The cost of purchasing the put option will be included when calculating the company's net proceeds. The premium will be treated as an upfront expense and carried forward to the settlement date using the USD interest rate.
- **Interest Rate Parity:** The model will compare the quoted forward rate with the rate calculated using U.S. and foreign interest rates. Any differences will be identified and explained rather than automatically considered an error.
- **Settlement:** All hedging strategies will use the same foreign currency amount and settlement period to make the comparisons fair.

These assumptions will help keep the model organized and make sure the results are calculated consistently. However, actual market conditions may be different, which could affect the final results.


## 5. Calculation Flow

The model will calculate the results of three different hedging strategies to determine how much money the company could receive in U.S. dollars. Each strategy will use the same foreign currency amount and settlement period so that the results can be compared fairly.

### Forward Hedge

A forward contract allows the company to lock in an exchange rate before receiving its payment. This protects the company from unfavorable changes in exchange rates because the amount of U.S. dollars received is already determined.

**Formula:**

`USD_FWD = FC_AMT * F0_in`

The amount of foreign currency expected to be received is multiplied by the forward exchange rate to calculate the guaranteed U.S. dollar proceeds.

### Money-Market Hedge

A money-market hedge involves borrowing foreign currency today, converting it into U.S. dollars, and investing the proceeds until the settlement date. When the company receives its foreign currency payment, it uses the money to repay the foreign currency loan.

**Step 1: Calculate the foreign currency borrowing amount**

`Borrow_FC = FC_AMT / (1 + R_FC * T_DAYS / 360)`

**Step 2: Convert the borrowed amount into U.S. dollars**

`USD_NOW = Borrow_FC * S0_in`

**Step 3: Calculate the future value of the U.S. dollar investment**

`USD_MM = USD_NOW * (1 + R_USD * T_DAYS / 360)`

The final result shows the amount of U.S. dollars the company would have at settlement using the money-market strategy.

### Currency Put Option

A currency put option gives the company the right to sell its euros at a predetermined exchange rate. Unlike a forward contract, the company can still benefit if the euro becomes stronger. However, the company must pay an option premium for this flexibility.

**Step 1: Calculate the option payoff at settlement**

`USD_PUT_GROSS = FC_AMT * MAX(S_T, K_PUT)`

Here, `S_T` represents the future exchange rate at settlement. The model uses whichever rate is higher: the future exchange rate or the put option strike price.

**Step 2: Calculate the future value of the option premium**

`USD_PREMIUM_FV = FC_AMT * PREM_PUT * (1 + R_USD * T_DAYS / 360)`

**Step 3: Calculate net proceeds**

`USD_PUT = USD_PUT_GROSS - USD_PREMIUM_FV`

The net proceeds show how much the company receives after accounting for the option premium and its financing cost.

### Comparing the Strategies

The results from each strategy will be compared to understand how much protection each one provides. The forward and money-market hedges provide relatively predictable U.S. dollar proceeds, while the currency put option provides protection with the possibility of benefiting from favorable exchange rate changes.


### Currency Call Option (Additional Reference)

Scenario 31 also provides a currency call option with a premium of USD 0.0448 per EUR and a strike price equal to the current spot exchange rate.

A call option gives its holder the right to buy euros at a predetermined rate. Since the company is expecting to receive euros rather than make a payment in euros, purchasing a put option is more directly related to protecting its receivable.

For reference, the model can calculate the call option's standalone net payoff using the following formulas:

`USD_CALL_PAYOFF = FC_AMT * MAX(S_T - K_CALL, 0)`

`USD_CALL_PREMIUM_FV = FC_AMT * PREM_CALL * (1 + R_USD * T_DAYS / 360)`

`USD_CALL_NET = USD_CALL_PAYOFF - USD_CALL_PREMIUM_FV`

These calculations show the net payoff from purchasing the call option, rather than the company's total receivable proceeds. The primary hedging comparison will remain focused on the forward contract, money-market hedge, and currency put option.



## 6. Sensitivity Plan

The model will include a sensitivity analysis to see how changes in exchange rates could affect the company's U.S. dollar proceeds. This is important because the future exchange rate is uncertain, and different hedging strategies may perform better under different conditions.

The analysis will test 11 possible exchange rates, ranging from 5% below to 5% above the current spot rate (`S0_in`), increasing by 1% each time.

**Formula for each exchange rate scenario:**

`S_T = S0_in * (1 + Percentage Change)`

The sensitivity table will include the following scenarios:

| Scenario | Change in Exchange Rate |
|---|---|
| 1 | -5% |
| 2 | -4% |
| 3 | -3% |
| 4 | -2% |
| 5 | -1% |
| 6 | 0% |
| 7 | +1% |
| 8 | +2% |
| 9 | +3% |
| 10 | +4% |
| 11 | +5% |

For each scenario, the model will calculate the U.S. dollar proceeds from the forward hedge, money-market hedge, and currency put option.

The forward and money-market hedge results should remain constant across all 11 scenarios because these strategies lock in the proceeds. However, the put option results may change depending on whether the future exchange rate is above or below the strike price.

The results will also be displayed in a line chart, with the future exchange rate on the horizontal axis and the U.S. dollar proceeds on the vertical axis. This will make it easier to compare the strategies and see how much protection each one provides against unfavorable exchange rate changes.



## 7. Validation Rules

To make sure the Excel model works correctly, several validation checks will be included. These checks will help identify errors in the formulas, inputs, and calculations before using the results to make financial decisions.

- **Input Validation:** The model will check that all ten required named ranges are included and have the correct values and units. Exchange rates and interest rates must be reasonable, the foreign currency amount must be positive, and the number of days until settlement must be greater than zero.

- **Formula Checks:** All calculations will be reviewed to make sure they reference the correct named ranges and do not contain Excel errors such as `#REF!`, `#VALUE!`, or `#DIV/0!`.

- **Interest Rate Parity:** The model will calculate an implied forward rate using the spot exchange rate and the two interest rates. This will be compared with the quoted forward rate to identify any differences.

  `F_implied = S0_in * (1 + R_USD * T_DAYS / 360) / (1 + R_FC * T_DAYS / 360)`

- **Forward and Money-Market Comparison:** The forward and money-market hedge results will be compared to see whether they are consistent. Large differences will be flagged for further review, since actual market quotes and borrowing rates may not match perfectly.

- **Scenario 31 Forward Check:** The forward hedge calculation should produce USD 11,688,930 using the assigned receivable of EUR 9,900,000 and the forward rate of 1.1807 USD/EUR. This will be used as a reference to check that the Excel model calculates the forward proceeds correctly. The money-market hedge results will be compared after the spot exchange rate and interest rates are verified.

- **Sensitivity Checks:** The model will confirm that all 11 exchange rate scenarios are included, starting at -5% and ending at +5%. It will also check that the forward and money-market results stay constant across scenarios while the put option changes when the future exchange rate rises above the strike price.

- **Option Calculation Checks:** The put option calculations will be reviewed to make sure the company receives the strike-rate protection when the euro weakens and can benefit from a stronger euro when the market rate is higher than the strike price. The option premium and financing cost must also be deducted correctly.

These validation rules will help make the model more reliable and easier to audit. They will also make it easier to identify mistakes before the model is used to compare hedging strategies.



## 8. Outputs

The completed Excel model will provide several outputs to help the company compare the different hedging strategies and understand how exchange rate changes could affect its cash flows.

**Hedging Strategy Summary**

The workbook will include a summary table showing the calculated U.S. dollar proceeds for each strategy.

| Hedging Strategy | Output | Description |
|---|---|---|
| Forward Hedge | `USD_FWD` | Total U.S. dollars received using the forward contract. |
| Money-Market Hedge | `USD_MM` | Total U.S. dollars available at settlement after borrowing foreign currency and investing in U.S. dollars. |
| Currency Put Option | `USD_PUT` | Net U.S. dollar proceeds after accounting for the option premium and its financing cost. |

**Sensitivity Analysis**

The Sensitivity worksheet will display the results for all 11 exchange rate scenarios, ranging from -5% to +5% of the current spot rate. Each scenario will show the future exchange rate and the U.S. dollar proceeds under the three strategies.

**Comparison Chart**

A line chart will visually compare how the hedging strategies perform under different exchange rates. The forward and money-market hedges should appear as horizontal lines because their proceeds are locked in. The put option will show how the company can benefit from favorable exchange rate movements while maintaining protection against unfavorable changes.

**Validation Results**

The workbook will also display validation results to help identify possible errors. These will include checks for missing inputs, formula errors, and differences between the quoted and implied forward exchange rates.

**Final Summary**

The model will provide a clear comparison of the three strategies to help management understand the advantages and disadvantages of each approach. The final recommendation will depend on the company's financial goals, level of risk, and the actual market data collected in Stage 4.



