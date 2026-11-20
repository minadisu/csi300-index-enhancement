# Data provenance and availability

## Primary source

The investment universe is the CSI 300 Index (`000300.XSHG`). The original analysis accessed historical index membership and weights, security prices, valuation ratios, fundamental data, industry classifications, and trading status through **JoinQuant**.

Raw licensed market and financial datasets are **not redistributed** here. The notebook and its HTML export include selected previews and historical outputs. The trading script contains compressed, encoded historical target holdings generated in the research workflow.

## Data pipeline

1. Obtain index constituents as of each rebalance date and filter ineligible securities.
2. Retrieve price, valuation, accounting, market-capitalization, and industry data.
3. Construct a cross-sectional factor panel; impute missing values, apply MAD-based outlier treatment, standardization, neutralization, and orthogonalization.
4. Evaluate rolling Rank IC, ICIR, and positive-IC ratios to select and weight signals.
5. Compute composite stock scores, industry × size-stratified target weights, monthly returns, and performance metrics.

## Original generated outputs

The names below refer to files produced by the original notebook; **they are not CSV files included in this repository**.

| Generated filename | Role |
|:--|:--|
| `index_enhancement_raw.csv` | Initial factor observations |
| `factors4_processed_v3.csv` | Processed factor panel |
| `factors5_score_v3.csv` | Composite scores |
| `rank_ic_v3.csv` | Period-by-period Rank IC |
| `rolling_icir_v3.csv` | Rolling IC information ratios |
| `rolling_ic_positive_ratio_v3.csv` | Positive-IC share |
| `dynamic_factor_weights_v3.csv` | Time-varying factor weights |
| `dynamic_factor_selected_v3.csv` | Factor selection history |
| `result_df_v3.csv` | Target holdings (`date`, `code`, `w`) |
| `monthly_return_v3.csv` | Monthly return series |
| `algorithm_nav_v3.csv` | Strategy and benchmark net asset values |
| `performance_v3.csv` | Aggregate performance |
| `performance_by_period_v3.csv` | Subperiod statistics |

The execution script does not require a separately supplied `result_df_v3.csv` because that historical weight table has been encoded in the source file. The table must be regenerated when changing research parameters or sample dates.

## Access and reproducibility limitations

- The hosted `jqdata`/`jqfactor` interfaces are not interchangeable with a local `jqdatasdk` installation, and the SDK does not provide the entire hosted trading simulator.
- API access, date coverage, and request quotas depend on the user's licensed account.
- Financial-statement publication dates, historical revisions, adjustment conventions, and constituent histories matter for point-in-time validity.
- The original V3 research notebook covers Jan 29, 2010 – Jun 15, 2026; the execution validation uses a different 2015–2026 window.
- Original platform-exported `.csv.url` shortcuts are omitted here; they were links to an account workspace rather than distributable datasets.

For context, see the [main README](../README.md#important-methodological-limitations) and [JoinQuant's SDK repository](https://github.com/JoinQuant/jqdatasdk).
