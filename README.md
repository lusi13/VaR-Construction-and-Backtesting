# VaR-Construction-and-Backtesting
This project aims to compare different models for estimating Value-at-Risk (VaR) and to evaluate their performance using rigorous backtesting procedures. The analysis leverages historical financial data, multiple modeling approaches, and statistical tests to assess the accuracy and robustness of the VaR estimates.

Source: Daily adjusted closing prices from various stocks and market indices.
Selected Tickers:
AAPL, AMZN, DIS, MSFT, JPM, F, PG, S&P500, IXIC.  
In-sample Time Period: January 2009 - December 2021.
Out-of-sample Time Period: Last 300 days for backtesting.

Selected Models:
- Historical Simulation
Estimates VaR using empirical distribution without assuming any specific return distribution.
Cornish-Fisher adjustment for skewness and kurtosis.
- Extreme Value Theory (EVT)
Generalized Extreme Value (GEV); Applied to block maxima of negative returns.
Generalized Pareto Distribution (GPD); Models excesses over the 95th percentile threshold.
- GARCH Models
GARCH(1,1) and GARCH(2,2):
Conditional volatility models with t-distribution for fat tails.
Captures volatility clustering and persistence in financial returns.
- Filtered Historical Simulation (FHS)
Combines GARCH volatility modeling with historical simulation.
Captures time-varying volatility and heteroskedasticity.
- EVT + GARCH
Combines GARCH for volatility estimation with EVT for extreme tail behavior.
- Dynamic Quantile Regression
Directly models tail quantiles at desired confidence levels (95%, 99%).
Captures asymmetric risk profiles by estimating conditional quantiles.

For the backtesting procedure, I used the Rolling Window Approach, and a Confidence Level set to 99%;
Rolling window of size 1000 to capture sudden volatility shifts.
Ensures responsiveness to recent market changes by avoiding overweighting of historical data.
Backtesting Steps:
- Define VaR model (e.g., Historical Simulation, EVT, GARCH).
- Set confidence level.
- Compute VaR estimates using rolling window predictions.
- Compare with realized returns to check for VaR breaches.
- Apply backtesting tests to statistically validate the model's performance.


Statistical Tests:
- Kupiec Test (Proportion of Failures)
Tests if the proportion of VaR breaches matches the expected violation rate.
Measures unconditional coverage of VaR model.
-Christoffersen Test (Conditional Coverage)
Evaluates the independence of VaR violations to ensure no clustering of breaches.
- Berkowitz Test
Checks if the predictive distribution of returns is correctly specified.
- Engle-Manganelli Test
Uses quantile regression to assess if the model accurately captures tail risk dynamics.
- TUFF Test (Time Until First Failure):
Measures the time interval between VaR breaches, identifies overly conservative or aggressive models.

Results Overview:
- Historical Simulation
Kupiec and Christoffersen tests generally accept the model.
Exceptions for AMZN and DIS, indicating underestimation of tail risk.
- EVT Models
More conservative VaR estimates compared to Historical Simulation.
GEV performed better for extreme tail risks, while GPD effectively captured excesses.
- GARCH Models
Captured volatility clustering and persistence effectively.
t-distribution helped in modeling fat tails.
GARCH(2,2) followed return volatility more closely than GARCH(1,1).
- Filtered Historical Simulation (FHS):
Better response to time-varying volatility.
Outperformed standard Historical Simulation during periods of market turmoil.
- Quantile Regression:
Captured asymmetric risk profiles, provided robust VaR estimates without assuming normality.

Final Considerations: 
No single model consistently outperformed others across all assets.
GARCH-based models showed robust performance across multiple tests, particularly for volatility clustering.
EVT models effectively captured extreme losses, with GEV being more conservative.
Quantile regression demonstrated flexibility in modeling asymmetric risk profiles.
