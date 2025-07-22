Vasicek Interest rate model is a mathematical method of modelling the movement and evolution of interest rates. It is a single factor model that predicts the evolution of interest rate prices over time. Since it is a single factor model, it takes into account only the market risk.
Apart from Vasicek, there are other single factor models that exists:
	i. *Merton Model -* This is helpful in determining the company's credit risk
	ii. *Cox-Ingersoll-Ross Model -* determines the interest rates in future by incorporating volatility, mean, and spread
	iii. *Hull-White Model -* Used to price interest rate derivatives. Assumes volatility will be low when short-term interest rates are near zero.
$$dr_t = \alpha(\mu -r_t)dt + \sigma dW_t$$
Where:

- $d_t$ - change in interest rate
- $\alpha$ - $(\alpha > 0)$ speed of mean reversion i.e. how fast the interest rate returns to the mean
- $\mu$ - long term average rate
- $r_t$ - interest rate at time $t$
- $dt$ - small change in time $\frac{1}{252}$
- $\sigma$ - $\sigma > 0$ volatility of interest rate
- $dW_t$ - Wiener process (Brownian Motion). The randomness or unpredictability fluctuation in interest over time. $dW_t = Z_t  \sqrt{\Delta t}$  where $Z_t$ is a random generated number from a standard normal distribution.
$\alpha(\mu-r_t)dt$ is the deterministic part (drift) and $\sigma dW_t$ is the stochastic part.

## Model Assumptions
The Vasicek Interest rate model makes the following:
	I. Interest rates follow a mean-reverting stochastic process
	II. Normally distributed interest rates. This occurs as the model is based on Brownian motion accounting for the possibility of negative interest rates which is a limitation.
	III. No arbitrage. Since the model is typically used under the risk-neutral measure, it assumes arbitrage-free markets.
## Model Calibration

For the Vasicek model to be useful, model calibration is necessary. Model calibration refers to the process of fine turning the model so that its output closely reflect the reality. In reference to the Vasicek model, we calibrate $a,b$ and $\sigma$. 

### Step 1: Discretize the Model
Finance data is usually provided in discrete intervals e.g. daily, monthly, or yearly. Since Vasicek Model is a continuous time stochastic differential equation, we will have to make it discrete to use it with our discrete data
$$r_{t+1} = r_t + \alpha(\mu - r_t)\Delta t + \sigma \sqrt{\Delta t \epsilon _{t} }$$
Where:
- $\Delta t : -$ time increment between observations $\frac{1}{252}$
- $\alpha (\mu -r_t) \Delta t :-$ deterministic component representing the pull towards the mean
- $\epsilon _t : -$ stochastic component capturing the random stock at time $t$
- $\epsilon _t \sim \mathcal{N}(0,1) :-$ standard normal random variable
# References
https://www.soa.org/48e9a7/globalassets/assets/files/resources/research-report/2023/interest-rate-model-calibration-study.pdf

https://www.thefinanalytics.com/post/calibrating-the-vasicek-model-using-historical-interest-rate-data