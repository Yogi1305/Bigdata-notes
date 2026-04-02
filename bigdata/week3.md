# 📘 Week 3: Statistical Inference — Complete Reference Guide

## Statistical Inference — Overview

**Statistical Inference** means taking decisions about a population based on a sample. We bridge the gap between unknown population parameters and known sample statistics.

**Flow**: Population (Unknown) → Collect Sample (Known) → Make Decision

### Two Branches of Inference

| **Estimation** | **Hypothesis Testing** |
|----------------|------------------------|
| "What is the average height of people in Antarctica?" (No idea) | "Is the average height in India above 7 feet?" (Have some idea) |
| We estimate the parameter from scratch | We verify a claim about the parameter |

---

## Types of Estimation

### Point Estimation
**Definition**: A single value guess for a population parameter.

**Example**: Estimating population mean μ using sample mean X̄
- Sample: {78, 82, 85, 88, 76}
- Point estimate: X̄ = 81.8

### Interval Estimation
**Definition**: A range of values that likely contains the parameter, with a specified level of confidence.

**Example**: "We are 95% confident that μ lies between 4.2 and 7.8"

---

## Confidence Interval — Definition

Let **X₁,...,Xₙ** be an i.i.d. sample with parameter **θ**, and **0 < α < 1**. A **100(1−α)% confidence interval** is an interval **[c₁, c₂]** (both functions of the sample) such that:


$$
P(\theta \in [c_1, c_2]) = 1 - \alpha
$$


Where:
- **(1−α)** = confidence level (e.g., 0.95 for 95%)
- **α** = significance level (e.g., 0.05)
- **c₁, c₂** = lower and upper confidence limits

**Interpretation**: If we were to take many samples and construct CIs, (1−α)% of them would contain the true parameter.

**Key Insight**: The wider the interval, the more confident we are — but the less precise our estimate becomes.

---

## Foundational Results Used in Confidence Intervals

### 4a. Weak Law of Large Numbers (WLLN)

**Definition**: For i.i.d. X₁,...,Xₙ with mean μ, for any ε > 0:


$$
\lim_{n \to \infty} P(|\bar{X} - \mu| \geq \epsilon) = 0
$$


Also: $Var(\bar{X}) = \frac{\sigma^2}{n}$

**Explanation**: As sample size grows, the sample mean converges to the population mean. The variance of the sample mean decreases as n increases.

**Practical Meaning**: With large samples, our sample mean becomes a reliable estimate of the population mean.

---

### 4b. Central Limit Theorem (CLT)

**Definition**: For i.i.d. X₁,...,Xₙ with mean μ and variance σ²:


$$
Z = \frac{\bar{X} - \mu}{\sigma/\sqrt{n}} \xrightarrow{d} N(0, 1) \quad \text{as } n \to \infty
$$


**Explanation**: Even if the original population is not normally distributed, the sampling distribution of the sample mean approaches normality as n grows large (typically n ≥ 30).

**Why It Matters**: We can use normal-based methods for inference even with non-normal populations, provided we have large enough samples.

---

### 4c. t-Distribution

**Definition**: If X₁,...,Xₙ ~ i.i.d. N(μ, σ²) and S² is sample variance:


$$
T = \frac{\bar{X} - \mu}{S/\sqrt{n}} \sim t_{n-1}
$$


**Explanation**: When σ is unknown and estimated by S, the test statistic follows a t-distribution with n−1 degrees of freedom.

**Key Characteristics**:
- Heavier tails than normal distribution
- Accounts for additional uncertainty from estimating σ
- Approaches N(0,1) as n → ∞

**When Used**: Confidence intervals and hypothesis tests when σ is unknown.

---

### 4d. Chi-squared Distribution

**Definition**: If X₁,...,Xₙ ~ i.i.d. N(μ, σ²):


$$
Q = \frac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1)
$$


**Explanation**: The ratio of sample variance to population variance (scaled) follows a chi-squared distribution.

**Key Characteristics**:
- Non-symmetric (right-skewed)
- Only takes positive values
- Degrees of freedom = n−1

