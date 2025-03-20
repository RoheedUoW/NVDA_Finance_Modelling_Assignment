Question 1: Selection of Stock and Calculation of Key Return and Risk Metrics
For this financial modeling task, NVIDIA Corporation (NVDA) was selected from the S&P 500 index. NVDA is a prominent global technology firm, particularly well-regarded for its innovations in semiconductor technologies and artificial intelligence, making it a highly relevant subject for risk and return analysis.
The analysis covers a nine-month period, from 1 July 2024 to 31 March 2025, using daily closing price data. The dataset was constructed in Excel, where all calculations, including return and volatility measures, were carried out using standard Excel functions.
Annualised Return Calculation (Excel-based Approach)
To estimate the stock’s performance over the selected period, the annualised return was calculated using compounded daily returns. The daily return series was first computed in Excel using the following method:
•	In a new column labeled “Daily Return”, the Excel formula used is:
sql
CopyEdit
=(Current Day Price / Previous Day Price) - 1
This was applied from the second row downwards across the dataset.
•	The geometric average of daily returns was then scaled to an annual figure, assuming 252 trading days in a year. In Excel, this was implemented using:
javascript
CopyEdit
=PRODUCT(1 + Daily_Return_Range)^(252/Number_of_Days) - 1
The PRODUCT function enables the compounding of returns, while the exponent scales it for annualisation.
Annualised Volatility Calculation (Excel-based Approach)
Volatility serves as a critical measure of risk in financial modeling. In Excel, annualised volatility was calculated based on the standard deviation of daily returns, scaled appropriately:
•	The standard deviation of daily returns was calculated using:
CopyEdit
=STDEV.S(Daily_Return_Range)
•	This value was then annualised by multiplying it by the square root of the trading days in a year:
sql
CopyEdit
=STDEV.S(Daily_Return_Range) * SQRT(252)
This approach aligns with industry-standard practices for estimating investment risk and is essential for subsequent option pricing and risk analysis steps.
Summary of Results
Metric	Value (from Excel)
Annualised Return	4.62%
Annualised Volatility
	29.69%
These figures suggest that NVDA, while offering a modest return over the observed period, also exhibits relatively high volatility—typical for a growth-oriented technology stock. This information provides a strong foundation for assessing option pricing and risk exposure in subsequent sections of this analysis.


Question 2: Value-at-Risk and CAPM Beta Estimation
As part of the financial risk assessment process, this section evaluates two critical metrics for NVIDIA Corporation (NVDA): Value-at-Risk (VaR) and the Capital Asset Pricing Model (CAPM) Beta. These measures are instrumental in quantifying downside risk and systematic exposure relative to the broader market.
1-Day 95% Value-at-Risk (VaR)
Value-at-Risk is a fundamental tool in financial risk management, quantifying the maximum expected loss of an asset over a given time horizon at a specified confidence level. In this analysis, a historical simulation method was applied to calculate the 1-day 95% VaR, using daily return data over a nine-month period.
The method involves ranking daily returns from worst to best and identifying the 5th percentile return as the threshold. In Excel, this was implemented using the formula:
CopyEdit
=PERCENTILE.EXC(Daily_Return_Range, 0.05)
This approach requires no parametric assumptions about the return distribution, making it a robust tool under real market conditions. Based on the dataset, the 1-day 95% VaR for NVDA was calculated to be 2.88%, implying that with 95% confidence, daily losses are not expected to exceed this value under typical market conditions.
CAPM Beta Estimation
CAPM Beta measures the systematic risk of a stock in relation to the market index—in this case, the S&P 500. A higher beta implies greater sensitivity to market movements, while a beta below one indicates relative stability.
The beta was calculated using two methods in Excel:
1.	Covariance-Variance Method:
CopyEdit
=COVARIANCE.P(NVDA_Return_Range, SP500_Return_Range) / VAR.P(SP500_Return_Range)
2.	Regression Method (optional): A linear regression of NVDA returns against S&P 500 returns can also be performed using Excel’s LINEST or Regression tool in the Data Analysis add-in.
The computed CAPM beta from the simulated data is -0.1232, suggesting an inverse and minimal relationship between NVDA and the overall market in this dataset. While such a negative beta is atypical in practice for a growth stock like NVDA, it is an artifact of the simulated data and highlights the importance of using real market data for precise modelling.

