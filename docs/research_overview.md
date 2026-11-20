# Research overview

## Title

**CSI 300 Index Enhancement Based on Dynamic Factor Selection and Industry–Size Stratified Sampling**

## Motivation

A conventional capitalization-weighted index portfolio closely tracks the market but cannot deliberately favor stocks exhibiting attractive characteristics. An unconstrained multi-factor portfolio may capture such signals at the cost of substantial departures from its benchmark. This project studies a transparent intermediate solution: combine a dynamic stock-ranking model with benchmark-aware industry and market-capitalization sampling.

## Model design

The eligible universe consists of historical CSI 300 constituents, filtered for relevant trading restrictions. Candidate factors span valuation, profitability, growth, past returns, volatility, liquidity, and size. The empirical workflow treats missing values and outliers, standardizes cross-sectional inputs, neutralizes selected market-cap and industry effects, and applies symmetric orthogonalization.

For each factor, the cross-sectional Spearman correlation between factor values and **subsequent** stock returns defines the Rank IC. Past rolling IC statistics and ICIRs are used to evaluate the direction and stability of predictive relationships. Factors are screened and assigned time-varying weights, producing a composite stock score.

Portfolio holdings are chosen from high-scoring stocks within industry and market-capitalization strata. Stratum-level benchmark weights guide allocation to contain large systematic deviations, while retention and turnover rules aim to reduce trading. The implementation focuses on an interpretable sampling procedure rather than full covariance-based risk optimization.

## Reported empirical findings

The saved **V3 research notebook** reports a Jan 2010–Jun 2026 monthly backtest with 6.58% annualized strategy return versus 2.62% for CSI 300, reported annualized excess return of 3.95%, tracking error of 3.82%, information ratio of 0.99, monthly win rate of 64.29%, and average monthly turnover of 22.64%. These are historical notebook outputs and were **not rerun for this repository update**.

A separately written **undergraduate course report** ends in Oct 2025 and gives 5.46% annualized strategy return, 2.21% benchmark return, 3.26% annualized excess return, 3.55% tracking error, and 0.90 information ratio. The source version, end date, and metrics differ; the figures should not be combined or presented as identical experiments.

## Interpretation and limitations

Reported positive active return is consistent with the model extracting useful historical signals in the sampled period. It does not establish a deployable investment edge. Prior to any stronger claim, the model must be rerun with end-to-end point-in-time controls, including actual financial disclosure availability, lagged end-of-day signals, executable rebalance dates, and consistent transaction costs. Also needed are strict constraint-feasibility checks, independent out-of-sample tests, and sensitivity analysis across factor selection windows and portfolio rules.

A key implementation distinction is that the separate JoinQuant execution script **replays embedded target weights**. It does not build factors or recompute portfolio holdings, and it must not be represented as an end-to-end independent implementation.

## References and provenance

- Tianfeng Securities (2018), *Index Enhancement Strategy Based on Adaptive Risk Control* (Chinese-language research report).
- Huatai Securities (2018), *Overview and Applications of Index Enhancement Methods* (Chinese-language research report).
- Fama and French (1993, 2015), multi-factor asset-pricing models.
- Jegadeesh and Titman (1993), return momentum.

This project originated as an undergraduate **course research project**, not a published paper or a graduate thesis. The repository's English documentation summarizes the work; some original notebook and source-code annotations remain in Chinese.

**Disclaimer:** For academic demonstration only; not financial advice.
