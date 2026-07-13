# Cointegration-Based Pairs Trading

Mean-reversion strategy on cointegrated equity pairs, evaluated with a strict
train/test split so that pair selection never sees the evaluation data.

## Method
- Engle-Granger scan of 136 equity pairs on a 2-year train window (2021-2023),
  with a Bonferroni check: ~7 false positives expected by chance at p < 0.05,
  and no pair survived the corrected cutoff. SPY/META was selected from the
  naive-cutoff list on compositional grounds (META is a top-10 SPY holding),
  disclosed in the notebook as a post-hoc judgment call.
- Rolling OLS hedge ratio; estimation window set to 3x the AR(1) half-life of
  the train-period spread, fit on train data only.
- Z-score signals (entry 2, exit 0.5, stop 4), next-bar execution, simple
  slippage model.
- All reported numbers come from a held-out 2-year test window (2023-2025)
  that played no role in pair selection or parameter choices.

## Out-of-sample results
Sharpe: 0.83,   
Max Drawdown: -7.3%,   
Trades: 12

The same strategy evaluated in-sample scores 1.4, i.e. selection bias alone
inflates the Sharpe by ~70%.

## Known limitations
Thin cost model (1bp slippage, no borrow or financing costs), a single pair,
and a small trade count. The notebook discusses each.

## Run
pip install yfinance pandas statsmodels matplotlib
Open Pairs_Trading_train_test_split.ipynb and run top to bottom.