**When Used**: Confidence intervals and hypothesis tests for population variance.

---

## CI for Mean — Variance Known (Z-interval)

### When to Use
- Population variance **σ² is known**
- Population is normal OR n is large (≥30, by CLT)

### Test Statistic

$$
Z = \frac{\bar{X} - \mu}{\sigma/\sqrt{n}} \sim N(0,1)
$$


### Formula

$$
CI = \left[\bar{X} - z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}}, \quad \bar{X} + z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}}\right]
$$


### Common Critical Values

| Confidence Level | α | α/2 | z_{α/2} |
|------------------|---|---|---------|
| 90% | 0.10 | 0.05 | 1.645 |
| 95% | 0.05 | 0.025 | 1.96 |
| 99% | 0.01 | 0.005 | 2.576 |

### Example: Manufacturing Quality Control

**Scenario**: A factory produces light bulbs with known lifespan variance σ² = 100 hours². A sample of 25 bulbs has average lifespan X̄ = 780 hours. Find 95% CI for true mean lifespan.

**Step-by-Step Solution**:

1. **Identify given values**:
   - σ = √100 = 10
   - n = 25
   - X̄ = 780
   - z_{0.025} = 1.96

2. **Calculate standard error**:
   
$$
SE = \frac{\sigma}{\sqrt{n}} = \frac{10}{\sqrt{25}} = \frac{10}{5} = 2
$$


3. **Calculate margin of error**:
   
$$
ME = z_{\alpha/2} \cdot SE = 1.96 \times 2 = 3.92
$$


4. **Construct confidence interval**:
   
$$
CI = [780 - 3.92, 780 + 3.92] = [776.08, 783.92]
$$


5. **Interpretation**: We are 95% confident that the true average lifespan of all bulbs produced by this factory is between 776.08 and 783.92 hours.

**Note**: For non-normal populations, the CLT allows this approach for large n.

---

## CI for Mean — Variance Unknown (t-interval)

### When to Use
- Population variance **σ² is unknown**
- Population is approximately normal

### Test Statistic

$$
T = \frac{\bar{X} - \mu}{S/\sqrt{n}} \sim t_{n-1}
$$


### Formula

$$
CI = \left[\bar{X} - t_{\alpha/2, n-1} \cdot \frac{S}{\sqrt{n}}, \quad \bar{X} + t_{\alpha/2, n-1} \cdot \frac{S}{\sqrt{n}}\right]
$$


### Example: Watermelon Weights

**Scenario**: 10 watermelon weights (lbs) measured. Find 95% CI for true mean weight.

**Given Data**:
- X̄ = 9.259 lbs
- S² = 3.96 (so S = 1.99)
- n = 10
- df = 9
- t_{0.025,9} = 2.262

**Step-by-Step Solution**:

1. **Calculate standard error**:
   
$$
SE = \frac{S}{\sqrt{n}} = \frac{1.99}{\sqrt{10}} = \frac{1.99}{3.162} = 0.629
$$


2. **Calculate margin of error**:
   
$$
ME = t_{\alpha/2, n-1} \cdot SE = 2.262 \times 0.629 = 1.423
$$


3. **Construct confidence interval**:
   
$$
CI = [9.259 - 1.423, 9.259 + 1.423] = [7.836, 10.682] \approx [7.84, 10.68]
$$


4. **Interpretation**: We are 95% confident that the true mean weight of watermelons in this population is between 7.84 and 10.68 pounds.

**Key Difference from Z-interval**: Uses S (sample standard deviation) instead of σ, and t-table instead of Z-table. The t-distribution has heavier tails, giving a wider interval to account for additional uncertainty.

---

## CI for Variance — Chi-squared Interval

### When to Use
- Estimating **population variance σ²**
- Population mean μ is unknown

### Test Statistic

$$
Q = \frac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1)
$$


### Formula

$$
CI = \left[\frac{(n-1)S^2}{\chi^2_{\alpha/2, n-1}}, \quad \frac{(n-1)S^2}{\chi^2_{1-\alpha/2, n-1}}\right]
$$


