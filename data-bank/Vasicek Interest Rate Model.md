Vasicek Interest rate model is a mathematical method of modelling the movement and evolution of interest rates. It is a single factor model that predicts the evolution of interest rate prices over time. Since it is a single factor model, it takes into account only the market risk.
Apart from Vasicek, there are other single factor models that exists:
	i. *Merton Model -* This is helpful in determining the company's credit risk
	ii. *Cox-Ingersoll-Ross Model -* determines the interest rates in future by incorporating volatility, mean, and spread
	iii. *Hull-White Model -* Used to price interest rate derivatives. Assumes volatility will be low when short-term interest rates are near zero.
$$dr_t = a(b -r_t)dt + \sigma dW_t$$
Where:

- $d_t$ - change in interest rate
- $a$ - $(a > 0)$ speed of mean reversion i.e. how fast the interest rate returns to the mean
- $b$ - long term average rate
- $r_t$ - interest rate at time $t$
- $dt$ - small change in time $\frac{1}{252}$
- $\sigma$ - $\sigma > 0$ volatility of interest rate
- $dW_t$ - Wiener process (Brownian Motion). The randomness or unpredictability fluctuation in interest over time. $dW_t = Z_t  \sqrt{\Delta t}$  where $Z_t$ is a random generated number from a standard normal distribution.
$a(b-r_t)dt$ is the deterministic part (drift) and $\sigma dW_t$ is the stochastic part.

## Model Assumptions
The Vasicek Interest rate model makes the following:
	I. Interest rates follow a mean-reverting stochastic process
	II. Normally distributed interest rates. This occurs as the model is based on Brownian motion accounting for the possibility of negative interest rates which is a limitation.
	III. No arbitrage. Since the model is typically used under the risk-neutral measure, it assumes arbitrage-free markets.
## Model Calibration

For the Vasicek model to be useful, model calibration is necessary. Model calibration refers to the process of fine turning the model so that its output closely reflect the reality. In reference to the Vasicek model, we calibrate $a,b$ and $\sigma$. 

### Step 1: Discretize the Model
Finance data is usually provided in discrete intervals e.g. daily, monthly, or yearly. Since Vasicek Model is a continuous time stochastic differential equation, we will have to make it discrete to use it with our discrete data. Using the Euler-Maruyama discretisation method we have:
$$r_{t+1} = r_t + a(b - r_t)\Delta t + \sigma \sqrt{\Delta t} \epsilon _{t} $$
Where:
- $\Delta t : -$ time increment between observations $\frac{1}{252}$
- $a (b -r_t) \Delta t :-$ deterministic component representing the pull towards the mean
- $\epsilon _t : -$ stochastic component capturing the random stock at time $t$
- $\epsilon _t \sim \mathcal{N}(0,1) :-$ standard normal random variable

The above equation can be rewritten as:
$$r_{t+1} = r_t - ar_t \Delta t + ab \Delta t + \sigma \sqrt{\Delta t} \epsilon_t$$
$$r_{t+1} = (1 - a \Delta t)r_t + ab \Delta t + \sigma \sqrt{\Delta t} \epsilon_t$$
Letting $\alpha = (1-a\Delta t)$, $\beta = ab\Delta t$ and $\xi = \sigma \sqrt{\Delta t} \epsilon_t$ 
$$r_{t+1}  = \alpha r_t + \beta + \xi$$
### Step 2: Use OLS to estimate the parameters $\alpha$ and $\beta$
$$\hat{a} = - \frac{In(\hat{\beta})}{\Delta t}$$
$$\hat{b} = \frac{\hat{\alpha}}{\Delta t(1 - \hat{\beta})}$$
### Step 3: Estimate $\sigma$
From residuals $\epsilon_t = r_{t +1} - \hat{\alpha}- \hat{\beta} r_t$, Compute
$$\hat{\sigma} = \sqrt{\frac{Var(\epsilon_t)}{\Delta t}}$$
### Step 4: Validation
- Check residual for normality and independence
- Compare model with yield curve or bond prices to observed market data

## Alternatively, using MLE
Using the maximum Likelihood Method (MLE) method to calibrate Vasicek model is more efficient compared to the OLS method. 
### Step 1: Get the Transition Distribution
The vasicek model has a closed-form solution for its transition (conditional) distribution:
$$r_{t+1}| r_t \sim \mathcal{N}(\mu_t, \sigma^2 _t) $$
where:
- $\mu_t = b + (r_t -b)e^{-\alpha \Delta t}$
- $\sigma^2_t = \frac{\sigma^2}{2a}(1-e^{-2a\Delta t})$
this gives the probability density of observing $r_{t + \Delta t}$ under parameters $a,b,\sigma$

### Step 2: Write the Log-Likelihood fn
Given a time series of interest rates $r_0, r_1..., r_n$ at interval $\Delta t$, the log-likelihood is:
$$\mathcal{L}(a,b,\sigma) = \sum^n_{i = 1}log f(r_i|r_{i-1}; a,b,\sigma)$$
where each term in the sum is the log of the normal density:
$$log f(r_i|r_i-1) = - \frac{1}{2}log(2\pi \sigma^2_t)- \frac{r_i -\mu_{i-1}^2}{2\sigma^2_t}$$
where:
- $\mu_t = b + (r_t -b)e^{-\alpha \Delta t}$
- $\sigma^2_t = \frac{\sigma^2}{2a}(1-e^{-2a\Delta t})$
### Step 3: Maximize the Log-Likelihood
Now that you have a function L(a,b,σ)L(a,b,σ), use a numerical optimizer to find the parameter values that maximize it.

### Step 4: Evaluate the fit
After finding the optimal a,b,σ:
- Simulate paths or calculate bond prices
- Compare to actual data or yields
- Plot residuals to verify normality and independence
# References
https://www.soa.org/48e9a7/globalassets/assets/files/resources/research-report/2023/interest-rate-model-calibration-study.pdf

https://www.thefinanalytics.com/post/calibrating-the-vasicek-model-using-historical-interest-rate-data