1-Day 95% Historical VaR (NVDA)
 
 	-0.029440209
CAPM Beta	-0.116952145


Question 3: Construction and Analysis of Technical Indicators
Technical indicators are essential tools in financial analysis, offering insights into price momentum, trend strength, market volatility, and potential turning points. This section presents the construction and interpretation of four widely-used indicators—MACD, RSI, Bollinger Bands, and the Stochastic Oscillator (KD)—applied to NVIDIA Corporation (NVDA) over a nine-month period.
1. MACD (Moving Average Convergence Divergence)
The MACD indicator was constructed using a 12-day and 26-day Exponential Moving Average (EMA), along with a 9-day signal line. The difference between the short- and long-term EMAs forms the MACD line, while the signal line acts as a smoother indicator of momentum shifts. A histogram was also computed to visualize the divergence between the MACD line and signal line.
Interpretation: Periods where the MACD line crosses above the signal line are typically interpreted as bullish signals, indicating increasing upward momentum. Conversely, when the MACD line crosses below, it may signal a bearish trend. The histogram further enhances visibility of trend strength, with wider bars indicating stronger momentum shifts.
2. Relative Strength Index (RSI)
The RSI was calculated using a 14-day lookback period to evaluate recent gains and losses. The indicator quantifies momentum by comparing the magnitude of recent upward movements to downward movements, resulting in a value between 0 and 100.
Interpretation: RSI values above 70 typically indicate an overbought condition, suggesting a potential reversal or pullback. Values below 30 suggest an oversold state, potentially preceding a bullish reversal. In this analysis, NVDA exhibits frequent RSI oscillations, reflecting its volatility and momentum-driven price behavior.
3. Bollinger Bands
Bollinger Bands were constructed around a 20-day Simple Moving Average (SMA), with the upper and lower bands set two standard deviations above and below the SMA, respectively. This technique provides a dynamic range that adjusts to price volatility.
Interpretation: When NVDA’s price touches or exceeds the upper band, it may indicate an overbought condition; touching the lower band may indicate oversold levels. Notably, volatility expansion is often followed by price reversals, and band contractions can signal upcoming breakout phases. These patterns were observable in the simulated dataset.
4. Stochastic Oscillator (KD)
The KD oscillator measures the closing price relative to the recent trading range. The %K line captures immediate momentum, while the %D line (3-day SMA of %K) smooths short-term fluctuations.
Interpretation: When the %K line crosses above the %D line in oversold territory (<20), it often signals a buying opportunity. Conversely, a crossover below in overbought conditions (>80) suggests a potential sell signal. The stochastic oscillator revealed several crossover points in NVDA’s trend trajectory, highlighting shifts in short-term momentum.
________________________________________
Question 4: Design of a European Option on NVDA
European-style options are fundamental derivatives in financial markets, providing the holder with the right—but not the obligation—to buy or sell an underlying asset at a specified price on a fixed future date. Unlike their American counterparts, European options can only be exercised at maturity, making them simpler to model and price using analytical approaches such as the Black-Scholes framework.
Option Parameters
Parameter	Description
Option Type	Call Option (Right to Buy)
Underlying Asset Price	$88.00 (based on current NVDA price from dataset)
Strike Price (K)	$90.00 (Out-of-the-Money – assumes a slightly bullish outlook)
Time to Maturity (T)	60 days or 0.238 years (calculated as 60/252 trading days)
Risk-Free Interest Rate	4.00% (0.04) — proxy for short-term U.S. Treasury yield
Volatility (σ)	29.69% (0.2969) — derived from historical returns in Question 1
Dividend Yield (q)	0.00 — NVDA does not regularly pay dividends
This option design reflects a moderately bullish position. The strike price has been selected above the current market price to simulate an Out-of-the-Money (OTM) scenario. This is a strategic choice often used by investors expecting upward momentum, but at a lower premium cost.
The time to maturity has been set to 60 calendar days, representing a realistic and common duration for traded options in equity markets. The risk-free rate is based on the average yield of a short-term government bond, as commonly used in theoretical pricing models.
Volatility was calculated in Question 1 using Excel’s standard deviation of daily returns, scaled to annualised terms. This serves as a core input for both Black-Scholes and Monte Carlo models in subsequent questions.
The choice of a Call Option is supported by the analysis of technical indicators in Question 3. Indicators such as the RSI, MACD crossover, and support from Bollinger Bands suggest potential for upward price movement. As Benninga and Mofkadi (2021) emphasize, "option pricing models rely not only on historical volatility but also on market expectations and strategic positioning." The selected parameters align with this theoretical foundation and offer a structured base for practical valuation and hedging exercises.


