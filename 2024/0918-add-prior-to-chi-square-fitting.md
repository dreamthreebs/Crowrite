# 0918-add prior to chi square fitting

#### 1. Gaussian Prior

A Gaussian (normal) prior on a parameter $\theta$ with mean $\mu$ and standard deviation $\sigma$ is expressed as:

$$
P(\theta) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left( -\frac{(\theta - \mu)^2}{2\sigma^2} \right).
$$

This function indicates that the parameter $\theta$ is more likely to be close to the mean $\mu$, with a spread governed by $\sigma$.

#### 2. Log-Likelihood of the Gaussian Prior

In Bayesian analysis, the prior is incorporated by adding the log of the prior probability to the log-likelihood of the data. Since the goal is to minimize a function (as in chi-square fitting), we use the negative log of the prior:

$$
-\log P(\theta) = \frac{(\theta - \mu)^2}{2\sigma^2} + \frac{1}{2}\log(2\pi\sigma^2).
$$

#### 3. Simplifying the Prior Contribution

For the purpose of adding this term to the chi-square, we can ignore the constant part $\frac{1}{2}\log(2\pi\sigma^2)$ since it does not depend on the parameter $\theta$. We focus on the part that depends on $\theta$:

$$
-\log P(\theta) \propto \frac{(\theta - \mu)^2}{2\sigma^2}.
$$

#### 4. Incorporating into Chi-Square

To incorporate this prior into the chi-square fitting procedure, we need to add a term to the chi-square statistic that represents the prior's penalty on deviations of $\theta$ from $\mu$. The conventional chi-square statistic has a factor of 1/2 in the exponent:

$$
\chi^2_{\text{prior}} = \sum_j \frac{(\theta_j - \mu_j)^2}{\sigma_j^2}.
$$

#### 5. Full Modified Chi-Square

The total chi-square to minimize becomes:

$$
\chi^2_{\text{total}} = \chi^2_{\text{data}} + \chi^2_{\text{prior}},
$$

where:

*   $\chi^2\_{\text{data\}}$ is the standard chi-square term representing the fit to the data:

    $$
    \chi^2_{\text{data}} = \sum_{i=1}^{N} \frac{(y_i - f(x_i; \theta))^2}{\sigma_i^2}.
    $$
*   $\chi^2\_{\text{prior\}}$ is the term derived from the Gaussian prior:

    $$
    \chi^2_{\text{prior}} = \sum_j \frac{(\theta_j - \mu_j)^2}{\sigma_{\theta_j}^2}.
    $$

These expressions now use LaTeX formatting for both inline and standalone equations.