**Important**: The chi-squared distribution is **not symmetric**, so we use different critical values for the lower and upper bounds. The larger chi-squared value goes in the denominator for the lower bound, and vice versa.

### Example: Watermelon Weight Variance

**Scenario**: Using same data as above (n=10, S²=3.96), find 95% CI for true variance.

**Given Data**:
- n = 10, df = 9
- S² = 3.96
- χ²_{0.025,9} = 19.02 (upper critical value)
- χ²_{0.975,9} = 2.70 (lower critical value)

**Step-by-Step Solution**:

1. **Calculate numerator**:
   
$$
(n-1)S^2 = 9 \times 3.96 = 35.64
$$


2. **Calculate lower bound**:
   
$$
\text{Lower} = \frac{35.64}{19.02} = 1.87
$$


3. **Calculate upper bound**:
   
$$
\text{Upper} = \frac{35.64}{2.70} = 13.20
$$


4. **Construct confidence interval**:
   
$$
CI = [1.87, 13.20]
$$


5. **Interpretation**: We are 95% confident that the true variance of watermelon weights is between 1.87 and 13.20 lbs².

---

## CI for Bernoulli Parameter p

### When to Use
- Estimating **success probability p** from Bernoulli trials
- Large n (typically np ≥ 10 and n(1−p) ≥ 10)

### Estimator

$$
\hat{p} = \frac{1}{n}\sum_{i=1}^{n} X_i = \frac{\text{number of successes}}{n}
$$


### Test Statistic (large n)

$$
Z = \frac{\hat{p} - p}{\sqrt{p(1-p)/n}} \xrightarrow{} N(0,1)
$$


### Formula (replace p with p̂ for practical use)

$$
CI = \left[\hat{p} - z_{\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}, \quad \hat{p} + z_{\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}\right]
$$


### Example: Political Polling

**Scenario**: In a survey of 1000 voters, 420 support Candidate A. Find 95% CI for true proportion of support.

**Step-by-Step Solution**:

1. **Calculate sample proportion**:
   
$$
\hat{p} = \frac{420}{1000} = 0.42
$$


2. **Calculate standard error**:
   
$$
SE = \sqrt{\frac{\hat{p}(1-\hat{p})}{n}} = \sqrt{\frac{0.42 \times 0.58}{1000}} = \sqrt{\frac{0.2436}{1000}} = \sqrt{0.0002436} = 0.0156
$$


3. **Calculate margin of error**:
   
$$
ME = z_{0.025} \times SE = 1.96 \times 0.0156 = 0.0306
$$


4. **Construct confidence interval**:
   
$$
CI = [0.42 - 0.0306, 0.42 + 0.0306] = [0.3894, 0.4506]
$$


5. **Interpretation**: We are 95% confident that between 38.94% and 45.06% of all voters support Candidate A.

**Note**: This approximation improves as sample size grows. For small samples, exact methods (Clopper-Pearson) should be used.

---

## Part 2: Hypothesis Testing

## Hypothesis Testing — Core Idea

**Definition**: A statistical method used when we have some idea about a population parameter and want to evaluate it against evidence from data, rather than estimating from scratch.

### Comparison: Estimation vs. Hypothesis Testing

| | **Estimation** | **Hypothesis Testing** |
|---|---|---|
| **Question** | "What is the average height in Antarctica?" | "Is the average height in India above 7ft?" |
| **Prior Knowledge** | No idea | Have some specific claim |
| **Goal** | Find the parameter value | Verify a claim about the parameter |

---

## Key Components of a Statistical Test

A statistical test is a rule to evaluate an assertion (H₀) against an alternative (H₁) based on a sample. It involves:

| Component | Description |
|-----------|-------------|
| **Hypotheses** | H₀ (null) vs H₁ (alternative) — competing statements about the parameter |
| **Test Statistic** | A numerical function T of the sample; its behavior is predictable under H₀ and H₁ |
| **Critical Region C** | If T ∈ C, reject H₀ (observations are more likely under H₁) |
| **Decision** | Reject H₀ or fail to reject H₀ |

**Key Principle**: The goal is to determine if there is **overwhelming evidence** to reject H₀. We assume H₀ is true until evidence strongly suggests otherwise.