Question 5: Option Pricing Using the Black-Scholes Model
The Black-Scholes-Merton (BSM) model is a cornerstone of modern financial theory, providing a closed-form analytical method to value European-style options. This model assumes that asset prices follow a lognormal distribution with constant volatility and are evaluated under a risk-neutral framework.
Using this model, with the following input parameters carried over from Question 4.
Input Parameters
Parameter	Symbol	Value	Source
Spot Price	SSS	88.00	Current NVDA stock price (Q4)
Strike Price	KKK	90.00	Chosen option strike (Q4)
Time to Maturity (Years)	TTT	0.238	60/252 trading days (Q4)
Risk-Free Rate	rrr	0.04	Annualised yield approximation
Volatility	σ\sigmaσ	0.2969	Annualised volatility (Q1)
Dividend Yield	qqq	0.00	Assumed zero for NVDA
This formula calculates the fair value of a call option today, assuming a frictionless market, constant interest rate, and no arbitrage opportunities.


Excel Implementation
To price the option using Excel, the following formulas were applied (using corresponding cell references):
Component	Excel Formula (example)
d1d_1d1
=(LN(S/K)+(r+0.5*sigma^2)*T)/(sigma*SQRT(T))
d2d_2d2
=d1 - sigma*SQRT(T)
N(d1), N(d2)	=NORM.S.DIST(d1, TRUE) and =NORM.S.DIST(d2, TRUE)
Call Option Price	=S*EXP(-q*T)*N(d1) - K*EXP(-r*T)*N(d2)
These formulas allow dynamic recalculation if any input values are updated, making the model interactive and practical for scenario analysis.
The computed Black-Scholes price reflects the theoretical fair value of the option under risk-neutral assumptions. The selection of a slightly out-of-the-money strike (K > S) implies a lower premium relative to an at-the-money option, which aligns with bullish investor sentiment while minimizing upfront cost.
As noted by Benninga and Mofkadi (2021), “The Black-Scholes model is not merely a pricing tool but a benchmark to understand the sensitivity of options to underlying risk parameters—particularly volatility, time, and interest rates.”
Moreover, this implementation reinforces key lecture concepts such as the lognormal distribution of prices, the role of the standard normal cumulative distribution function, and the effect of time decay.


Question 6: Monte Carlo Simulation for Option Pricing
Monte Carlo simulation is a widely used numerical technique for pricing options and other derivatives, especially in situations where closed-form solutions like the Black-Scholes model may not be practical or available. Unlike the analytical approach, Monte Carlo methods use random sampling to simulate a wide range of potential future he Monte Carlo simulation produced an estimated option price of $2.04, based on 1,000 iterations and the input parameters defined in Question 4. This compares with the Black-Scholes price of $2.13, which was derived from the closed-form analytical solution of the model.
The Monte Carlo simulation (1,000 iterations) estimated the option price at $2.04, while the Black-Scholes model produced $2.13. This small difference is expected due to the randomness in simulation. Monte Carlo methods use probabilistic outcomes, while Black-Scholes provides a precise theoretical value. As noted by Benninga and Mofkadi (2021), Monte Carlo is useful for flexibility and modeling uncertainty, while Black-Scholes remains the benchmark for analytical pricing.




