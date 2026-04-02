# Week 2 - Complete Statistical Inference Notes
## Full detailed notes with formulas, derivations, explanations, and examples

---

## Table of Contents

1. [What is Statistical Inference?](#1-what-is-statistical-inference)
2. [Key Definitions and Setup](#2-key-definitions-and-setup)
3. [Unbiasedness](#3-unbiasedness)
4. [Asymptotics and Consistency](#4-asymptotics-and-consistency)
5. [Consistent Asymptotically Normal (CAN) Estimators](#5-consistent-asymptotically-normal-can-estimators)
6. [Maximum Likelihood Estimation (MLE)](#6-maximum-likelihood-estimation-mle)
7. [Method of Moments (MoM)](#7-method-of-moments-mom)
8. [Comparison of All Concepts](#8-comparison-of-all-concepts)
9. [Complete Summary Tables](#9-complete-summary-tables)

---

## 1. What is Statistical Inference?

Statistical inference is the process of using sample data to learn about unknown population quantities.

Because observing an entire population is usually impossible or too expensive, we use a sample and then:

- estimate parameters (for example, mean or variance), and
- test hypotheses (for example, whether a treatment works).

### Main branches

```text
Statistical Inference
|
|-- Estimation
|   |-- Point estimation (single best value)
|   `-- Interval estimation (range of plausible values)
`
|-- Hypothesis testing (decision between competing claims)
```


## Why Do We Need Statistical Inference?

**Real-World Scenario**

A pharmaceutical company develops a new drug. They cannot test it on every person in the world. Instead, they test it on 1000 patients and use the results to infer the drug's effectiveness for the entire population.

**Another Scenario**

An election pollster surveys 2000 voters out of millions. From this sample, they estimate the percentage of votes each candidate will receive.

In both cases, we go from sample to population using statistical inference.

# 2. Key Definitions and Setup

## Population

The population is the entire collection of individuals, items, or observations we want to study.

- **Population size**: N (may be infinite)
- **Described by parameters** such as μ, σ², p, λ

## Sample

A sample is a subset of the population that we actually observe.

- X₁, X₂, …, Xₙ
- **Sample size**: n
- Usually assumed to be i.i.d. (independent and identically distributed)

**What does i.i.d. mean?**

- **Independent**: knowing the value of one observation tells us nothing about the others
- **Identically distributed**: each observation comes from the same probability distribution

## Parameter

A parameter is a fixed but unknown quantity that describes the population.

**Examples:**

| Symbol | Meaning |
|--------|---------|
| μ | population mean |
| σ² | population variance |
| p | population proportion |
| λ | population rate |

## Statistic

A statistic is any function of the sample data.

T = T(X₁, X₂, …, Xₙ)

A statistic does not depend on unknown parameters.

**Common Statistics**

| Statistic | Formula | Estimates |
|-----------|---------|-----------|
| Sample mean | X̄ = (1/n)∑Xᵢ | μ |
| Sample variance | S² = [1/(n-1)]∑(Xᵢ - X̄)² | σ² |
| Sample proportion | p̂ = X̄ | p |
| Sample maximum | X₍ₙ₎ = max(X₁, …, Xₙ) | upper bound |

## Estimator vs Estimate

- An **estimator** is a rule or formula (a random variable).
- An **estimate** is a specific numerical value obtained by plugging in observed data.

**Example**

- Estimator: X̄ = (1/n)∑Xᵢ
- Estimate: if data are 3, 5, 7, then x̄ = 5.

## Sampling Distribution

The sampling distribution of a statistic is the probability distribution of that statistic over all possible samples.

**Example**

If X₁, …, Xₙ ~ N(μ, σ²), then:

X̄ ~ N(μ, σ²/n)

So the sampling distribution of X̄ is normal with:

- mean μ
- variance σ²/n

**Example with numbers**

If μ = 10, σ² = 4, n = 16:

X̄ ~ N(10, 4/16) = N(10, 0.25)

Standard error:

SE(X̄) = σ/√n = 2/4 = 0.5

# 3. Unbiasedness

## Definition

An estimator T is unbiased for parameter θ if:

E(T) = θ

This means that on average, the estimator gives the correct value.

## Bias

The bias of an estimator is:

Bias(T) = E(T) - θ

If Bias(T) = 0, the estimator is unbiased.

## Important Rules for Computing Expectations

**Rule 1: Linearity of Expectation**

E(∑ᵢ Zᵢ) = ∑ᵢ E(Zᵢ)

This works even if the variables are not independent.

**Rule 2: Constant Multiple**

E(cZ) = cE(Z)

**Rule 3: Variance of Sum of Independent Variables**

If Z₁, …, Zₙ are pairwise independent:

Var(∑ᵢ cᵢZᵢ) = ∑ᵢ cᵢ² Var(Zᵢ)

**Rule 4: Variance Formula**

Var(X) = E(X²) - [E(X)]²

## Example 1: Sample Mean is Unbiased for Population Mean

**Setup**

Suppose:
- X₁, …, Xₙ are i.i.d. with E(Xᵢ) = μ
- Define: X̄ = (1/n)∑Xᵢ

**Proof**

E(X̄) = E[(1/n)∑Xᵢ]
= (1/n)E(∑Xᵢ) (by constant multiple rule)
= (1/n)∑E(Xᵢ) (by linearity)
= (1/n)(nμ) = μ

**Conclusion**

E(X̄) = μ

The sample mean is unbiased for the population mean.

**Numerical Example**

Suppose the true population mean is μ = 50.

If we take thousands of samples, each of size n = 10, and compute the sample mean of each, then the average of all those sample means will be approximately 50.

## Example 2: Bernoulli Sample Mean is Unbiased for p

**Setup**

Suppose:
- X₁, …, Xₙ ~ Bernoulli(p)
- Then: E(Xᵢ) = p

**Proof**

E(X̄) = (1/n)∑E(Xᵢ) = (1/n)(np) = p

**Conclusion**

X̄ is unbiased for p.

**Numerical Example**

Suppose a coin has p = 0.7 probability of heads.

We flip it n = 10 times: 1, 1, 0, 1, 1, 1, 0, 1, 1, 0

Sample mean: X̄ = 7/10 = 0.7

In this particular sample, our estimate equals the true value.

## Example 3: Normal Sample Mean is Unbiased

**Setup**

X₁, …, Xₙ ~ N(μ, σ²)

**Proof**

Same as Example 1: E(X̄) = μ

**Additional Result**

For normal data, X̄ itself is normally distributed:

X̄ ~ N(μ, σ²/n)

## Example 4: Finite Population Sampling

**Setup**

A population has values: a₁, a₂, …, aₙ

The population mean is:

μ = (1/N)∑ⱼ aⱼ

We draw a random sample Y₁, …, Yₙ.

**Result**

E(Ȳ) = μ

So the sample mean is unbiased for the population mean even in finite population sampling.

**Numerical Example**

Population: 10, 20, 30, 40, 50

Population mean: μ = (10+20+30+40+50)/5 = 30

We draw a sample of size 3: 20, 30, 50

Sample mean: Ȳ = (20+30+50)/3 = 33.3

This particular sample overestimates μ. But on average across all possible samples of size 3, the sample mean equals 30.

## Unbiased Estimator of Population Variance

**The Two Formulas**

1. **Biased Estimator** (denominator n):

S'² = (1/n)∑(Xᵢ - X̄)²

E(S'²) = [(n-1)/n]σ² ≠ σ²

This is biased downward.

2. **Unbiased Estimator** (denominator n-1):

S² = [1/(n-1)]∑(Xᵢ - X̄)²

E(S²) = σ²

This is unbiased.

**Why n-1?**

When computing deviations from X̄, we lose one degree of freedom because X̄ is itself computed from the data. Dividing by n-1 corrects for this.

**Proof Sketch**

We can show:

∑(Xᵢ - X̄)² = ∑Xᵢ² - nX̄²

Taking expectations:

E[∑(Xᵢ - X̄)²] = nE(Xᵢ²) - nE(X̄²)

We know:

E(Xᵢ²) = Var(Xᵢ) + [E(Xᵢ)]² = σ² + μ²
E(X̄²) = Var(X̄) + [E(X̄)]² = σ²/n + μ²

Substituting:

E[∑(Xᵢ - X̄)²] = n(σ² + μ²) - n(σ²/n + μ²)
= nσ² + nμ² - σ² - nμ²
= (n-1)σ²

Therefore:

E[[1/(n-1)]∑(Xᵢ - X̄)²] = σ²

**Numerical Example**

Data: 2, 4, 6

Mean: X̄ = 4

Deviations squared: (2-4)² = 4, (4-4)² = 0, (6-4)² = 4

Sum of squares: 8

Biased estimate: S'² = 8/3 ≈ 2.667

Unbiased estimate: S² = 8/2 = 4

# 4. Asymptotics and Consistency

## Why Study Asymptotics?

In practice, we want estimators that become better as we collect more data.

As sample size n increases, we want:

1. Estimates to get closer to the true parameter
2. Variability to shrink
3. Wrong estimates to become unlikely

Asymptotics formalizes what happens as n → ∞.

## Weak Consistency (Convergence in Probability)

**Definition**

A sequence of estimators {Tₙ} is weakly consistent for θ if for every ε > 0:

limₙ→∞ P(|Tₙ - θ| < ε) = 1

Equivalent notation: Tₙ →ᴾ θ

**Interpretation**

No matter how small a margin ε we choose, the probability that Tₙ lies within that margin of θ approaches 1.

**Visual Interpretation**

Imagine the sampling distribution of Tₙ as n grows:

For small n:
## this break
<!-- this break -->

The distribution concentrates around θ.

## Strong Consistency (Almost Sure Convergence)

**Definition**

Tₙ is strongly consistent for θ if:

Tₙ →ᵃˢ θ

This means Tₙ converges to θ almost surely, i.e., with probability 1.

**Relationship**

Strong consistency implies weak consistency, but not vice versa.

## Sufficient Conditions for Weak Consistency

**Theorem**

If:

1. E(Tₙ) → θ as n → ∞ (asymptotically unbiased)
2. Var(Tₙ) → 0 as n → ∞ (variance shrinks)

then Tₙ is weakly consistent for θ.

**Proof Idea**

By Chebyshev's inequality:

P(|Tₙ - θ| ≥ ε) ≤ E[(Tₙ - θ)²]/ε²

Now:

E[(Tₙ - θ)²] = Var(Tₙ) + [E(Tₙ) - θ]²

This is the mean squared error (MSE).

If both terms go to zero, then:

P(|Tₙ - θ| ≥ ε) → 0

which means:

P(|Tₙ - θ| < ε) → 1

## Mean Squared Error (MSE)

**Formula**

MSE(T) = E[(T - θ)²] = Var(T) + [Bias(T)]²

**Interpretation**

MSE measures total error:

- Variance: how much the estimator fluctuates
- Bias squared: how far the average estimate is from the truth

If MSE goes to zero, the estimator is consistent.

**Example**

If Tₙ = X̄, then:

Bias = 0
Var(X̄) = σ²/n
MSE(X̄) = σ²/n → 0

So X̄ is consistent.

## Example 1: Sample Mean is Consistent

**Setup**

X₁, …, Xₙ i.i.d. with E(Xᵢ) = μ, Var(Xᵢ) = σ²

**Check Condition 1: Asymptotic Unbiasedness**

E(X̄) = μ → μ ✓

**Check Condition 2: Variance Shrinks**

Var(X̄) = σ²/n → 0 ✓

**Conclusion**

X̄ is consistent for μ.

**Numerical Illustration**

Suppose μ = 50, σ² = 100.

| n | Var(X̄) = 100/n | SD(X̄) |
|---|----------------|--------|
| 1 | 100 | 10 |
| 10 | 10 | 3.16 |
| 100 | 1 | 1 |
| 1000 | 0.1 | 0.316 |
| 10000 | 0.01 | 0.1 |

As n grows, the standard deviation of X̄ shrinks, so the estimate clusters closer to μ = 50.

## Example 2: Sample Median is Consistent (Normal Population)

**Setup**

X₁, …, Xₙ ~ N(μ, σ²)

Let Mₙ denote the sample median.

**Properties of Sample Median**

- E(Mₙ) = μ (by symmetry of normal distribution)
- Var(Mₙ) ≈ πσ²/(2n)

**Check Conditions**

1. E(Mₙ) = μ → μ ✓
2. Var(Mₙ) = πσ²/(2n) → 0 ✓

**Conclusion**

The sample median is consistent for μ.

**Comparison with Sample Mean**

| Estimator | Variance |
|-----------|----------|
| Sample mean | σ²/n |
| Sample median | πσ²/(2n) ≈ 1.571σ²/n |

The sample median has about 57% higher variance than the sample mean. So both are consistent, but the sample mean is more efficient.

**Important Point**

Consistent estimators are not unique. Multiple estimators can be consistent for the same parameter.

## Example 3: Biased but Consistent Estimator of Variance

**Setup**

Define: Sₙ'² = (1/n)∑(Xᵢ - X̄)²

**Is it unbiased?**

We showed: E(Sₙ'²) = [(n-1)/n]σ²

Since (n-1)/n ≠ 1, the estimator is biased.

**Bias**

Bias(Sₙ'²) = [(n-1)/n]σ² - σ² = -σ²/n

**Check Condition 1**

E(Sₙ'²) = [(n-1)/n]σ² → σ² ✓

**Check Condition 2**

The variance of Sₙ'² can be shown to go to 0. For normal data:

Var(Sₙ'²) = [2(n-1)σ⁴]/n² → 0 ✓

**Conclusion**

Sₙ'² is consistent for σ², even though it is biased.

**Lesson**

Bias does not prevent consistency.

**Numerical Illustration**

Suppose σ² = 100.

| n | E(Sₙ'²) | Bias |
|---|----------|------|
| 5 | 80 | -20 |
| 10 | 90 | -10 |
| 50 | 98 | -2 |
| 100 | 99 | -1 |
| 1000 | 99.9 | -0.1 |

The bias shrinks to zero as n grows.

## Example 4: Unbiased but NOT Consistent

**Setup**

Suppose we estimate μ using only the first observation:

Tₙ = X₁

**Is it unbiased?**

E(Tₙ) = E(X₁) = μ ✓

**Is it consistent?**

Var(Tₙ) = Var(X₁) = σ²

This does not depend on n. It does not shrink.

Even if we collect n = 1,000,000 observations, the estimator still uses only the first one.

**Conclusion**

Tₙ = X₁ is unbiased but not consistent.

**Lesson**

Unbiasedness does not guarantee consistency.

An estimator that ignores additional data cannot be consistent.

## Example 5: Another Non-Consistent Estimator

**Setup**

Define: Tₙ = X̄ + 1/n

**Mean**

E(Tₙ) = μ + 1/n

This is biased, but: E(Tₙ) → μ

**Variance**

Var(Tₙ) = Var(X̄) = σ²/n → 0

**Conclusion**

Tₙ is biased for every n, but consistent because:

- bias → 0
- variance → 0

**Numerical Illustration**

If μ = 10, σ² = 4:

| n | E(Tₙ) | Var(Tₙ) | Bias |
|---|-------|----------|------|
| 1 | 11 | 4 | 1 |
| 4 | 10.5 | 1 | 0.5 |
| 100 | 10.1 | 0.04 | 0.1 |
| 10000 | 10.01 | 0.0004 | 0.01 |

## Properties of Consistent Estimators

**Property 1: Invariance**

If Tₙ is consistent for θ and g is a continuous function, then:

g(Tₙ) →ᴾ g(θ)

**Example**

If X̄ →ᴾ μ, then:

- X̄² →ᴾ μ²
- e^(X̄) →ᴾ e^μ
- log(X̄) →ᴾ log(μ) (μ > 0)
- 1/X̄ →ᴾ 1/μ (μ ≠ 0)

**Property 2: Algebra of Consistent Estimators**

If:
- Tₙ →ᴾ α
- Sₙ →ᴾ β

then:

- Sum: Tₙ + Sₙ →ᴾ α + β
- Product: TₙSₙ →ᴾ αβ
- Quotient: Tₙ/Sₙ →ᴾ α/β (β ≠ 0)

**Example**

Suppose:
- X̄ →ᴾ μ
- S² →ᴾ σ²

Then: S²/X̄ →ᴾ σ²/μ (μ ≠ 0)

This is the consistent estimator of the coefficient of variation (squared).

## Law of Large Numbers (LLN)

**Weak Law of Large Numbers (WLLN)**

If X₁, …, Xₙ are i.i.d. with E(Xᵢ) = μ, then:

X̄ →ᴾ μ

This is the theoretical foundation for the consistency of the sample mean.

**Strong Law of Large Numbers (SLLN)**

X̄ →ᵃˢ μ

**Intuition**

If you flip a fair coin many times, the proportion of heads converges to 0.5.

**Numerical Illustration**

Flip a fair coin. The running proportion of heads:

| Flips | Heads | Proportion |
|-------|-------|------------|
| 10 | 6 | 0.60 |
| 100 | 53 | 0.53 |
| 1000 | 502 | 0.502 |
| 10000 | 5012 | 0.5012 |
| 100000 | 49987 | 0.49987 |

The proportion converges to p = 0.5.

## Drawbacks of Asymptotic Theory

**Drawback 1: Unknown Sampling Distribution**

The exact distribution of a consistent estimator may not be known for finite n.

**Drawback 2: Sample-Size Dependent Shape**

The shape of the sampling distribution can change as n grows.

**Drawback 3: Small-Sample Performance**

An estimator that is consistent may still perform poorly for small samples.

**Drawback 4: Multiple Consistent Estimators**

Since consistency is not unique, we need additional criteria (like efficiency or minimum variance) to choose between consistent estimators.

# 5. Consistent Asymptotically Normal (CAN) Estimators

## Definition

An estimator Tₙ is called CAN (Consistent Asymptotically Normal) for θ if:

**Condition 1: Consistency**

Tₙ →ᴾ θ

**Condition 2: Asymptotic Normality**

√n(Tₙ - θ) →ᴰ N(0, σₜ²)

where σₜ² is called the asymptotic variance.

## Why is CAN Important?

If Tₙ is CAN, then for large n:

Tₙ ≈ N(θ, σₜ²/n)

This allows us to:

1. Construct confidence intervals
2. Perform hypothesis tests
3. Compute standard errors

## Example 1: Sample Mean is CAN

By the Central Limit Theorem (CLT):

√n(X̄ - μ) →ᴰ N(0, σ²)

So X̄ is CAN with asymptotic variance σ².

For large n: X̄ ≈ N(μ, σ²/n)

**Numerical Application**

Suppose μ = 100, σ² = 25, n = 64.

Then:

X̄ ≈ N(100, 25/64) = N(100, 0.3906)

SE(X̄) = 5/8 = 0.625

A 95% confidence interval:

X̄ ± 1.96 × 0.625 = X̄ ± 1.225

If X̄ = 101.5: (101.5 - 1.225, 101.5 + 1.225) = (100.275, 102.725)

## Example 2: Sample Proportion is CAN

If X₁, …, Xₙ ~ Bernoulli(p):

√n(p̂ - p) →ᴰ N(0, p(1-p))

So p̂ = X̄ is CAN with asymptotic variance p(1-p).

For large n: p̂ ≈ N(p, p(1-p)/n)

**Numerical Application**

Suppose n = 400 and we observe 240 successes.

p̂ = 240/400 = 0.6

Standard error:

SE(p̂) = √[0.6(0.4)/400] = √0.0006 = 0.0245

95% confidence interval:

0.6 ± 1.96(0.0245) = 0.6 ± 0.048 = (0.552, 0.648)

## Asymptotic Relative Efficiency (ARE)

If Tₙ and Sₙ are both CAN estimators of θ, with asymptotic variances σₜ² and σₛ², then:

ARE(Tₙ, Sₙ) = σₛ²/σₜ²

If ARE > 1, then Tₙ is more efficient.

**Example**

For normal data:
- Asymptotic variance of X̄ is σ²
- Asymptotic variance of median is πσ²/2

ARE(X̄, median) = (πσ²/2)/σ² = π/2 ≈ 1.571

So the mean is about 57% more efficient than the median.

# 6. Maximum Likelihood Estimation (MLE)

## Core Idea

Given observed data, the MLE finds the parameter value that makes the data most probable.

It answers the question: For what parameter value is the observed sample most likely?

## Likelihood Function

If the sample X₁, …, Xₙ is i.i.d. with density (or pmf) f_θ(x):

L(θ) = ∏ᵢ f_θ(Xᵢ)

L(θ) is viewed as a function of θ (not of the data).

## Log-Likelihood

Since the log is a monotonically increasing function:

ℓ(θ) = log L(θ) = ∑ᵢ log f_θ(Xᵢ)

Maximizing L(θ) is equivalent to maximizing ℓ(θ).

The log is easier to work with because:
- Products become sums
- Exponentials simplify

## Step-by-Step MLE Procedure

1. Write the likelihood L(θ)
2. Take the log to get ℓ(θ)
3. Compute the derivative: dℓ/dθ = 0 (score equation)
4. Solve for θ̂
5. Verify that it is a maximum by checking: d²ℓ/dθ²|θ=θ̂ < 0

## Example 1: Bernoulli MLE (Full Derivation)

**Setup**

X₁, …, Xₙ ~ Bernoulli(p)

The pmf is: f(x) = p^x (1-p)^(1-x), x ∈ {0,1}

**Step 1: Likelihood**

L(p) = ∏ᵢ p^Xᵢ (1-p)^(1-Xᵢ)
= p^(∑Xᵢ) (1-p)^(n-∑Xᵢ)

Let k = ∑Xᵢ (number of successes).

L(p) = p^k (1-p)^(n-k)

**Step 2: Log-likelihood**

ℓ(p) = k log p + (n-k) log(1-p)

**Step 3: Differentiate**

dℓ/dp = k/p - (n-k)/(1-p)

**Step 4: Set to zero and solve**

k/p = (n-k)/(1-p)

Cross multiply: k(1-p) = (n-k)p

k - kp = np - kp

k = np

p̂ = k/n = (∑Xᵢ)/n = X̄

**Step 5: Second derivative check**

d²ℓ/dp² = -k/p² - (n-k)/(1-p)²

At p̂ = k/n: = -n²/k - n²/(n-k) < 0 ✓

**Final Answer**

p̂_MLE = X̄

**Numerical Example**

Data: 1, 0, 1, 1, 0, 1, 1, 0, 1, 0

n = 10, k = ∑Xᵢ = 6

p̂ = 6/10 = 0.6

## Example 2: Poisson MLE (Full Derivation)

**Setup**

X₁, …, Xₙ ~ Poisson(μ)

The pmf is: f(x) = e^(-μ) μ^x / x!, x = 0,1,2,…

**Step 1: Likelihood**

L(μ) = ∏ᵢ [e^(-μ) μ^Xᵢ / Xᵢ!] = e^(-nμ) μ^(∑Xᵢ) / ∏Xᵢ!

**Step 2: Log-likelihood**

ℓ(μ) = -nμ + (∑Xᵢ) log μ - ∑log(Xᵢ!)

**Step 3: Differentiate**

dℓ/dμ = -n + (∑Xᵢ)/μ

**Step 4: Solve**

-n + (∑Xᵢ)/μ = 0

μ̂ = (∑Xᵢ)/n = X̄

**Step 5: Check**

d²ℓ/dμ² = -(∑Xᵢ)/μ² < 0 ✓

**Final Answer**

μ̂_MLE = X̄

**Numerical Example**

A store records customer arrivals per hour for 5 hours: 3, 7, 4, 5, 6

X̄ = 25/5 = 5

So μ̂ = 5 arrivals per hour.

## Example 3: Exponential MLE (Full Derivation)

**Setup**

X₁, …, Xₙ ~ Exponential(θ) where θ is the mean

The pdf is: f(x) = (1/θ)e^(-x/θ), x > 0

**Step 1: Likelihood**

L(θ) = ∏ᵢ (1/θ)e^(-Xᵢ/θ) = θ^(-n) exp(-∑Xᵢ/θ)

**Step 2: Log-likelihood**

ℓ(θ) = -n log θ - ∑Xᵢ/θ

**Step 3: Differentiate**

dℓ/dθ = -n/θ + ∑Xᵢ/θ²

**Step 4: Solve**

-n/θ + ∑Xᵢ/θ² = 0

Multiply by θ²: -nθ + ∑Xᵢ = 0

θ̂ = (∑Xᵢ)/n = X̄

**Step 5: Check**

d²ℓ/dθ² = n/θ² - 2∑Xᵢ/θ³

At θ̂ = X̄: = n/X̄² - 2nX̄/X̄³ = n/X̄² - 2n/X̄² = -n/X̄² < 0 ✓

**Final Answer**

θ̂_MLE = X̄

**Numerical Example**

Lifetimes of 5 light bulbs (in hours): 950, 1100, 1050, 900, 1000

X̄ = 5000/5 = 1000

So the estimated mean lifetime is 1000 hours.

## Example 4: Normal MLE (Full Derivation for Both Parameters)

**Setup**

X₁, …, Xₙ ~ N(μ, σ²)

The pdf is: f(x) = (1/√(2πσ²)) exp[-(x-μ)²/(2σ²)]

**Step 1: Likelihood**

L(μ, σ²) = ∏ᵢ (1/√(2πσ²)) exp[-(Xᵢ-μ)²/(2σ²)]
= (2πσ²)^(-n/2) exp[-1/(2σ²)∑(Xᵢ-μ)²]

**Step 2: Log-likelihood**

ℓ(μ, σ²) = -(n/2)log(2π) - (n/2)log(σ²) - 1/(2σ²)∑(Xᵢ-μ)²

**Step 3a: Differentiate with respect to μ**

∂ℓ/∂μ = (1/σ²)∑(Xᵢ-μ)

Set to zero: ∑(Xᵢ-μ) = 0

∑Xᵢ = nμ

μ̂ = X̄

**Step 3b: Differentiate with respect to σ²**

∂ℓ/∂σ² = -n/(2σ²) + 1/(2σ⁴)∑(Xᵢ-μ)²

Set to zero: -n/(2σ²) + ∑(Xᵢ-μ)²/(2σ⁴) = 0

σ̂² = (1/n)∑(Xᵢ-μ̂)² = (1/n)∑(Xᵢ-X̄)²

**Final Answers**

μ̂_MLE = X̄
σ̂²_MLE = (1/n)∑(Xᵢ-X̄)²

**Important Note**

The MLE for σ² uses denominator n and is biased. The unbiased estimator uses denominator n-1:

S² = [1/(n-1)]∑(Xᵢ-X̄)²

**Numerical Example**

Data: 10, 12, 14, 16, 18

X̄ = 70/5 = 14

Deviations squared: (10-14)²=16, (12-14)²=4, (14-14)²=0, (16-14)²=4, (18-14)²=16

Sum = 40

σ̂²_MLE = 40/5 = 8
S² = 40/4 = 10

## Example 5: Uniform(0,θ) MLE (Full Derivation)

**Setup**

X₁, …, Xₙ ~ U(0,θ)

The pdf is: f(x) = 1/θ, 0 < x < θ

**Step 1: Likelihood**

The likelihood is nonzero only if all observations satisfy Xᵢ ≤ θ:

L(θ) = { θ^(-n) if θ ≥ X_(n) = max(X₁,…,Xₙ)
       { 0 otherwise

**Step 2: Maximize**

Since θ^(-n) is a decreasing function of θ, the maximum occurs at the smallest allowable value of θ.

The constraint is θ ≥ X_(n).

So: θ̂_MLE = X_(n)

**Note**

This MLE cannot be found by setting a derivative to zero. It is a boundary maximum.

**Numerical Example**

Data: 2.3, 5.1, 7.8, 4.6, 6.2

X_(n) = max = 7.8

So: θ̂ = 7.8

**Is this unbiased?**

No. We can show: E(X_(n)) = [n/(n+1)]θ

So: Bias = [n/(n+1)]θ - θ = -θ/(n+1)

The MLE underestimates θ on average. But as n→∞: E(X_(n)) → θ, so it is asymptotically unbiased and consistent.

## Example 6: Gamma MLE (with known shape)

**Setup**

X₁, …, Xₙ ~ Gamma(α,θ) with known shape α and unknown scale θ.

The pdf is: f(x) = [1/(Γ(α)θ^α)] x^(α-1) e^(-x/θ)

**Log-likelihood**

ℓ(θ) = -nα log θ + (α-1)∑log Xᵢ - ∑Xᵢ/θ - n log Γ(α)

**Differentiate**

dℓ/dθ = -nα/θ + ∑Xᵢ/θ²

**Set to zero**

-nα/θ + ∑Xᵢ/θ² = 0

θ̂ = (∑Xᵢ)/(nα) = X̄/α

**Numerical Example**

If α = 3 and data are: 6, 9, 12, 15, 18

X̄ = 12

θ̂ = 12/3 = 4

## Example 7: Binomial MLE

**Setup**

X ~ Binomial(N,p) where N is known and p is unknown.

**Result**

p̂ = X/N

or equivalently from n observations: p̂ = X̄/N

**Numerical Example**

In 20 trials (N=20), we observe 8 successes.

p̂ = 8/20 = 0.4

## Properties of MLE

**Property 1: Invariance**

If θ̂ is the MLE of θ and g is any function, then:

g(θ̂) is the MLE of g(θ)

**Example**

If p̂ = 0.6 is the MLE of p, then:

MLE of p(1-p) = 0.6(0.4) = 0.24

**Property 2: Consistency**

Under regularity conditions, the MLE is consistent.

**Property 3: Asymptotic Normality**

Under regularity conditions:

√n(θ̂ - θ) →ᴰ N(0, 1/I(θ))

where I(θ) is the Fisher information.

**Property 4: Asymptotic Efficiency**

The MLE achieves the Cramer-Rao lower bound asymptotically.

## Fisher Information

The Fisher information for one observation is:

I(θ) = E[-d²log f_θ(X)/dθ²]

**Example: Bernoulli**

log f(x) = x log p + (1-x) log(1-p)

d²log f/dp² = -x/p² - (1-x)/(1-p)²

I(p) = E[X/p² + (1-X)/(1-p)²] = 1/p + 1/(1-p) = 1/[p(1-p)]

# 7. Method of Moments (MoM)

## Core Idea

The Method of Moments says: Sample moments should approximate population moments.

If sample moments ≈ population moments, then we can solve for unknown parameters.

## Population Moments

The j-th population moment is:

α_j(θ) = E(X^j)

- First moment: α₁ = E(X) = μ
- Second moment: α₂ = E(X²) = Var(X) + [E(X)]² = σ² + μ²
- Third moment: α₃ = E(X³)

## Sample Moments

The j-th sample moment is:

α̂_j = (1/n)∑Xᵢ^j

- First sample moment: α̂₁ = (1/n)∑Xᵢ = X̄
- Second sample moment: α̂₂ = (1/n)∑Xᵢ²

## General Procedure

Suppose the model has k unknown parameters θ₁, …, θₖ.

**Step 1**

Find the first k population moments as functions of θ₁, …, θₖ:

α_j(θ₁,…,θₖ) = E(X^j), j=1,…,k

**Step 2**

Compute the first k sample moments:

α̂_j = (1/n)∑Xᵢ^j

**Step 3**

Set population moments equal to sample moments:

α_j(θ̂₁,…,θ̂ₖ) = α̂_j

**Step 4**

Solve the k equations for θ̂₁, …, θ̂ₖ.

## Example 1: MoM for Bernoulli (Full Derivation)

**Setup**

X ~ Bernoulli(p)

One unknown parameter: p

**Step 1: Population moment**

α₁ = E(X) = p

**Step 2: Sample moment**

α̂₁ = X̄

**Step 3: Set equal**

p = X̄

**Step 4: Solve**

p̂_MoM = X̄

**Numerical Example**

Data: 1, 0, 1, 1, 0, 1, 0, 0, 1, 1

X̄ = 6/10 = 0.6

p̂_MoM = 0.6

## Example 2: MoM for Exponential (Full Derivation)

**Setup**

X ~ Exponential(λ) with E(X) = 1/λ

One unknown parameter: λ

**Step 1: Population moment**

α₁ = E(X) = 1/λ

**Step 2: Sample moment**

α̂₁ = X̄

**Step 3: Set equal**

1/λ = X̄

**Step 4: Solve**

λ̂_MoM = 1/X̄

**Numerical Example**

Waiting times (in minutes): 3, 5, 2, 4, 6

X̄ = 20/5 = 4

λ̂_MoM = 1/4 = 0.25

Interpretation: events arrive at rate 0.25 per minute (one every 4 minutes).

## Example 3: MoM for Poisson (Full Derivation)

**Setup**

X ~ Poisson(μ)

**Step 1**

α₁ = E(X) = μ

**Step 2**

α̂₁ = X̄

**Step 3**

μ = X̄

**Result**

μ̂_MoM = X̄

**Numerical Example**

Number of emails per hour: 12, 8, 15, 10, 5

X̄ = 50/5 = 10

μ̂_MoM = 10

## Example 4: MoM for Normal (Two Parameters — Full Derivation)

**Setup**

X ~ N(μ, σ²)

Two unknown parameters: μ and σ²

**Step 1: Population moments**

First moment: α₁ = E(X) = μ
Second moment: α₂ = E(X²) = Var(X) + [E(X)]² = σ² + μ²

**Step 2: Sample moments**

α̂₁ = X̄
α̂₂ = (1/n)∑Xᵢ²

**Step 3: Set equal**

μ = X̄
σ² + μ² = (1/n)∑Xᵢ²

**Step 4: Solve**

From the first equation: μ̂ = X̄

Substitute into the second: σ̂² = (1/n)∑Xᵢ² - X̄²

This can be rewritten as: σ̂² = (1/n)∑(Xᵢ-X̄)²

**Proof that both forms are equal**

(1/n)∑(Xᵢ-X̄)² = (1/n)∑(Xᵢ² - 2XᵢX̄ + X̄²)
= (1/n)∑Xᵢ² - 2X̄(1/n)∑Xᵢ + X̄²
= (1/n)∑Xᵢ² - 2X̄² + X̄²
= (1/n)∑Xᵢ² - X̄²

**Final Answers**

μ̂_MoM = X̄
σ̂²_MoM = (1/n)∑(Xᵢ-X̄)²

**Numerical Example**

Data: 3, 5, 7, 9, 11

X̄ = 35/5 = 7

(1/5)∑Xᵢ² = (9+25+49+81+121)/5 = 285/5 = 57

σ̂² = 57 - 49 = 8

So: μ̂ = 7, σ̂² = 8

## Example 5: MoM for Uniform(a,b) (Two Parameters)

**Setup**

X ~ U(a,b)

Two unknown parameters: a and b

**Step 1: Population moments**

E(X) = (a+b)/2
E(X²) = Var(X) + [E(X)]² = (b-a)²/12 + (a+b)²/4

**Step 2: Sample moments**

α̂₁ = X̄
α̂₂ = (1/n)∑Xᵢ²

**Step 3: Set equal**

(a+b)/2 = X̄
(b-a)²/12 + (a+b)²/4 = (1/n)∑Xᵢ²

**Step 4: Solve**

From the first equation: a+b = 2X̄

Let S_MoM² = (1/n)∑(Xᵢ-X̄)²

Then (b-a)²/12 = S_MoM², so:

b-a = 2√(3S_MoM²)

Solve:

â = X̄ - √(3S_MoM²)
b̂ = X̄ + √(3S_MoM²)

**Numerical Example**

Data: 2, 4, 6, 8, 10

X̄ = 6
S_MoM² = (16+4+0+4+16)/5 = 40/5 = 8

â = 6 - √24 = 6 - 4.899 = 1.101
b̂ = 6 + √24 = 6 + 4.899 = 10.899

## Example 6: Two-Parameter MoM with Frequency Data

**Setup**

75 observations take values:

| Value | Frequency |
|-------|-----------|
| 0 | 27 |
| 1 | 38 |
| 2 | 10 |

Total n = 27+38+10 = 75

**First sample moment**

α̂₁ = [0(27) + 1(38) + 2(10)]/75 = (0+38+20)/75 = 58/75 ≈ 0.7733

**Second sample moment**

α̂₂ = [0²(27) + 1²(38) + 2²(10)]/75 = (0+38+40)/75 = 78/75 = 1.04

**Sample variance**

σ̂² = α̂₂ - α̂₁² = 1.04 - 0.5980 = 0.4420

**Set up moment equations**

If the theoretical model gives:

E(X) = g₁(θ,α)
E(X²) = g₂(θ,α)

then solve the system:

g₁(θ̂,α̂) = 0.7733
g₂(θ̂,α̂) = 1.04

**Main Point**

For a model with k parameters, we need k moment equations.

# 8. Comparison of All Concepts

## Unbiasedness vs Consistency

| Property | Unbiasedness | Consistency |
|----------|--------------|-------------|
| Type | Finite-sample property | Asymptotic property |
| Definition | E(T) = θ | Tₙ →ᴾ θ |
| Sample size | Holds for each n | Requires n → ∞ |
| One implies other? | No | No |

## Critical Examples

| Estimator | Unbiased? | Consistent? |
|-----------|-----------|-------------|
| X̄ for μ | Yes | Yes |
| X₁ for μ | Yes | No |
| (1/n)∑(Xᵢ-X̄)² for σ² | No | Yes |
| [1/(n-1)]∑(Xᵢ-X̄)² for σ² | Yes | Yes |

## MLE vs Method of Moments

| Feature | MLE | Method of Moments |
|---------|-----|-------------------|
| Approach | Maximize likelihood | Match moments |
| Requires | Full distribution specification | Only first k moments |
| Efficiency | Asymptotically optimal | Often less efficient |
| Computation | May require numerical methods | Usually algebraic |
| Always unbiased? | Not necessarily | Not necessarily |
| Always consistent? | Yes (under conditions) | Yes (under conditions) |

## When MLE = MoM

For many common distributions, the two methods give the same estimator:

- Bernoulli: p̂ = X̄ (both)
- Poisson: μ̂ = X̄ (both)
- Exponential: θ̂ = X̄ (both)

# 9. Complete Summary Tables

## Summary of Estimator Properties

| Estimator | Parameter | Unbiased? | Consistent? | CAN? | Variance Formula |
|-----------|-----------|-----------|-------------|------|-----------------|
| X̄ | μ | Yes | Yes | Yes | σ²/n |
| p̂ = X̄ | p | Yes | Yes | Yes | p(1-p)/n |
| S² | σ² | Yes | Yes | Yes* | 2σ⁴/(n-1)* |
| S'² | σ² | No | Yes | Yes* | 2σ⁴(n-1)/n²* |
| Mₙ (median) | μ | Yes** | Yes | Yes | πσ²/(2n)** |
| X_(n) | θ (Uniform) | No | Yes | No | - |

*For normal data
**For symmetric distributions

## Common Distributions and Their Estimators

| Distribution | Parameter(s) | MLE | MoM | Unbiased Estimator |
|-------------|--------------|-----|-----|-------------------|
| Bernoulli(p) | p | X̄ | X̄ | X̄ |
| Poisson(μ) | μ | X̄ | X̄ | X̄ |
| Exponential(λ) | λ (mean = 1/λ) | X̄ | 1/X̄ | X̄ |
| Exponential(θ) | θ (mean = θ) | X̄ | X̄ | X̄ |
| N(μ,σ²) | μ, σ² | μ̂=X̄, σ̂²=(1/n)∑(Xᵢ-X̄)² | μ̂=X̄, σ̂²=(1/n)∑(Xᵢ-X̄)² | μ̂=X̄, S²=[1/(n-1)]∑(Xᵢ-X̄)² |
| Uniform(0,θ) | θ | X_(n) | 2X̄ | [(n+1)/n]X_(n) |
| Uniform(a,b) | a, b | â=min(Xᵢ), b̂=max(Xᵢ) | â=X̄-√3S, b̂=X̄+√3S | - |
| Gamma(α,θ) (α known) | θ | X̄/α | X̄/α | X̄/α |
| Binomial(N,p) | p | X/N | X/N | X/N |

## Important Formulas

1. **Bias**: Bias(T) = E(T) - θ
2. **Mean Squared Error**: MSE(T) = E[(T-θ)²] = Var(T) + [Bias(T)]²
3. **Consistency conditions**: E(Tₙ) → θ and Var(Tₙ) → 0
4. **Asymptotic normality**: √n(Tₙ - θ) →ᴰ N(0, σ²)
5. **Fisher information**: I(θ) = E[-d²log f_θ(X)/dθ²]
6. **Cramer-Rao lower bound**: Var(T) ≥ 1/[nI(θ)] for unbiased T
7. **Method of moments**: α_j(θ) = E(X^j) = (1/n)∑Xᵢ^j
8. **MLE equations**: dℓ/dθ = 0 or ∂ℓ/∂θ_j = 0 for multiple parameters

---

**Key Takeaways:**

1. **Unbiasedness** is a finite-sample property; an unbiased estimator gives the correct value on average.
2. **Consistency** is an asymptotic property; a consistent estimator converges to the true value as sample size increases.
3. **CAN estimators** are both consistent and asymptotically normal, enabling inference.
4. **MLE** maximizes the likelihood function and has optimal asymptotic properties.
5. **Method of Moments** matches sample moments to population moments.
6. Different estimators can have different properties; choose based on your needs (unbiasedness, efficiency, robustness).

These concepts form the foundation of statistical inference and are essential for understanding how we learn from data.