---

## Type I and Type II Errors

### Error Matrix

| | **H₀ is True** | **H₀ is False** |
|---|---|---|
| **Reject H₀** | ❌ Type I Error (α) | ✅ Correct Decision |
| **Don't Reject H₀** | ✅ Correct Decision | ❌ Type II Error (β) |

### Definitions

| Error | Definition | Probability |
|-------|-----------|-------------|
| **Type I Error** | Rejecting H₀ when it is actually true | α (significance level) |
| **Type II Error** | Failing to reject H₀ when H₁ is actually true | β |
| **Power** | Correctly rejecting false H₀ | 1 − β |

### Medical Analogy

**Scenario**: Testing for cancer
- **H₀**: Patient has cancer
- **H₁**: Patient does not have cancer

| Error | Outcome | Severity |
|-------|---------|----------|
| Type I | Failing to diagnose existing cancer | ← More serious (patient dies untreated) |
| Type II | Wrongly diagnosing healthy patient | Patient undergoes unnecessary treatment |

**Important**: The "more serious" error is designated as Type I — this depends entirely on the context and purpose of the test.

---

## Coin Toss Example — Tradeoff Between Error Types

### Setup
- **H₀**: p = 0.5 (coin is fair)
- **H₁**: p = 0.6 (coin is biased toward heads)
- **n** = 10 tosses

### Decision Rules and Error Probabilities

| Rule: Reject H₀ if X ≥ | Type I Error (α) | Type II Error (β) |
|---|---|---|
| 6 | 0.37 | 0.36 |
| 7 | 0.171 | 0.61 |
| 8 | 0.054 | 0.83 |
| 9 | 0.01 | 0.95 |
| 10 | 0.0009 | 0.99 |

### Key Insights

1. **Error Tradeoff**: Making the critical region stricter (higher threshold) reduces Type I error but increases Type II error.

2. **Sample Size Effect**: With n = 1000 (instead of 10), both errors become extremely small simultaneously. Larger n improves both types of accuracy.

3. **Cannot Optimize Both**: For fixed sample size, reducing α increases β, and vice versa. You need more data to improve both.

---

## Z-Test for Mean (σ Known)

### Setup
- X ~ N(μ, σ²), σ known
- Test H₀: μ = c₁ vs H₁: μ = c₂ (where c₂ > c₁, one-sided test)

### Test Statistic

$$
Z = \frac{\bar{X} - c_1}{\sigma/\sqrt{n}} \sim N(0,1) \quad \text{under H}_0
$$


### Decision Rule
Reject H₀ if:

$$
\bar{X} \geq c_1 + z_{\alpha} \cdot \frac{\sigma}{\sqrt{n}}
$$


Or equivalently, reject if Z ≥ z_α

### Error Probabilities

**Type I Error** (chosen by researcher):

$$
\alpha = P(Z \geq z_{\alpha})
$$


**Type II Error**:

$$
\beta = P\left(Z \leq z_{\alpha} + \frac{c_1 - c_2}{\sigma/\sqrt{n}}\right)
$$


### Example: Teaching Method Effectiveness

**Scenario**: 
- Traditional method: μ = 70, σ = 10
- Claimed new method: μ = 75
- Sample: n = 25
- Test at α = 0.05

**Step-by-Step Solution**:

1. **State hypotheses**:
   - H₀: μ = 70
   - H₁: μ = 75

2. **Find critical value**:
   - z_{0.05} = 1.645
   - 
$$
\bar{X}_{crit} = 70 + 1.645 \times \frac{10}{\sqrt{25}} = 70 + 1.645 \times 2 = 73.29
$$


3. **Decision rule**: Reject H₀ if sample mean ≥ 73.29

4. **Calculate Type II error**:
   
$$
\beta = P\left(Z \leq 1.645 + \frac{70-75}{10/\sqrt{25}}\right) = P(Z \leq 1.645 - 2.5) = P(Z \leq -0.855) = 0.196
$$


5. **Power**: 1 − β = 0.804

