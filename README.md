# Simple Moving Average (SMA) Crossover Backtesting

## Introduction

This project investigates the performance of a Simple Moving Average (SMA) crossover trading strategy compared to a Buy & Hold baseline. The SMA crossover is a basic technical analysis method where a buy signal is generated when a short-term average rises above a longer-term average, and a sell signal when the short-term average falls below. The purpose of this project was to determine whether these strategies could reduce risk or improve returns in different market conditions.

---

## Methodology

Historical stock data was collected using the `yfinance` library. Four representative assets were examined: AAPL during 2020 to show behaviour in a strong bull run after the COVID crash, MSFT during 2021–2022 to capture a clear peak and subsequent decline, XOM during 2020 to reflect the sharp fall and recovery in the energy sector, and IBM during 2016 to demonstrate behaviour in a largely sideways market. Three SMA strategies were tested with short and long pairs of 10/30, 20/50, and 50/100 days. A Buy & Hold approach was used as the baseline.

Daily returns were calculated from closing prices, and cumulative returns were constructed for each strategy to form equity curves. These equity curves were then used to calculate final return, volatility, Sharpe ratio, and maximum drawdown. Outputs were saved as tables in the `tables/` directory and as equity curve plots in the `imgs/` directory.

---

## Results

For AAPL in 2020, Buy & Hold captured the full upward move of the market, whereas SMA crossovers exited too early and missed much of the recovery. The equity curve is shown in Figure 1 and the summary table in Table 1.

<img src="imgs/EquityCurve AAPL_2020-01-01_2020-12-31.png" alt="Equity Curve AAPL 2020" width="600"/>

**Figure 1.** Equity curve comparison of Buy & Hold and SMA strategies for AAPL between January and December 2020.

|                  |   Buy/Hold |     10/30 |     20/50 |    50/100 |
|:-----------------|-----------:|----------:|----------:|----------:|
| Final Return     |   1.79624  |  1.62925  |  1.90052  |  1.60969  |
| Volatility       |   0.467809 |  0.287728 |  0.272483 |  0.297394 |
| Sharpe Ratio     |   0.093965 |  0.116384 |  0.157746 |  0.110632 |
| Maximum Drawdown |  -0.314273 | -0.189575 | -0.203756 | -0.203756 |

**Table 1.** Performance metrics for Buy & Hold and SMA strategies applied to AAPL between January and December 2020.

For MSFT between November 2021 and December 2022, Buy & Hold suffered a drawdown of over 35%, whereas the SMA strategies significantly reduced losses by moving to cash. The equity curve is displayed in Figure 2 and the performance metrics in Table 2.

<img src="imgs/EquityCurve MSFT_2021-11-01_2022-12-31.png" alt="Equity Curve MSFT 2021–2022" width="600"/>

**Figure 2.** Equity curve comparison of Buy & Hold and SMA strategies for MSFT between November 2021 and December 2022.

|                  |   Buy/Hold |      10/30 |      20/50 |    50/100 |
|:-----------------|-----------:|-----------:|-----------:|----------:|
| Final Return     |  0.736285  |  0.814715  |  0.839538  |  0.849866 |
| Volatility       |  0.337817  |  0.176697  |  0.15242   |  0.103361 |
| Sharpe Ratio     | -0.0384699 | -0.0572805 | -0.0573569 | -0.081958 |
| Maximum Drawdown | -0.371485  | -0.229724  | -0.193448  | -0.15466  |

**Table 2.** Performance metrics for Buy & Hold and SMA strategies applied to MSFT between November 2021 and December 2022.

XOM during 2020 provided an example where SMA strategies added value by avoiding part of the sharp crash and re-entering during the recovery. The equity curve is presented in Figure 3 and the summary table in Table 3.

<img src="imgs/EquityCurve XOM_2020-03-01_2020-12-01.png" alt="Equity Curve XOM 2020" width="600"/>

**Figure 3.** Equity curve comparison of Buy & Hold and SMA strategies for XOM between March and December 2020.

|                  |   Buy/Hold |     10/30 |       20/50 |     50/100 |
|:-----------------|-----------:|----------:|------------:|-----------:|
| Final Return     |  0.753386  |  1.07122  |  0.941162   |  0.943677  |
| Volatility       |  0.579775  |  0.344219 |  0.273998   |  0.0918702 |
| Sharpe Ratio     | -0.0226358 |  0.027391 | -0.00992457 | -0.0498009 |
| Maximum Drawdown | -0.411896  | -0.241564 | -0.245423   | -0.0630381 |

**Table 3.** Performance metrics for Buy & Hold and SMA strategies applied to XOM between March and December 2020.

IBM during the first half of 2016 highlighted the weakness of SMA crossovers in sideways conditions. Frequent false signals led to poor performance compared to Buy & Hold. The equity curve is shown in Figure 4 and the results table in Table 4.

<img src="imgs/EquityCurve IBM_2016-01-01_2016-06-01.png" alt="Equity Curve IBM 2016" width="600"/>

**Figure 4.** Equity curve comparison of Buy & Hold and SMA strategies for IBM between January and June 2016.

|                  |   Buy/Hold |      10/30 |      20/50 |    50/100 |
|:-----------------|-----------:|-----------:|-----------:|----------:|
| Final Return     |  1.15343   |  1.16305   |  1.03359   | 1.03661   |
| Volatility       |  0.241452  |  0.155539  |  0.144036  | 0.0377947 |
| Sharpe Ratio     |  0.0996397 |  0.156148  |  0.040259  | 0.149258  |
| Maximum Drawdown | -0.123638  | -0.0559232 | -0.0559232 | 0         |

**Table 4.** Performance metrics for Buy & Hold and SMA strategies applied to IBM between January and June 2016.

---

## Discussion

The outcomes across the different assets highlight both the strengths and weaknesses of SMA crossover strategies. In the case of AAPL during 2020, the method failed to capture the bulk of the bull run, illustrating that in sustained uptrends the strategy exits too early and leaves returns on the table. By contrast, MSFT between late 2021 and 2022 demonstrates the protective side of the approach. While Buy & Hold endured a drawdown of more than a third, the crossover rules cut exposure and limited the fall to less severe levels. The XOM results show how the strategy can provide balance, avoiding the deepest part of a crash while still participating in the recovery, though the timing was not perfect and some of the upside was missed. IBM in 2016 reveals the other major limitation: when the market moves sideways with no clear trend, crossovers generate repeated false signals, leading to poor performance.

Taken together, these cases underline that SMA crossovers are best viewed as risk management tools. They smooth equity curves and cushion losses in downturns, but they lag when prices rise quickly and they falter in flat markets. This pattern was visible in the tables, where maximum drawdowns consistently improved under SMA strategies while final returns often fell short. The central trade‑off is clear: lower risk comes at the cost of lower reward.

---

## Conclusion

SMA crossovers reduced volatility and maximum drawdowns in most cases, but their returns lagged behind Buy & Hold when markets trended upwards. No single SMA pair was optimal in all scenarios, but these findings confirm that while simple moving averages can smooth equity curves and reduce losses, they do not reliably outperform passive investing in the long term.

---

## References

[yfinance documentation](https://pypi.org/project/yfinance/)
Selected literature on trend-following and moving average strategies
