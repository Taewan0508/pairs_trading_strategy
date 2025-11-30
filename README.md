# 📈 KO–PEP Pairs Trading Strategy (Mean Reversion) Regression Comparison
This project implements a classic statistical arbitrage pairs trading strategy using Coca-Cola (KO) and Pepsi (PEP).
I came across an interesting issue I faced while wokring on this project. I wanted to see whether if the results for pairs trading would differ if the independent and dependent variables altered. Ultimately, figuring out if beta (the hedge ratio) would differentiate by the change of variables. 
The strategy uses:

- **Linear regression** to estimate the** hedge ratio (β)**
- **Spread calculation** using the hedged prices
- **Z-score normalization** to detect deviations
- **Long/short trading signals** based on extreme spread movements
- **Backtest performance** using cumulative strategy returns
  
## 🚀 Key Features

- Downloads KO & PEP historical price data using yfinance
- Computes the hedge ratio via OLS regression
- Creates a mean-reverting spread
- Converts spread into a normalized z-score
- Generates trading signals when the spread diverges
- Backtests the strategy with no look-ahead bias
- Visualizes:
  - Spread z-score and trading thresholds
  - Cumulative strategy performance
- Fully reproducible on Google Colab or Jupyter Notebook

## 🧠 Concept Overview
Pairs trading assumes that two historically related stocks (KO & PEP) maintain a stable long-term relationship.
### When PEP is regressed on KO
1. **Estimate Hedge Ratio**
  - Regress PEP on KO:
  - PEP = α+β * KO +ϵ

2. **Compute Spread**
  - _spread_= PEP - β *KO
  - mean reverting

3. **Z-score Standardization**
  - z​=(spread​−μ​)/σ

4. **Trading Rules**
  - Long KO, Short PEP when zscore > +2
  - Short KO, Long PEP when zscore < -2
  - Close positions when z-score goes back towards 0

5. **Strategy Returns**
  - rstrategy​=(rKO​−β * rPEP​) * signalt−1​

### When KO is regress on PEP
- vice versa


## 🧪 Technologies Used

- Python
- pandas
- numpy
- statsmodels
- matplotlib
- yfinance

## Results 
- The z-scores did not match
- PEP's regrression on KO had a significant much higher z-score as well as strategy equity curve (as shown in chart under /results)
    - The equity value varied from 1.14 to 0.5
- Then how do I determine which method is correct?
    - Neither diretion is objectively correct but the method with more stable independent variable would be ideal
    - Having KO as a independent variable since KO is more of a stable stock compared to PEP (more volatile)
 
### Explanation
- The betas are not reciprocals of each other
- The betas differ because:
  -  Regression minimizes squared errors **in the Y direction only**
  -  Errors in X are ignored
  -  Thus switching X and Y changes the entire minizing geometry
- **_Regression is not symmetric_**