**Interpretation**: If the true mean is 75, we have an 80.4% chance of detecting this improvement with our test.

### Effect of Sample Size

| n | Critical X̄ | Type I Error (α) | Type II Error (β) |
|---|------------|------------------|-------------------|
| 25 | 73.29 | 0.050 | 0.196 |
| 100 | 71.65 | 0.050 | 0.00003 |

**Key Finding**: Larger sample size maintains the same α while dramatically reducing β. Critical value formula: $\bar{X}_{crit} = \mu_0 + z_{\alpha} \cdot \frac{\sigma}{\sqrt{n}}$

---

## t-Test for Mean (σ Unknown)

### Setup
- X ~ N(μ, σ²), σ **unknown**
- Test H₀: μ = c₁ vs H₁: μ = c₂

### Test Statistic

$$
T = \frac{\bar{X} - c_1}{S/\sqrt{n}} \sim t_{n-1} \quad \text{under H}_0
$$


### Decision Rule
Reject H₀ if:

$$
\bar{X} \geq c_1 + t_{\alpha, n-1} \cdot \frac{S}{\sqrt{n}}
$$


### Error Probabilities

**Type I Error**:

$$
\alpha = P(T \geq t_{\alpha, n-1})
$$


**Type II Error**:

$$
\beta = P\left(T \leq t_{\alpha, n-1} + \frac{c_1 - c_2}{S/\sqrt{n}}\right)
$$


### Example: Drug Blood Pressure Test

**Scenario**:
- Standard drug reduces BP by: μ = 10 mmHg
- New drug claimed: μ = 15 mmHg
- Sample: n = 25, s = 5
- Test at α = 0.05

**Step-by-Step Solution**:

1. **State hypotheses**:
   - H₀: μ = 10
   - H₁: μ = 15

2. **Find critical value**:
   - df = 24, t_{0.05,24} = 1.711
   - 
$$
\bar{X}_{crit} = 10 + 1.711 \times \frac{5}{\sqrt{25}} = 10 + 1.711 \times 1 = 11.711
$$


3. **Decision rule**: Reject H₀ if sample mean ≥ 11.711

4. **Calculate Type II error**:
   
$$
\beta \approx 0.0006
$$
 (very small!)

5. **Power**: 1 − β ≈ 0.9994

**Interpretation**: Very high probability (99.94%) of detecting if the new drug truly reduces blood pressure by 15 mmHg instead of 10 mmHg.

### Effect of Sample Size

| n | Critical X̄ | Type I Error (α) | Type II Error (β) |
|---|------------|------------------|-------------------|
| 25 | 11.71 | 0.050 | 0.0006 |
| 50 | 11.40 | 0.050 | 0.0000005 |
| 75 | 11.29 | 0.050 | < 10⁻⁹ |

**Key Finding**: Larger sample size dramatically reduces β while maintaining α at the chosen level.

---

## p-value

### Definition
The **p-value** is the probability, assuming H₀ is true, of observing a test statistic at least as extreme as what was actually observed from the sample.

### Formula (one-sided test for mean)

$$
\text{p-value} = P(Y \geq X | H_0) = P\left(Z \geq \frac{\sqrt{n}(\bar{X} - c)}{\sigma}\right)
$$


Where Y is a random future sample mean and X is the observed sample mean.

### Decision Rule

| Condition | Action | Interpretation |
|-----------|--------|----------------|
| p-value < α | Reject H₀ | Sample is inconsistent with H₀ |
| p-value ≥ α | Fail to reject H₀ | Sample is consistent with H₀ |

### p-value Interpretation Guide

| p-value Range | Evidence Against H₀ |
|-------------|---------------------|
| p > 0.10 | Little or no evidence |
| 0.05 < p ≤ 0.10 | Weak evidence |
| 0.01 < p ≤ 0.05 | Moderate evidence |
| p ≤ 0.01 | Strong evidence |
| p ≤ 0.001 | Very strong evidence |

### Example: Coin Fairness Test

**Scenario**: Test if coin is fair (p = 0.5). Toss 10 times, get 7 heads.

**Calculation**:

