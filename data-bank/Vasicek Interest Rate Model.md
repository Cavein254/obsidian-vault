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
## Calibration
*Maximum Likelihood Estimator (MLE)* is a method which is used to find the best fitting parameters for a mathematical model, based on obtained data.
In the case of the vasicek model, the MLE adjusts the $a,b$ and $\sigma$. 
This is done using the following steps:
### Step 1 - Calculate the change in interest rates
This is done by getting the change in actual interest rates and also finding the change in interest rates given by the vasicek model.

| Actual Interest rate $(r_{tA})$ | Vasicek Interest Rate $(r_{tV}$) | $\Delta r_{tA}$ | $\Delta r_{tV}$ |
| :-----------------------------: | -------------------------------- | --------------- | --------------- |
|               5.1               | 4.5                              | 5.9-5.1         | 4.88 - 4.5      |
|               5.9               | 4.88                             |                 |                 |
|                .                | .                                |                 |                 |
|                .                | .                                |                 |                 |

### Step 2 - Calculate the residual
| $\Delta r_{tA}$ | $\Delta r_{tV}$ | Residual ($\Delta r_{tA}$ - $\Delta r_{tV}$) |
| :-------------: | --------------- | -------------------------------------------- |
|      0.002      | 0.0015          | 0.002 - 0.0015                               |
### Step 3 - Take Likelihood Function
Take the normal distribution of the residuals with mean = 0 and std = $\sigma$

| $\Delta r_{tA}$ | $\Delta r_{tV}$ | Residual ($\Delta r_{tA}$ - $\Delta r_{tV}$) | Normal Distribution |
| :-------------: | --------------- | -------------------------------------------- | ------------------- |
|      0.002      | 0.0015          | 0.002 - 0.0015                               |                     |

### Step 4 - Take log Likelihood Function

| $\Delta r_{tA}$ | $\Delta r_{tV}$ | Residual ($\Delta r_{tA}$ - $\Delta r_{tV}$) | Normal distribution | Log Normal Distribution |
| :-------------: | --------------- | -------------------------------------------- | ------------------- | ----------------------- |
|      0.002      | 0.0015          | 0.002 - 0.0015                               |                     |                         |

# References
https://www.soa.org/48e9a7/globalassets/assets/files/resources/research-report/2023/interest-rate-model-calibration-study.pdf
