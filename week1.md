# Complete Statistics Reference
## Statistical Framework, Discrete and Continuous Distributions, and Regression

---

# Table of Contents

1. [Statistical Framework](#statistical-framework)
   - [Population vs Sample](#population-vs-sample)
   - [Mean, Median, Mode, Variance](#mean-median-mode-variance)
   - [Probability Framework](#probability-framework)
   - [Expectation, Variance, MGF](#expectation-variance-mgf)
2. [Discrete Distributions](#discrete-distributions)
   - Discrete Uniform
   - Binomial
   - Poisson
   - Geometric
   - Negative Binomial
   - Hypergeometric
3. [Continuous Distributions](#continuous-distributions)
   - Continuous Uniform
   - Exponential
   - Normal
   - Gamma
   - Chi-Square
   - F Distribution
   - Beta
   - Log-Normal
   - Cauchy
   - Pareto
   - Weibull
4. [Regression](#regression)
   - Least Squares Derivation
   - Hessian Verification
   - Worked Example
   - Coin Toss Inference
5. [Summary Tables](#summary-tables)

---

# Statistical Framework

## Population vs Sample

### Population
A **population** is the complete set of all observations or individuals we are interested in.

- Population size: `N`
- Population mean: `μ`
- Population variance: `σ²`

### Sample
A **sample** is a subset of the population used to estimate population quantities.

- Sample size: `n`
- Sample mean: `x̄`
- Sample variance: `s²`

### Example
A school has 5,000 students.  
That is the **population**.

If we select 100 students and measure their heights, those 100 students form a **sample**.

---

## Mean, Median, Mode, Variance

## Mean

### Population Mean
$$
\mu = \frac{1}{N}\sum_{i=1}^{N}x_i
$$

### Sample Mean
$$
\bar{x} = \frac{1}{n}\sum_{i=1}^{n}x_i
$$

### Derivation of Mean
The mean minimizes the sum of squared deviations:

$$
f(c) = \sum_{i=1}^{n}(x_i-c)^2
$$

Differentiate:

$$
\frac{d}{dc}f(c) = -2\sum_{i=1}^{n}(x_i-c)
$$

Set equal to zero:

$$
\sum_{i=1}^{n}x_i - nc = 0
$$

$$
c = \frac{1}{n}\sum_{i=1}^{n}x_i = \bar{x}
$$

### Example
Data: `2, 4, 6, 8, 10`

$$
\bar{x} = \frac{2+4+6+8+10}{5} = 6
$$

---

## Median

The median is the middle value in sorted data.

- If `n` is odd: median is the middle value
- If `n` is even: median is the average of the two middle values

### Example 1
Data: `1, 3, 5, 7, 9`

Median = `5`

### Example 2
Data: `1, 2, 3, 5, 7, 9`

$$
\text{Median} = \frac{3+5}{2} = 4
$$

---

## Mode

The mode is the most frequently occurring value.

### Example
Data: `2, 3, 3, 5, 7, 7, 7, 9`

Mode = `7`

---

## Variance

### Population Variance
$$
\sigma^2 = \frac{1}{N}\sum_{i=1}^{N}(x_i-\mu)^2
$$

### Sample Variance
$$
s^2 = \frac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar{x})^2
$$

### Standard Deviation
$$
\sigma = \sqrt{\sigma^2}, \qquad s = \sqrt{s^2}
$$

### Example
Data: `2, 4, 6, 8, 10`

Mean:
$$
\bar{x} = 6
$$

Squared deviations:
$$
(2-6)^2 = 16,\quad (4-6)^2 = 4,\quad (6-6)^2 = 0,\quad (8-6)^2 = 4,\quad (10-6)^2 = 16
$$

Sum:
$$
16+4+0+4+16 = 40
$$

Sample variance:
$$
s^2 = \frac{40}{5-1} = 10
$$

Sample standard deviation:
$$
s = \sqrt{10} \approx 3.162
$$

---

## Probability Framework

### Axioms of Probability

1. $$
P(A) \ge 0
$$

2. $$
P(S) = 1
$$

3. If \(A \cap B = \emptyset\), then:

$$
P(A \cup B) = P(A) + P(B)
$$

### Important Rules

#### Complement Rule
$$
P(A^c) = 1 - P(A)
$$

#### Addition Rule
$$
P(A \cup B) = P(A) + P(B) - P(A \cap B)
$$

#### Conditional Probability
$$
P(A|B) = \frac{P(A \cap B)}{P(B)}
$$

#### Multiplication Rule
$$
P(A \cap B) = P(A|B)P(B)
$$

#### Independence
$$
P(A \cap B) = P(A)P(B)
$$

#### Bayes' Theorem
$$
P(A|B) = \frac{P(B|A)P(A)}{P(B)}
$$

### Example: Medical Test

Suppose:

- Disease prevalence: `P(D)=0.01`
- Test sensitivity: `P(+|D)=0.99`
- False positive rate: `P(+|D^c)=0.05`

Then:

$$
P(+) = P(+|D)P(D) + P(+|D^c)P(D^c)
$$

$$
P(+) = 0.99(0.01) + 0.05(0.99) = 0.0594
$$

Using Bayes:

$$
P(D|+) = \frac{0.99(0.01)}{0.0594} \approx 0.1667
$$

So a positive test does **not** mean 99% chance of disease.

---

## Expectation, Variance, MGF

### Discrete Expected Value
$$
E[X] = \sum_x xP(X=x)
$$

### Continuous Expected Value
$$
E[X] = \int_{-\infty}^{\infty}xf(x)\,dx
$$

### Variance
$$
Var(X) = E[(X-\mu)^2] = E[X^2] - (E[X])^2
$$

### Moment Generating Function
$$
M_X(t) = E[e^{tX}]
$$

### Properties
$$
E[X] = M'_X(0)
$$

$$
E[X^2] = M''_X(0)
$$

$$
Var(X) = M''_X(0) - (M'_X(0))^2
$$

---

# Discrete Distributions

## 1. Discrete Uniform Distribution

If \(X\in\{1,2,\dots,N\}\) with equal probability:

### PMF
$$
P(X=k)=\frac{1}{N}, \qquad k=1,2,\dots,N
$$

### Mean
$$
E[X]=\frac{N+1}{2}
$$

### Variance
$$
Var(X)=\frac{N^2-1}{12}
$$

### MGF
$$
M_X(t)=\frac{1}{N}\sum_{k=1}^{N}e^{tk}
$$

### Example
For a fair die, \(N=6\):

$$
P(X=k)=\frac{1}{6}
$$

$$
E[X]=\frac{6+1}{2}=3.5
$$

$$
Var(X)=\frac{6^2-1}{12}=\frac{35}{12}
$$

$$
P(X \le 3)=\frac{3}{6}=0.5
$$

---

## 2. Binomial Distribution

Counts the number of successes in `n` independent trials.

### PMF
$$
P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}, \qquad k=0,1,\dots,n
$$

### Mean
$$
E[X]=np
$$

### Variance
$$
Var(X)=np(1-p)
$$

### MGF
$$
M_X(t)=(pe^t+1-p)^n
$$

### Example
A factory has 10% defective rate. In 20 items:

$$
X \sim Binomial(20, 0.1)
$$

#### Probability of exactly 3 defectives
$$
P(X=3)=\binom{20}{3}(0.1)^3(0.9)^{17}
$$

$$
=1140(0.001)(0.1668)\approx 0.1901
$$

#### Mean
$$
E[X]=20(0.1)=2
$$

#### Variance
$$
Var(X)=20(0.1)(0.9)=1.8
$$

---

## 3. Poisson Distribution

Models event counts over a fixed interval.

### PMF
$$
P(X=k)=\frac{e^{-\lambda}\lambda^k}{k!}, \qquad k=0,1,2,\dots
$$

### Mean
$$
E[X]=\lambda
$$

### Variance
$$
Var(X)=\lambda
$$

### MGF
$$
M_X(t)=e^{\lambda(e^t-1)}
$$

### Example
If calls arrive at rate \(\lambda=4\) per minute:

#### Exactly 6 calls
$$
P(X=6)=\frac{e^{-4}4^6}{6!}\approx 0.1042
$$

#### No calls
$$
P(X=0)=e^{-4}\approx 0.0183
$$

---

## 4. Geometric Distribution

Number of trials until first success.

### PMF
$$
P(X=k)=(1-p)^{k-1}p, \qquad k=1,2,\dots
$$

### Mean
$$
E[X]=\frac{1}{p}
$$

### Variance
$$
Var(X)=\frac{1-p}{p^2}
$$

### MGF
$$
M_X(t)=\frac{pe^t}{1-(1-p)e^t}
$$

### Example
A player makes a shot with probability \(p=0.8\).

Probability first success occurs on 3rd trial:

$$
P(X=3)=(0.2)^2(0.8)=0.032
$$

Expected number of trials:

$$
E[X]=\frac{1}{0.8}=1.25
$$

---

## 5. Negative Binomial Distribution

Number of trials until the \(r\)-th success.

### PMF
$$
P(X=k)=\binom{k-1}{r-1}p^r(1-p)^{k-r}, \qquad k=r,r+1,\dots
$$

### Mean
$$
E[X]=\frac{r}{p}
$$

### Variance
$$
Var(X)=\frac{r(1-p)}{p^2}
$$

### MGF
$$
M_X(t)=\left(\frac{pe^t}{1-(1-p)e^t}\right)^r
$$

### Example
A salesperson closes a deal with \(p=0.3\). Need \(r=5\) deals.

$$
E[X]=\frac{5}{0.3}=16.67
$$

$$
Var(X)=\frac{5(0.7)}{0.09}=38.89
$$

#### Probability that 5th success occurs on 10th call
$$
P(X=10)=\binom{9}{4}(0.3)^5(0.7)^5
$$

$$
=126(0.00243)(0.16807)\approx 0.0515
$$

---

## 6. Hypergeometric Distribution

Sampling without replacement.

### PMF
$$
P(X=k)=\frac{\binom{K}{k}\binom{N-K}{n-k}}{\binom{N}{n}}
$$

### Mean
$$
E[X]=n\frac{K}{N}
$$

### Variance
$$
Var(X)=n\frac{K}{N}\frac{N-K}{N}\frac{N-n}{N-1}
$$

### Example
Draw 5 cards from a deck of 52 cards, where 13 are hearts.

#### Exactly 2 hearts
$$
P(X=2)=\frac{\binom{13}{2}\binom{39}{3}}{\binom{52}{5}}
\approx 0.2743
$$

#### Mean
$$
E[X]=5\cdot\frac{13}{52}=1.25
$$

---

# Continuous Distributions

## 1. Continuous Uniform Distribution

### PDF
$$
f(x)=\frac{1}{b-a}, \qquad a\le x\le b
$$

### Mean
$$
E[X]=\frac{a+b}{2}
$$

### Variance
$$
Var(X)=\frac{(b-a)^2}{12}
$$

### MGF
$$
M_X(t)=\frac{e^{tb}-e^{ta}}{t(b-a)}
$$

### Example
If \(X\sim U(0,1)\),

$$
P(0.2<X<0.7)=0.5
$$

$$
E[X]=0.5
$$

$$
Var(X)=\frac{1}{12}
$$

---

## 2. Exponential Distribution

### PDF
$$
f(x)=\lambda e^{-\lambda x}, \qquad x\ge 0
$$

### CDF
$$
F(x)=1-e^{-\lambda x}
$$

### Mean
$$
E[X]=\frac{1}{\lambda}
$$

### Variance
$$
Var(X)=\frac{1}{\lambda^2}
$$

### MGF
$$
M_X(t)=\frac{\lambda}{\lambda-t}, \qquad t<\lambda
$$

### Example
A bulb lifetime has mean 1000 hours, so \(\lambda=0.001\).

#### Probability lifetime exceeds 1500
$$
P(X>1500)=e^{-0.001(1500)}=e^{-1.5}\approx 0.2231
$$

---

## 3. Normal Distribution

### PDF
$$
f(x)=\frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$

### Mean
$$
E[X]=\mu
$$

### Variance
$$
Var(X)=\sigma^2
$$

### MGF
$$
M_X(t)=\exp\left(\mu t+\frac{\sigma^2 t^2}{2}\right)
$$

### Standardization
$$
Z=\frac{X-\mu}{\sigma}
$$

### Example
Exam scores: \(\mu=1060,\ \sigma=195\)

#### Probability score above 1300
$$
z=\frac{1300-1060}{195}=1.23
$$

$$
P(X>1300)=P(Z>1.23)\approx 0.1093
$$

---

## 4. Gamma Distribution

### PDF
$$
f(x)=\frac{\lambda^\alpha}{\Gamma(\alpha)}x^{\alpha-1}e^{-\lambda x}, \qquad x>0
$$

### Mean
$$
E[X]=\frac{\alpha}{\lambda}
$$

### Variance
$$
Var(X)=\frac{\alpha}{\lambda^2}
$$

### MGF
$$
M_X(t)=\left(\frac{\lambda}{\lambda-t}\right)^\alpha
$$

### Example
If \(\alpha=3,\ \lambda=0.5\),

$$
E[X]=\frac{3}{0.5}=6
$$

$$
Var(X)=\frac{3}{0.25}=12
$$

---

## 5. Chi-Square Distribution

If \(Z_1,\dots,Z_k\sim N(0,1)\), then

$$
X=\sum_{i=1}^{k}Z_i^2 \sim \chi^2(k)
$$

### PDF
$$
f(x)=\frac{1}{2^{k/2}\Gamma(k/2)}x^{k/2-1}e^{-x/2}, \qquad x>0
$$

### Mean
$$
E[X]=k
$$

### Variance
$$
Var(X)=2k
$$

### MGF
$$
M_X(t)=(1-2t)^{-k/2}
$$

### Example
For \(k=5\),

$$
E[X]=5,\qquad Var(X)=10
$$

Used in variance tests and goodness-of-fit tests.

---

## 6. F Distribution

If

$$
U\sim \chi^2(d_1), \qquad V\sim \chi^2(d_2)
$$

independently, then

$$
F=\frac{U/d_1}{V/d_2}\sim F(d_1,d_2)
$$

### Mean
$$
E[X]=\frac{d_2}{d_2-2}, \qquad d_2>2
$$

### Variance
$$
Var(X)=\frac{2d_2^2(d_1+d_2-2)}{d_1(d_2-2)^2(d_2-4)}, \qquad d_2>4
$$

### Example
If sample variances are:

- \(s_1^2=25\)
- \(s_2^2=15\)

then

$$
F=\frac{25}{15}=1.667
$$

Used to compare two variances and in ANOVA.

---

## 7. Beta Distribution

### PDF
$$
f(x)=\frac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha,\beta)}, \qquad 0<x<1
$$

### Mean
$$
E[X]=\frac{\alpha}{\alpha+\beta}
$$

### Variance
$$
Var(X)=\frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}
$$

### Example
If \(X\sim Beta(4,8)\),

$$
E[X]=\frac{4}{12}=\frac{1}{3}
$$

$$
Var(X)=\frac{4\cdot8}{12^2\cdot13}=\frac{32}{1872}\approx 0.0171
$$

Used in Bayesian statistics for probabilities.

---

## 8. Log-Normal Distribution

If

$$
\ln(X)\sim N(\mu,\sigma^2)
$$

then \(X\) is log-normal.

### PDF
$$
f(x)=\frac{1}{x\sigma\sqrt{2\pi}}e^{-\frac{(\ln x-\mu)^2}{2\sigma^2}}, \qquad x>0
$$

### Mean
$$
E[X]=e^{\mu+\sigma^2/2}
$$

### Variance
$$
Var(X)=e^{2\mu+\sigma^2}(e^{\sigma^2}-1)
$$

### Example
If \(\mu=0.05,\ \sigma^2=0.04\),

$$
E[X]=e^{0.05+0.02}=e^{0.07}\approx 1.0725
$$

If starting price is 100:

$$
E[\text{Price}] = 100(1.0725)=107.25
$$

---

## 9. Cauchy Distribution

### PDF
$$
f(x)=\frac{1}{\pi\gamma\left[1+\left(\frac{x-x_0}{\gamma}\right)^2\right]}
$$

### Important Properties
- Mean does not exist
- Variance does not exist
- MGF does not exist

### Example
Standard Cauchy:

$$
f(x)=\frac{1}{\pi(1+x^2)}
$$

Used in resonance physics and extreme heavy-tail modeling.

---

## 10. Pareto Distribution

### PDF
$$
f(x)=\frac{\alpha x_m^\alpha}{x^{\alpha+1}}, \qquad x\ge x_m
$$

### Mean
$$
E[X]=\frac{\alpha x_m}{\alpha-1}, \qquad \alpha>1
$$

### Variance
$$
Var(X)=\frac{x_m^2\alpha}{(\alpha-1)^2(\alpha-2)}, \qquad \alpha>2
$$

### Example
If \(x_m=30000,\ \alpha=2.5\),

$$
E[X]=\frac{2.5(30000)}{1.5}=50000
$$

#### Probability income above 100000
$$
P(X>100000)=\left(\frac{30000}{100000}\right)^{2.5}\approx 0.0493
$$

---

## 11. Weibull Distribution

### PDF
$$
f(x)=\frac{k}{\lambda}\left(\frac{x}{\lambda}\right)^{k-1}e^{-(x/\lambda)^k}, \qquad x\ge0
$$

### Mean
$$
E[X]=\lambda\Gamma\left(1+\frac{1}{k}\right)
$$

### Variance
$$
Var(X)=\lambda^2\left[\Gamma\left(1+\frac{2}{k}\right)-\Gamma^2\left(1+\frac{1}{k}\right)\right]
$$

### Example
If \(k=2,\ \lambda=5000\),

$$
E[X]=5000\Gamma(1.5)\approx 4431
$$

#### Probability survives beyond 3000
$$
P(X>3000)=e^{-(3000/5000)^2}=e^{-0.36}\approx 0.6977
$$

---

# Regression

## Simple Linear Regression Model

$$
y = \beta_0 + \beta_1 x + \varepsilon
$$

We minimize:

$$
S(\beta_0,\beta_1)=\sum_{i=1}^{n}(y_i-\beta_0-\beta_1x_i)^2
$$

---

## Least Squares Derivation

### Differentiate with respect to \(\beta_0\)

$$
\frac{\partial S}{\partial \beta_0}=-2\sum_{i=1}^{n}(y_i-\beta_0-\beta_1x_i)=0
$$

$$
\sum y_i - n\beta_0 - \beta_1\sum x_i = 0
$$

$$
\hat{\beta}_0 = \bar{y}-\hat{\beta}_1\bar{x}
$$

### Differentiate with respect to \(\beta_1\)

$$
\frac{\partial S}{\partial \beta_1}=-2\sum_{i=1}^{n}x_i(y_i-\beta_0-\beta_1x_i)=0
$$

Solving gives:

$$
\hat{\beta}_1=\frac{\sum x_i y_i - n\bar{x}\bar{y}}{\sum x_i^2 - n\bar{x}^2}
$$

Equivalent form:

$$
\hat{\beta}_1 = \frac{S_{xy}}{S_{xx}}
$$

where

$$
S_{xy}=\sum (x_i-\bar{x})(y_i-\bar{y})
$$

$$
S_{xx}=\sum (x_i-\bar{x})^2
$$

---

## Hessian Verification

The Hessian is:

$$
H=
2\begin{pmatrix}
n & \sum x_i \\
\sum x_i & \sum x_i^2
\end{pmatrix}
$$

For a minimum:
- \(2n > 0\)
- determinant \(>0\)

$$
\det(H)=4\left(n\sum x_i^2-(\sum x_i)^2\right)>0
$$

So the least squares estimates produce a minimum.

---

## Worked Example: \(y=-x+6\)

Data points:

- \((1,5)\)
- \((2,4)\)
- \((3,3)\)
- \((4,2)\)
- \((5,1)\)

### Compute averages
$$
\sum x_i=15,\quad \sum y_i=15
$$

$$
\bar{x}=3,\quad \bar{y}=3
$$

### Compute sums
$$
\sum x_i^2=55
$$

$$
\sum x_i y_i=35
$$

### Compute slope
$$
S_{xy}=35-5(3)(3)=-10
$$

$$
S_{xx}=55-5(9)=10
$$

$$
\hat{\beta}_1=\frac{-10}{10}=-1
$$

### Compute intercept
$$
\hat{\beta}_0=3-(-1)(3)=6
$$

### Regression line
$$
\hat{y}=-x+6
$$

Residuals are all 0, so this is a perfect fit.

---

## Coin Toss Inference Example

Suppose 100 tosses produce 62 heads.

Let \(Y_i=1\) for head, \(0\) for tail.

Then:

$$
\hat{p}=\frac{62}{100}=0.62
$$

### Likelihood
$$
L(p)=p^{62}(1-p)^{38}
$$

### Log-likelihood
$$
\ell(p)=62\ln p + 38\ln(1-p)
$$

Differentiate:
$$
\frac{d\ell}{dp}=\frac{62}{p}-\frac{38}{1-p}=0
$$

This gives:
$$
\hat{p}=0.62
$$

### Standard error
$$
SE(\hat{p})=\sqrt{\frac{0.62(0.38)}{100}}\approx 0.0486
$$

### 95% Confidence Interval
$$
0.62 \pm 1.96(0.0486)
$$

$$
0.62 \pm 0.0952
$$

$$
(0.5248, 0.7152)
$$

### Hypothesis Test
Test:

- \(H_0: p=0.5\)
- \(H_1: p\ne 0.5\)

$$
z=\frac{0.62-0.5}{\sqrt{0.25/100}}=\frac{0.12}{0.05}=2.4
$$

p-value \(\approx 0.0164\)

Since \(0.0164<0.05\), reject \(H_0\).

---

# Summary Tables

## Discrete Distributions Summary

| Distribution | PMF | Mean | Variance | MGF |
|---|---|---|---|---|
| Discrete Uniform | \(P(X=k)=1/N\) | \((N+1)/2\) | \((N^2-1)/12\) | \(\frac{1}{N}\sum e^{tk}\) |
| Binomial | \(\binom{n}{k}p^k(1-p)^{n-k}\) | \(np\) | \(np(1-p)\) | \((pe^t+1-p)^n\) |
| Poisson | \(\frac{e^{-\lambda}\lambda^k}{k!}\) | \(\lambda\) | \(\lambda\) | \(e^{\lambda(e^t-1)}\) |
| Geometric | \((1-p)^{k-1}p\) | \(1/p\) | \((1-p)/p^2\) | \(\frac{pe^t}{1-(1-p)e^t}\) |
| Negative Binomial | \(\binom{k-1}{r-1}p^r(1-p)^{k-r}\) | \(r/p\) | \(r(1-p)/p^2\) | \(\left(\frac{pe^t}{1-(1-p)e^t}\right)^r\) |
| Hypergeometric | \(\frac{\binom{K}{k}\binom{N-K}{n-k}}{\binom{N}{n}}\) | \(nK/N\) | \(n\frac{K}{N}\frac{N-K}{N}\frac{N-n}{N-1}\) | No simple closed form |

---

## Continuous Distributions Summary

| Distribution | PDF | Mean | Variance |
|---|---|---|---|
| Uniform \((a,b)\) | \(1/(b-a)\) | \((a+b)/2\) | \((b-a)^2/12\) |
| Exponential \((\lambda)\) | \(\lambda e^{-\lambda x}\) | \(1/\lambda\) | \(1/\lambda^2\) |
| Normal \((\mu,\sigma^2)\) | Gaussian formula | \(\mu\) | \(\sigma^2\) |
| Gamma \((\alpha,\lambda)\) | \(\frac{\lambda^\alpha}{\Gamma(\alpha)}x^{\alpha-1}e^{-\lambda x}\) | \(\alpha/\lambda\) | \(\alpha/\lambda^2\) |
| Chi-Square \((k)\) | special Gamma | \(k\) | \(2k\) |
| F \((d_1,d_2)\) | ratio of chi-square variables | \(d_2/(d_2-2)\) | formula above |
| Beta \((\alpha,\beta)\) | \(\frac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha,\beta)}\) | \(\alpha/(\alpha+\beta)\) | \(\frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}\) |
| Log-Normal | log of variable is normal | \(e^{\mu+\sigma^2/2}\) | \(e^{2\mu+\sigma^2}(e^{\sigma^2}-1)\) |
| Cauchy | heavy-tailed density | DNE | DNE |
| Pareto | \(\frac{\alpha x_m^\alpha}{x^{\alpha+1}}\) | \(\frac{\alpha x_m}{\alpha-1}\) | \(\frac{x_m^2\alpha}{(\alpha-1)^2(\alpha-2)}\) |
| Weibull | \(\frac{k}{\lambda}(x/\lambda)^{k-1}e^{-(x/\lambda)^k}\) | \(\lambda\Gamma(1+1/k)\) | \(\lambda^2[\Gamma(1+2/k)-\Gamma^2(1+1/k)]\) |

---

# End of Notes