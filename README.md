# Raunak Sood

M.S. Computer Science at USC · machine learning at Innovius Capital · B.S. Economics,
Santa Clara. Quantitative research, applied ML, and product engineering.

[raunaksood.vercel.app](https://raunaksood.vercel.app) · [LinkedIn](https://www.linkedin.com/in/raunak-sood)

---

## Featured work

### [Point-in-Time US Equity Factor Research](https://github.com/quantraunak/ls-multifactor-research)

A cross-sectional equity signal on reconstructed point-in-time index membership and SEC
EDGAR XBRL fundamentals joined on **filing date**, evaluated with a purged and embargoed
walk-forward before any portfolio is constructed.

**IC 0.0165 (t = 2.00) · decile spread 68bp/month (t = 3.08) · 727 names, 2004–2026**

The result the project is actually about: regressing the decile spread on the market shows
**59% of the apparent edge is beta rather than stock selection**, and seed dispersion across
six identical re-fits holds IC at 0.0164 ± 0.0008 while Sharpe ranges 0.09–0.49 — a
distinction that decides whether a factor study is a strategy.

`Python · LightGBM · CVXPY · pandas`
[Results dashboard](https://quantraunak.github.io/ls-multifactor-research/) · [Write-up](https://raunaksood.vercel.app/work/quant)

### [Resampled Thought Trees](https://github.com/quantraunak/tot-resampled-thought-trees)

Co-authored research (five-author team, USC) on measuring which intermediate states in
Tree-of-Thought LLM search actually preserve downstream success. Node-level resampling and
branch ablation across Game24 and constrained crossword search — **22,350 resampling trials
across 280 logged search trees**, with nodes classified into five categories by measured
downstream utility rather than by final answer alone.

[Paper](https://github.com/quantraunak/tot-resampled-thought-trees/blob/main/docs/paper.pdf) · [Write-up](https://raunaksood.vercel.app/work/reasoning)

### [Melange](https://github.com/quantraunak/Melange)

A collaboration-matching app for photographers, models, stylists, and filmmakers — post a
project, swipe, match, and message to plan the shoot. Two shipped clients (Next.js web and
Expo/React Native iOS) against one Postgres, with authorisation enforced by row-level
security on every table rather than by a trusted backend.

`Next.js · React Native · Supabase · Postgres`
[Live demo](https://melange-psi.vercel.app) · [Write-up](https://raunaksood.vercel.app/work/melange)

---

## Also here

| | |
|---|---|
| [Bitcoin-Prediction](https://github.com/quantraunak/Bitcoin-Prediction) | LSTM vs Auto-ARIMA on 3.7M rows of Binance BTC limit-order-book data |
| [GS-Volatility](https://github.com/quantraunak/GS-Volatility) | Exponential smoothing vs GARCH vs LSTM for volatility forecasting |
| [Minimum-Wage](https://github.com/quantraunak/Minimum-Wage) | Two-way fixed-effects and IV panel study of minimum wage pass-through |
| [Earnings-Calls](https://github.com/quantraunak/Earnings-Calls) | Text analysis of earnings call transcripts joined to daily returns |
| [Labor-Shock](https://github.com/quantraunak/Labor-Shock) | Dynamic macroeconomic modelling of the US business cycle |

## Stack

`Python` `PyTorch` `LightGBM` `CVXPY` `scikit-learn` `pandas` `LangChain` `CatBoost`
`R` `SQL` `C++` `TypeScript` `Next.js` `Supabase` `Postgres` `Docker` `AWS`
