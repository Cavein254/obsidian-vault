$$dr_t = a(b -r_t)dt + \sigma dW_t$$
Where:
- $d_t$ - change in interest rate
- $a$ - speed of mean reversion i.e. how fast the interest rate returns to the mean
- $b$ - long term average rate
- $r_t$ - interest rate at time $t$
- $dt$ - small change in time $\frac{1}{252}$
- $\sigma$ - volatility of interest rate
- $dW_t$ - Wiener process (Brownian Motion). The randomness or unpredictability fluctuation in interest over time. $dW_t = Z_t  \sqrt{\Delta t}$  where $Z_t$ is a random generated number from a standard normal distribution.
$a(b-r_t)dt$ is the deterministic part and $\sigma dW_t$ is the stochastic part.


## Calibration
*Maximum Likelihood Estimator (MLE)* is a method which is used to find the best fitting parameters for a mathematical model, based on obtained data.