$$
\text{p-value} = P(X \geq 7 | p=0.5) = \sum_{k=7}^{10} \binom{10}{k}(0.5)^{10} = \frac{120}{1024} \approx 0.1719
$$


**Decision** (with α = 0.05):
- 0.1719 > 0.05
- **Fail to reject H₀**

**Interpretation**: There is not enough evidence to conclude the coin is biased. Getting 7 or more heads in 10 flips is not unusual for a fair coin.

---

## 📊 Master Summary Table

| Concept | Test Statistic | Distribution | When to Use |
|---------|---------------|------------|-------------|
| **CI for μ (σ known)** | $Z = \frac{\bar{X}-\mu}{\sigma/\sqrt{n}}$ | N(0,1) | σ is known |
| **CI for μ (σ unknown)** | $T = \frac{\bar{X}-\mu}{S/\sqrt{n}}$ | $t_{n-1}$ | σ is unknown |
| **CI for σ²** | $Q = \frac{(n-1)S^2}{\sigma^2}$ | $\chi^2_{n-1}$ | Estimating variance |
| **CI for p (Bernoulli)** | $Z = \frac{\hat{p}-p}{\sqrt{p(1-p)/n}}$ | N(0,1) | Large n, estimating proportion |
| **Z-test for μ** | $Z = \frac{\bar{X}-c}{\sigma/\sqrt{n}}$ | N(0,1) | σ known, hypothesis test |
| **t-test for μ** | $T = \frac{\bar{X}-c}{S/\sqrt{n}}$ | $t_{n-1}$ | σ unknown, hypothesis test |

---

## ⚡ Golden Rules to Remember

| # | Rule | Explanation |
|---|------|-------------|
| 1 | **σ known → use Z** | Normal distribution table |
| 2 | **σ unknown → use t** | t-table with n−1 degrees of freedom |
| 3 | **Variance estimation → use χ²** | Chi-squared distribution |
| 4 | **Larger n → smaller errors** | Reduces both Type I and Type II errors |
| 5 | **p-value < α → Reject H₀** | Evidence is strong enough |
| 6 | **Error tradeoff** | Can't reduce one error without increasing the other (for fixed n) |
| 7 | **Estimation vs. Testing** | Estimation = no prior knowledge; Testing = prior belief being verified |

---

## Common Misconceptions to Avoid

| Misconception | Correct Understanding |
|-------------|----------------------|
| "95% CI means 95% probability the parameter is in this interval" | The parameter is fixed; the interval is random. 95% of similarly constructed intervals would contain the parameter |
| "Failing to reject H₀ means H₀ is true" | Only means insufficient evidence against H₀; H₀ may still be false |
| "p-value is probability H₀ is true" | p-value is P(data\|H₀), not P(H₀\|data) |
| "Statistical significance = practical importance" | A result can be statistically significant but have negligible practical effect |
| "Smaller p-value means larger effect" | p-value depends on sample size; effect size is separate |

---

## Key Formulas Quick Reference

### Confidence Intervals
| Parameter | Formula |
|-----------|---------|
| μ (σ known) | $\bar{X} \pm z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}}$ |
| μ (σ unknown) | $\bar{X} \pm t_{\alpha/2, n-1} \cdot \frac{S}{\sqrt{n}}$ |
| σ² | $\left[\frac{(n-1)S^2}{\chi^2_{\alpha/2, n-1}}, \frac{(n-1)S^2}{\chi^2_{1-\alpha/2, n-1}}\right]$ |
| p | $\hat{p} \pm z_{\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}$ |

### Hypothesis Tests
| Test | Test Statistic | Reject H₀ if |
|------|---------------|--------------|
| Z-test (μ) | $Z = \frac{\bar{X}-\mu_0}{\sigma/\sqrt{n}}$ | $Z \geq z_\alpha$ or p-value < α |
| t-test (μ) | $T = \frac{\bar{X}-\mu_0}{S/\sqrt{n}}$ | $T \geq t_{\alpha, n-1}$ or p-value < α |

---

*This guide covers all concepts from Week 3 of Statistical Inference. Mastery requires both understanding these foundations and practicing with varied problems.*