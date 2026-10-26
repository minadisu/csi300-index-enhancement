# 数据来源与获取说明

## 来源与覆盖

研究对象为沪深300指数（000300.XSHG），主要数据来自聚宽（JoinQuant）研究环境，包括历史指数成分股及权重、股票行情、估值、财务指标、行业分类与交易状态。

仓库不附完整原始行情、财务数据库及完整因子面板。笔记本和 HTML 中保留部分历史数据预览，交易脚本内嵌历史目标持仓。完整研究数据的获取与使用须遵守对应账号权限和数据服务条款。

## 数据处理流程

1. 按月获取当期成分股，过滤 ST、新上市及交易不活跃股票。
2. 获取行情、估值、财务、市值和行业数据，构建原始因子面板。
3. 完成缺失值处理、去极值、中性化、标准化及对称正交。
4. 计算滚动 Rank IC、ICIR 和 IC 正向占比，生成因子权重与综合得分。
5. 按行业—市值分层抽样构建目标组合，计算月度收益及绩效。

## 研究流程生成的文件

以下名称是笔记本运行时生成的文件，不表示仓库已包含这些 CSV。

| 文件 | 用途 |
|---|---|
| index_enhancement_raw.csv | 原始因子面板 |
| factors4_processed_v3.csv | 预处理后的因子 |
| factors5_score_v3.csv | 因子综合评分 |
| rank_ic_v3.csv | 各期 Rank IC |
| rolling_icir_v3.csv | 滚动 ICIR |
| rolling_ic_positive_ratio_v3.csv | 滚动 IC 正向占比 |
| dynamic_factor_weights_v3.csv | 动态因子权重 |
| dynamic_factor_selected_v3.csv | 动态因子筛选记录 |
| result_df_v3.csv | 目标持仓，交易执行使用 date、code、w 三列 |
| monthly_return_v3.csv | 月度收益 |
| algorithm_nav_v3.csv | 策略、基准及相对净值 |
| performance_v3.csv | 整体绩效 |
| performance_by_period_v3.csv | 分阶段绩效 |

当前交易脚本已将历史目标持仓压缩编码后内嵌，运行时无需外部 CSV。更新研究参数或区间时，应同步更新交易输入。

## 环境与复现限制

- 平台内的 `jqdata`、`jqfactor` 与本地 `jqdatasdk` 的使用环境不同，本地 SDK 不包含完整平台回测引擎。
- 历史覆盖范围与调用额度取决于账号权限和平台条件。
- 财务数据公告时点、历史修订、行业口径和价格复权方式均可能影响结果。
- 原报告记录的研究端区间为 2010-01-29 至 2026-06-15，交易验证区间为 2015-01-05 至 2026-06-15。
- 原研究未对全部财务指标额外进行公告日滞后调整；交易时点问题及其他限制见[项目首页](../README.md#研究局限)。

官方参考：[JQData SDK](https://github.com/JoinQuant/jqdatasdk)。
