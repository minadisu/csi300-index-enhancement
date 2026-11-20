# CSI 300 Index Enhancement: Dynamic Factor Selection and Stratified Sampling

*A Python-based empirical study of benchmark-aware multi-factor equity selection in China's A-share market.*

This undergraduate quantitative finance project investigates whether dynamically selected stock characteristics can improve returns relative to the **CSI 300 Index**, while limiting unintended industry and market-capitalization exposures. The workflow combines cross-sectional factor research, rolling predictive-signal evaluation, stratified portfolio construction, turnover-aware rebalancing, and historical performance analysis.

> **Research status:** The metrics below are preserved from the original research notebook, **not independently rerun or verified during repository preparation**. This is an academic backtest, not a live trading record.

## Key results — research notebook (V3)

| Metric | Historical backtest |
|:--|--:|
| Period | Jan 29, 2010 – Jun 15, 2026 |
| Rebalancing | Monthly |
| Strategy annualized return | 6.58% |
| CSI 300 annualized return | 2.62% |
| Reported annualized excess return | **3.95%** |
| Annualized tracking error | **3.82%** |
| Information ratio | **0.99** |
| Maximum portfolio drawdown | −38.95% |
| Maximum relative drawdown | −4.05% |
| Monthly excess-return win rate | 64.29% |
| Average monthly turnover | 22.64% |

**Interpretation:** The reported annualized excess return is the difference between the strategy and benchmark annualized returns before rounding; it is **not** a claim of a separately compounded active-return portfolio. Backtest results depend on the data vintage, signal timing, execution assumptions, and cost model.

The earlier *course-report version* uses a different end date and reports different outcomes (2010–2025; 3.26% annualized excess return and 3.55% tracking error). Results from these versions must not be interchanged.

## Research question and methodology

The project evaluates a practical trade-off: can an index-aware portfolio capture time-varying cross-sectional return signals without taking excessive active risk against the benchmark?

1. **Investment universe.** Retrieve historical CSI 300 constituents at each monthly rebalancing date and apply eligibility/tradability filters.
2. **Factor engineering.** Examine valuation, profitability, earnings growth, technical/return-based signals, volatility, liquidity, and size.
3. **Cross-sectional preprocessing.** Handle missing observations, mitigate outliers using median absolute deviation (MAD), standardize factor values, neutralize selected industry and size effects, and apply symmetric (Löwdin) orthogonalization to reduce factor collinearity.
4. **Dynamic factor selection.** Evaluate relationships between factor ranks and next-period stock returns with rolling Spearman rank information coefficients (Rank ICs). Use rolling IC information ratios (ICIRs), signal-direction consistency, and historical observations to select and weight factors.
5. **Portfolio construction.** Rank eligible securities by their composite factor scores, select high-ranked stocks within industry × market-cap strata, and allocate approximately benchmark-consistent stratum weights. Incorporate position/turnover controls.
6. **Evaluation.** Compare monthly portfolio and benchmark returns using active return, tracking error, information ratio, drawdown, win rate, and turnover. A separate JoinQuant transaction simulation applies stored historical target weights.

This is a **stratified-sampling approach**, not a claim to have implemented a fully specified commercial multi-factor risk optimizer.

## Repository guide

| Resource | Description |
|:--|:--|
| [Research notebook](notebooks/index_enhancement_research.ipynb) | Main research implementation and stored notebook outputs |
| [Notebook HTML](notebooks/index_enhancement_research.html) | Static export for convenient viewing without executing code |
| [Trading backtest](src/joinquant_execution_backtest.py) | JoinQuant execution script; decodes embedded historical target weights rather than rebuilding signals |
| [Research overview](docs/research_overview.md) | Extended English account of methodology, findings, version differences, and limitations |
| [Data notes](data/README.md) | Data provenance, generated-file inventory, and access limitations |
| [Dependencies](requirements.txt) | General Python dependencies; not an environment lockfile |

## Reproducibility and environment

The research notebook was developed in the **JoinQuant research environment**, using platform-provided `jqdata` and `jqfactor` APIs. Market data and fundamentals require the relevant JoinQuant account permissions. Installing the packages in `requirements.txt` does not reproduce the full platform environment or grant a data license.

To explore the project:

1. Open the [HTML notebook](notebooks/index_enhancement_research.html) to inspect the saved analytical workflow and figures.
2. To rerun, load the [Jupyter notebook](notebooks/index_enhancement_research.ipynb) in an appropriately authorized JoinQuant environment; check factor definitions, historical index membership, availability dates, and the rebalancing convention.
3. Regenerate factor scores and target portfolio weights in the research environment.
4. Run the [execution backtest](src/joinquant_execution_backtest.py) in the JoinQuant backtesting environment **only after updating its embedded target weights** to match any revised research run.
5. Verify signal/transaction timing before interpreting simulated returns.

The original dependency versions were not recorded, and an end-to-end reproduction on a fresh environment has not been demonstrated.

## Important methodological limitations

- **Potential look-ahead bias:** A prior execution configuration trades around 10:00 on the signal date even though parts of the research workflow use same-day closing information. Results require revalidation with properly lagged signals.
- **Fundamental-data timing:** Not every financial field was independently lagged to its actual public disclosure date. Point-in-time fidelity needs additional auditing.
- **Portfolio constraints:** Certain fallback normalization paths may relax the intended individual-name cap when strict feasibility is not attained.
- **Trading realism:** Simplified research-side transaction-cost and turnover assumptions differ from the execution simulator's fills and costs.
- **Out-of-sample testing:** Dividing historical results by calendar period is not equivalent to a fully independent out-of-sample evaluation; model selection and robustness still require testing.
- **External data:** The repository does not redistribute underlying licensed price/fundamental datasets. Embedded historical weights are not a substitute for the original factor database.

## Research context

The methods are informed by public literature on factor investing, active portfolio management, symmetric orthogonalization, and index-enhancement approaches, including 2018 research publications from Tianfeng Securities and Huatai Securities. These third-party reports are referenced for research context, not reproduced in this repository.

**Purpose:** Academic research and portfolio construction demonstration. Historical simulated performance does not guarantee future results and should not be interpreted as investment advice.
