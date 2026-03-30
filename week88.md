# 📘 Multivariate Probability & Statistics: Complete Guide (NPTEL)

---

# PART 1: MULTIVARIATE DISTRIBUTIONS — FUNDAMENTALS

---

## 🔷 CONCEPT 1: Joint Cumulative Distribution Function (CDF)

### Explanation
For a random vector **X** = (X₁, X₂, …, Xₙ) in ℝⁿ, the joint CDF is:
```
F(x₁, x₂, …, xₙ) = P(X₁ ≤ x₁, X₂ ≤ x₂, …, Xₙ ≤ xₙ)
```

**Four Key Properties:**
1. **Monotonicity:** F never decreases in any coordinate
2. **Right-Continuity:** F jumps from the right at discontinuity points
3. **Boundary Conditions:**
   - F → 0 if any xᵢ → −∞
   - F → 1 if all xᵢ → +∞
4. **Non-negative Increment:** Probability assigned to any box in ℝⁿ is always ≥ 0

### Detailed Example: Die + Coin Experiment

**Scenario:** Roll a fair die (X = face value 1-6) and toss a fair coin (Y = 0 for tails, 1 for heads).

**Sample Space:** 12 equally likely outcomes, each with probability 1/12.

**Computing F(2, 0):**
```
F(2, 0) = P(X ≤ 2, Y ≤ 0) 
        = P(X=1, Y=0) + P(X=2, Y=0)
        = 1/12 + 1/12 
        = 1/6 ≈ 0.167
```

**Verification:** Only outcomes (1,0) and (2,0) satisfy X≤2 and Y≤0.

**Piecewise CDF Structure:**
```
F(x,y) = 0                          if x < 1 or y < 0
       = (1/12)⌊x⌋                 if 0 ≤ y < 1, 1 ≤ x < 6
       = (1/6)⌊x⌋                  if y ≥ 1, 1 ≤ x < 6
       = 1                          if x ≥ 6, y ≥ 1
```

**Visualization in 2D:**
```
Y (Coin)
1 |     ████████████████  F jumps to 1/2, 2/3, 5/6, 1 as x increases
  |     ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
0 | ░░░░▒▒▒▒▓▓▓▓████
  +------------------→ X (Die)
    1   2   3   4   5   6
```

---

## 🔷 CONCEPT 2: Joint Probability Mass Function (PMF) — Discrete Case

### Explanation
A random vector **X** = (X₁, …, Xₙ) is **discrete** if it takes values from a countable set A with probability 1. The joint PMF assigns positive probability to each "jump point":
```
p_{i₁i₂…iₙ} = P(X₁ = x₁ᵢ₁, X₂ = x₂ᵢ₂, …, Xₙ = xₙᵢₙ)
```

**Normalization:** Σ pᵢ₁ᵢ₂…ᵢₙ = 1 (sum over all possible combinations)

### Detailed Example: Three Coin Tosses

**Scenario:** Toss 3 fair coins. Define:
- **X** = number of heads (0, 1, 2, 3)
- **Y** = |heads − tails| = |2X − 3| (1 or 3)

**Sample Space Analysis:**
| Outcome | X | Y | Probability |
|---------|---|---|-------------|
| TTT | 0 | 3 | 1/8 |
| HTT, THT, TTH | 1 | 1 | 3/8 |
| HHT, HTH, THH | 2 | 1 | 3/8 |
| HHH | 3 | 3 | 1/8 |

**Joint PMF Table:**

| p(x,y) | X=0 | X=1 | X=2 | X=3 | **P(Y=y)** |
|--------|-----|-----|-----|-----|------------|
| **Y=1** | 0 | 3/8 | 3/8 | 0 | **6/8 = 3/4** |
| **Y=3** | 1/8 | 0 | 0 | 1/8 | **2/8 = 1/4** |
| **P(X=x)** | **1/8** | **3/8** | **3/8** | **1/8** | **1** |

**Key Observations:**
- Row totals = Marginal PMF of Y
- Column totals = Marginal PMF of X
- Zero entries where combinations are impossible (e.g., X=0, Y=1 is impossible)

**Verification:** All probabilities sum to 1/8 + 3/8 + 3/8 + 1/8 = 1 ✓

---

## 🔷 CONCEPT 3: Joint Probability Density Function (PDF) — Continuous Case

### Explanation
A random vector **X** = (X₁, …, Xₙ) is **continuous** if there exists a non-negative function f such that:
```
F(x₁, …, xₙ) = ∫_{-∞}^{x₁} … ∫_{-∞}^{xₙ} f(u₁, …, uₙ) duₙ … du₁
```

**Properties:**
- f(x₁, …, xₙ) ≥ 0 for all x
- ∫_{-∞}^{∞} … ∫_{-∞}^{∞} f(x₁, …, xₙ) dx₁…dxₙ = 1
- P(X ∈ A) = ∫_A f(x) dx (probability as volume under density surface)

### Detailed Example: Triangular Region

**PDF:**
```
f(x, y) = 2   for 0 < x < y < 1
        = 0   elsewhere
```

**Verification (Normalization):**
```
∫∫ f(x,y) dx dy = ∫₀¹ ∫₀ʸ 2 dx dy
                = ∫₀¹ 2y dy
                = [y²]₀¹ 
                = 1  ✓
```

**Geometric Interpretation:**
```
Y
1 |      /|
  |     / |
  |    /  |  f=2 in this triangle
  |   /   |  f=0 outside
  |  /    |
  | /     |
  |/______|
  0        1    X
```

**Probability Calculation:** P(X < 0.5, Y > 0.5)
```
= ∫_{0.5}^{1} ∫_{0}^{min(y,0.5)} 2 dx dy
= ∫_{0.5}^{1} 2(0.5) dy   [since x < 0.5 and x < y]
= ∫_{0.5}^{1} 1 dy
= 0.5
```

---

## 🔷 CONCEPT 4: Marginal Distributions

### Explanation
The marginal distribution of a subset of variables is obtained by "summing out" (discrete) or "integrating out" (continuous) the other variables.

**Discrete:**
```
P(Xₖ = xₖ) = Σ_{all other indices} p(i₁, …, iₙ)
```

**Continuous:**
```
fₖ(xₖ) = ∫_{-∞}^{∞} … ∫_{-∞}^{∞} f(x₁, …, xₙ) dx₁…dxₖ₋₁ dxₖ₊₁…dxₙ
```

### Detailed Example 1: Discrete (from Coin Toss)

**Marginal of X (sum over Y):**
```
P(X=0) = p(0,1) + p(0,3) = 0 + 1/8 = 1/8
P(X=1) = p(1,1) + p(1,3) = 3/8 + 0 = 3/8
P(X=2) = 3/8 + 0 = 3/8
P(X=3) = 0 + 1/8 = 1/8
```

**Marginal of Y (sum over X):**
```
P(Y=1) = 0 + 3/8 + 3/8 + 0 = 3/4
P(Y=3) = 1/8 + 0 + 0 + 1/8 = 1/4
```

### Detailed Example 2: Continuous (from Triangular PDF)

**Marginal of X:**
```
f₁(x) = ∫_{x}^{1} 2 dy = 2(1-x)   for 0 < x < 1
      = 0                         elsewhere
```

**Check:** ∫₀¹ 2(1-x) dx = [2x - x²]₀¹ = 2 - 1 = 1 ✓

**Marginal of Y:**
```
f₂(y) = ∫_{0}^{y} 2 dx = 2y   for 0 < y < 1
      = 0                     elsewhere
```

**Check:** ∫₀¹ 2y dy = [y²]₀¹ = 1 ✓

**Visual Interpretation:**
- f₁(x) = 2(1-x): Linear decrease from 2 (at x=0) to 0 (at x=1)
- f₂(y) = 2y: Linear increase from 0 (at y=0) to 2 (at y=1)

---

## 🔷 CONCEPT 5: Conditional Distributions and Conditional Expectation

### Explanation
**Conditional PMF (discrete):**
```
P(X = x | Y = y) = P(X = x, Y = y) / P(Y = y)
```

**Conditional PDF (continuous):**
```
f_{X|Y}(x|y) = f_{X,Y}(x,y) / f_Y(y)
```

**Conditional Expectation:**
```
E[X | Y = y] = ∫ x · f_{X|Y}(x|y) dx   (continuous)
             = Σ x · P(X=x | Y=y)     (discrete)
```

**Key Properties:**
1. **Linearity:** E[aX + bZ | Y] = aE[X|Y] + bE[Z|Y]
2. **Law of Total Expectation:** E[E[X|Y]] = E[X]
3. **Independence:** If X ⊥ Y, then E[X|Y] = E[X]
4. **Tower Property:** E[E[X|Y,Z]|Y] = E[X|Y]

### Detailed Example 1: Discrete (Coin Toss)

**Scenario:** X = total heads in 2 flips, Y = indicator of head on first flip (0 or 1).

**Conditional Expectations:**
```
Given Y=1 (first is Head):
Possible outcomes: HT, HH
X values: 1, 2
E[X|Y=1] = (1 + 2)/2 = 1.5

Given Y=0 (first is Tail):
Possible outcomes: TT, TH  
X values: 0, 1
E[X|Y=0] = (0 + 1)/2 = 0.5
```

**Law of Total Expectation:**
```
E[X] = E[X|Y=1]·P(Y=1) + E[X|Y=0]·P(Y=0)
     = 1.5 × 0.5 + 0.5 × 0.5
     = 0.75 + 0.25
     = 1.0  ✓
```
(Actual E[X] for 2 coins = 1, verified!)

### Detailed Example 2: Continuous (Triangular Region)

**Given:** f(x,y) = 2 for 0 < x < y < 1

**Step 1:** Find marginal f_Y(y) = 2y (from Concept 4)

**Step 2:** Find conditional
```
f_{X|Y}(x|y) = f(x,y) / f_Y(y) = 2 / (2y) = 1/y   for 0 < x < y
```

**Interpretation:** Given Y=y, X is Uniform on (0,y)!

**Conditional Expectation:**
```
E[X|Y=y] = ∫₀ʸ x · (1/y) dx 
         = (1/y) · [x²/2]₀ʸ
         = (1/y) · (y²/2)
         = y/2
```

**As a random variable:** E[X|Y] = Y/2

**Law of Total Expectation:**
```
E[X] = E[E[X|Y]] = E[Y/2] = (1/2)E[Y]

E[Y] = ∫₀¹ y · 2y dy = 2∫₀¹ y² dy = 2/3

Therefore: E[X] = (1/2)(2/3) = 1/3  ✓
```

**Verification via marginal:** E[X] = ∫₀¹ x · 2(1-x) dx = 2[x²/2 - x³/3]₀¹ = 2(1/2 - 1/3) = 1/3 ✓

---

# PART 2: BIVARIATE NORMAL DISTRIBUTION

---

## 🔷 CONCEPT 6: Definition and Parameters

### Explanation
The **bivariate normal** distribution is the fundamental model for two correlated continuous variables. Its PDF is:
```
f(x,y) = 1/(2πσ_X σ_Y √(1−ρ²)) · exp{−Q(x,y) / [2(1−ρ²)]}
```

where the **quadratic form** is:
```
Q(x,y) = [(x−µ_X)/σ_X]² − 2ρ[(x−µ_X)/σ_X][(y−µ_Y)/σ_Y] + [(y−µ_Y)/σ_Y]²
```

**Five Parameters:**
| Parameter | Symbol | Meaning |
|-----------|--------|---------|
| Mean of X | µ_X | Center location in x-direction |
| Mean of Y | µ_Y | Center location in y-direction |
| Std dev X | σ_X | Spread in x-direction |
| Std dev Y | σ_Y | Spread in y-direction |
| Correlation | ρ | Linear dependence (−1 ≤ ρ ≤ 1) |

**Covariance Matrix:**
```
Σ = [ σ_X²      ρσ_Xσ_Y  ]
    [ ρσ_Xσ_Y   σ_Y²     ]
```

### Detailed Example: Height and Weight

**Parameters for adult males:**
- µ_X = 170 cm (height), σ_X = 10 cm
- µ_Y = 70 kg (weight), σ_Y = 15 kg  
- ρ = 0.7 (positive correlation)

**PDF Structure:**
- Centered at (170, 70)
- Elliptical contours tilted upward (positive ρ)
- Narrower in height direction (σ_X < σ_Y)
- Stretched along major axis determined by ρ

**Real-world contexts where bivariate normal arises:**
- Height and weight of individuals
- Exam scores in two related subjects (Math and Physics)
- Returns on two correlated stocks
- Blood pressure (systolic, diastolic)

---

## 🔷 CONCEPT 7: Geometry — Elliptical Contours

### Explanation
Setting f(x,y) = constant yields **Q(x,y) = constant**, which defines an **ellipse**. The shape reveals the correlation structure.

**Ellipse Geometry:**
- **Center:** (µ_X, µ_Y)
- **Axes directions:** Eigenvectors of Σ
- **Axes lengths:** Proportional to √λ₁, √λ₂ where λ are eigenvalues of Σ
- **Tilt angle θ:** tan(2θ) = 2ρσ_Xσ_Y / (σ_X² − σ_Y²)

### Detailed Example: Effect of Correlation ρ

**Case 1: ρ = 0 (Independent)**
```
    Y
    |   ◯◯◯
    |  ◯   ◯   (Axis-aligned circle if σ_X=σ_Y)
    | ◯  ●  ◯   or ellipse if σ_X≠σ_Y
    |  ◯   ◯
    |   ◯◯◯
    +----------→ X
```

**Case 2: ρ = +0.8 (Strong positive)**
```
    Y
    |    ╱──╲
    |   ╱    ╲   (Tilted up-right)
    |  ╱  ●   ╲  Major axis: y increases with x
    | ╱        ╲
    |╱__________╲
    +----------→ X
```

**Case 3: ρ = −0.8 (Strong negative)**
```
    Y
    |╲          ╱
    | ╲        ╱   (Tilted up-left)
    |  ╲  ●   ╱    Major axis: y decreases as x increases
    |   ╲    ╱
    |    ╲──╱
    +----------→ X
```

**Case 4: Equal variances (σ_X = σ_Y = σ)**
- Eigenvalues: λ₁ = σ²(1+ρ), λ₂ = σ²(1−ρ)
- Eigenvectors: [1,1]ᵀ and [1,−1]ᵀ (rotated 45°)
- When ρ > 0: Major axis along y=x line (45°)
- When ρ < 0: Major axis along y=−x line (−45°)

---

## 🔷 CONCEPT 8: Marginal and Conditional Distributions

### Explanation
**Marginal Distributions:**
- X ~ N(µ_X, σ_X²)
- Y ~ N(µ_Y, σ_Y²)

**Conditional Distribution:** Given Y=y, X is normal with:
```
Mean:   µ_{X|Y} = µ_X + ρ(σ_X/σ_Y)(y − µ_Y)
Variance: σ²_{X|Y} = σ_X²(1 − ρ²)
```

**Key Insights:**
1. **Linear regression:** The conditional mean is linear in y
2. **Variance reduction:** Knowing Y reduces variance by factor (1−ρ²)
3. **Perfect correlation (ρ=±1):** Variance becomes 0 (X completely determined by Y)

### Detailed Example: Height given Weight

**Given:** µ_X=170, µ_Y=70, σ_X=10, σ_Y=15, ρ=0.7

**Person weighs Y=85 kg (1 std dev above mean):**

**Predicted height:**
```
E[X|Y=85] = 170 + 0.7×(10/15)×(85−70)
          = 170 + 0.7×0.667×15
          = 170 + 7
          = 177 cm
```

**Uncertainty:**
```
Var(X|Y=85) = 100 × (1 − 0.49) = 51
σ_{X|Y} = √51 ≈ 7.1 cm  (vs 10 cm marginally)
```

**Interpretation:** 
- Without knowing weight: best guess 170±10 cm
- Knowing weight is 85 kg: best guess 177±7.1 cm
- Information reduced uncertainty from 10 cm to 7.1 cm

**When ρ = −0.8:**
```
E[X|Y=85] = 170 − 0.8×(10/15)×15 = 170 − 8 = 162 cm
```
Heavier person predicted to be shorter (negative correlation example).

---

## 🔷 CONCEPT 9: Independence ↔ Zero Correlation

### Explanation
For **bivariate normal only**: ρ = 0 ⟺ Independence

**When ρ = 0:**
```
Q(x,y) = [(x−µ_X)/σ_X]² + [(y−µ_Y)/σ_Y]²
f(x,y) = [1/(√2πσ_X)exp(−(x−µ_X)²/2σ_X²)] × [1/(√2πσ_Y)exp(−(y−µ_Y)²/2σ_Y²)]
       = f_X(x) · f_Y(y)
```

The joint PDF factors into product of marginals — the definition of independence!

**Critical Distinction:** This is **unique** to normal distributions. For other distributions, uncorrelated does NOT imply independent.

### Detailed Example: Counterexample (Non-normal)

**Construction:**
- X ~ N(0,1)
- W ~ Bernoulli(1/2) (coin flip)
- Y = (2W−1)X = { X if W=1, −X if W=0 }

**Properties:**
- Y ~ N(0,1) (symmetric)
- Cov(X,Y) = E[XY] − E[X]E[Y] = E[X²(2W−1)] = E[X²]E[2W−1] = 1×0 = 0

**But (X,Y) is NOT bivariate normal!**
- Points concentrated on two lines: y=x and y=−x
- Not an elliptical contour!
- Clearly dependent: knowing X completely determines |Y|

**Visualization:**
```
    Y
    |    /
    |   /  (Points only on diagonals)
    |  / 
    | /
    |/______→ X
```

---

# PART 3: MULTIVARIATE NORMAL DISTRIBUTION

---

## 🔷 CONCEPT 10: Definition of Nₚ(µ, Σ)

### Explanation
A p-dimensional random vector **X** = (X₁, …, Xₚ)ᵀ follows **Nₚ(µ, Σ)** if:
1. Every linear combination aᵀX follows a univariate normal distribution
2. The PDF (when Σ is positive definite) is:
```
f(x) = 1/[(2π)^(p/2) |Σ|^(1/2)] · exp{−(x−µ)ᵀΣ⁻¹(x−µ)/2}
```

**Parameters:**
- **µ:** p×1 mean vector
- **Σ:** p×p positive definite covariance matrix
- **|Σ|:** Determinant of Σ (measures volume of uncertainty)

**Connection to 1D:** When p=1, this reduces to the familiar univariate normal with (x−µ)²/σ² in the exponent. The term (x−µ)ᵀΣ⁻¹(x−µ) is the **Mahalanobis distance** squared — accounting for correlations and different variances.

### Detailed Example: 4-Variate Normal with Independence

**Given PDF:**
```
f(x) = (1/48π²) · exp{−½[(x₁−2)²/6 + (x₂+1)²/3 + x₃²/4 + (x₄−4)²/2]}
```

**Identification:**
- No cross-terms (xᵢxⱼ) in the exponent → independent components
- Σ is diagonal: Σ = diag(6, 3, 4, 2)
- µ = (2, −1, 0, 4)ᵀ

**Verification of constant:**
```
(2π)^(4/2) = (2π)² = 4π²
|Σ|^(1/2) = √(6×3×4×2) = √144 = 12
Constant = 1/(4π² × 12) = 1/(48π²)  ✓
```

---

## 🔷 CONCEPT 11: Four Key Properties

### Explanation

**Property 1: Linear Transformations**
```
If X ~ Nₚ(µ, Σ), then AX + d ~ N_q(Aµ + d, AΣAᵀ)
```
for any q×p matrix A and q×1 vector d.

**Property 2: Marginal Normality**
Any subset of variables is multivariate normal. Partition X = [X₁, X₂]ᵀ, then:
```
X₁ ~ N_q(µ₁, Σ₁₁)
```

**Property 3: Zero Covariance ⟺ Independence**
Subsets X₁ and X₂ are independent iff Σ₁₂ = 0 (off-diagonal block is zero matrix).

**Property 4: Quadratic Form**
```
(X−µ)ᵀΣ⁻¹(X−µ) ~ χ²ₚ
```
(Chi-squared with p degrees of freedom)

This defines probability ellipsoids: the set {x : (x−µ)ᵀΣ⁻¹(x−µ) ≤ χ²ₚ(α)} contains probability 1−α.

### Detailed Example: Independence Check

**Given:** X = (X₁, X₂, X₃)ᵀ ~ N₃(µ, Σ) with:
```
Σ = [ 4  1  0 ]
    [ 1  3  0 ]
    [ 0  0  2 ]
```

**Partition:** X₁ = (X₁, X₂)ᵀ, X₂ = X₃

**Check Σ₁₂:**
```
Σ = [ Σ₁₁  | Σ₁₂ ]
    [------+-----]
    [ Σ₂₁  | Σ₂₂ ]

Σ₁₂ = [ 0 ]
      [ 0 ]  (2×1 zero vector)
```

**Conclusion:** Since Σ₁₂ = 0, (X₁, X₂) and X₃ are **independent**.

**But:** X₁ and X₂ have σ₁₂ = 1 ≠ 0, so they are **not independent** of each other.

**Implication:** We can model X₃ separately from (X₁, X₂), but must model X₁ and X₂ jointly.

---

# PART 4: SAMPLING DISTRIBUTIONS & INFERENCE

---

## 🔷 CONCEPT 12: Sample Mean Vector and Covariance Matrix

### Explanation
For n i.i.d. observations X₁, …, Xₙ from p-dimensional distribution, arranged as n×p data matrix **X**:

**Sample Mean Vector:**
```
X̄ = (1/n) Xᵀ**1**   (column means)
```

**Sample Covariance Matrix:**
```
S = 1/(n−1) · Xᵀ(I − **11**ᵀ/n)X
```
where **1** is vector of ones, I is identity matrix.

**Entry (i,k):**
```
sᵢₖ = 1/(n−1) Σⱼ(xⱼᵢ − X̄ᵢ)(xⱼₖ − X̄ₖ)
```

**Unbiasedness Properties:**
- E[X̄] = µ
- Cov(X̄) = (1/n)Σ
- E[S] = Σ (unbiased estimator)

**Biased alternative:** Sₙ = (n−1)S/n = (1/n)Σ(Xⱼ−X̄)(Xⱼ−X̄)ᵀ divides by n instead of n−1.

### Detailed Example: 2D Data

**Data (n=4):**
```
    X₁  X₂
X = [ 1   2 ]
    [ 3   4 ]
    [ 5   6 ]
    [ 7   8 ]
```

**Sample Mean:**
```
X̄₁ = (1+3+5+7)/4 = 4
X̄₂ = (2+4+6+8)/4 = 5
X̄ = [4, 5]ᵀ
```

**Centered Data:**
```
    -3  -3
    -1  -1
     1   1
     3   3
```

**Sample Covariance:**
```
s₁₁ = (9+1+1+9)/3 = 20/3 ≈ 6.67
s₂₂ = (9+1+1+9)/3 = 20/3 ≈ 6.67  
s₁₂ = (9+1+1+9)/3 = 20/3 ≈ 6.67

S = [ 6.67  6.67 ]
    [ 6.67  6.67 ]
```

**Interpretation:** Perfect correlation (ρ=1) because X₂ = X₁ + 1 exactly!

---

## 🔷 CONCEPT 13: Wishart Distribution and Sampling Properties

### Explanation
For X₁, …, Xₙ iid Nₚ(µ, Σ):

**Sampling Distributions:**
1. **X̄ ~ Nₚ(µ, (1/n)Σ)** exactly
2. **(n−1)S ~ Wishartₚ(n−1, Σ)** — the multivariate chi-squared
3. **X̄ and S are independent**

**Wishart Distribution:** Generalization of chi-squared. If Z₁, …, Zₙ ~ Nₚ(0,Σ) iid, then Σ ZᵢZᵢᵀ ~ Wishartₚ(n, Σ).

**Univariate case (p=1):** Wishart reduces to σ²χ²ₙ₋₁.

**Central Limit Theorem (Multivariate):**
For large n:
```
√n(X̄ − µ) ≈ Nₚ(0, Σ)
n(X̄ − µ)ᵀS⁻¹(X̄ − µ) ≈ χ²ₚ
```

---

## 🔷 CONCEPT 14: Maximum Likelihood Estimation (MLE)

### Explanation
For random sample from Nₚ(µ, Σ), find parameters maximizing likelihood.

**Likelihood Function:**
```
L(µ, Σ) = ∏ⱼ f(Xⱼ; µ, Σ)
```

**Log-Likelihood (using trace trick):**
```
ln L = −(np/2)ln(2π) − (n/2)ln|Σ| − ½Σ(Xⱼ−µ)ᵀΣ⁻¹(Xⱼ−µ)
```

**Key Identity:**
```
Σ(Xⱼ−µ)ᵀΣ⁻¹(Xⱼ−µ) = tr[Σ⁻¹Σ(Xⱼ−X̄)(Xⱼ−X̄)ᵀ] + n(X̄−µ)ᵀΣ⁻¹(X̄−µ)
```

**MLE Solutions:**
1. **µ̂ = X̄** (sample mean)
   - Maximizes by making second term zero
   
2. **Σ̂ = (1/n) Σ(Xⱼ−X̄)(Xⱼ−X̄)ᵀ = (n−1)S/n**
   - Biased! Divides by n, not n−1

### Detailed Example: MLE vs Unbiased

**Scenario:** n=100 observations of 3 variables.

**If S (unbiased) calculates to:**
```
S = [ 4  1  0 ]
    [ 1  3  1 ]
    [ 0  1  2 ]
```

**Then MLE is:**
```
Σ̂ = (99/100) × S = 0.99 × S

Σ̂ = [ 3.96  0.99  0   ]
    [ 0.99  2.97  0.99]
    [ 0     0.99  1.98]
```

**Bias:** E[Σ̂] = (n−1)/n × Σ = 0.99Σ, so bias = −0.01Σ (small for large n).

---

# PART 5: HYPOTHESIS TESTING AND MODEL CHECKING

---

## 🔷 CONCEPT 15: Hotelling's T² Test

### Explanation
The multivariate generalization of the t-test for:
```
H₀: µ = µ₀ vs H₁: µ ≠ µ₀
```

**Test Statistic:**
```
T² = n(X̄ − µ₀)ᵀ S⁻¹ (X̄ − µ₀)
```

**Distribution under H₀:**
```
T² ~ [(n−1)p/(n−p)] × F_{p, n−p}
```

**Decision Rule:** Reject H₀ at level α if:
```
T² > [(n−1)p/(n−p)] × F_{p, n−p}(α)
```

**Intuition:** Compares the scaled Mahalanobis distance between sample mean and hypothesized mean, accounting for sample covariance structure.

### Detailed Example: Testing Mean Vector

**Scenario:** Test if population mean height-weight is µ₀ = (170, 70)ᵀ.

**Sample (n=50):**
- X̄ = (172, 73)ᵀ
- S = [ 100   120 ]
      [ 120   225 ]  (correlation ≈ 0.8)

**Compute S⁻¹:**
```
|S| = 100×225 − 120² = 22500 − 14400 = 8100
S⁻¹ = (1/8100) [ 225  −120 ]
               [ −120  100 ]
```

**Compute T²:**
```
X̄ − µ₀ = [2, 3]ᵀ

(X̄−µ₀)ᵀS⁻¹(X̄−µ₀) = [2, 3] × (1/8100) [ 225  −120 ] [2]
                                           [ −120  100 ] [3]

= (1/8100) [2, 3] · [ 225×2 − 120×3 ] 
                  [ −120×2 + 100×3 ]

= (1/8100) [2, 3] · [ 450−360 ]
                  [ −240+300 ]

= (1/8100) [2, 3] · [90]
                  [60]

= (1/8100) (180 + 180) = 360/8100 ≈ 0.0444

T² = 50 × 0.0444 ≈ 2.22
```

**Critical Value (α=0.05):**
```
p=2, n=50
[(49×2)/48] × F_{2,48}(0.05) = 2.042 × 3.19 ≈ 6.51
```

**Conclusion:** T² = 2.22 < 6.51, so **fail to reject H₀**. The observed mean (172, 73) is not significantly different from (170, 70) given the sample covariance.

---

## 🔷 CONCEPT 16: Q-Q Plot for Normality Assessment

### Explanation
**Q-Q (Quantile-Quantile) Plot** assesses whether data follow a theoretical distribution (usually normal).

**Construction Steps:**
1. Sort data: x₍₁₎ ≤ x₍₂₎ ≤ … ≤ x₍ₙ₎
2. Compute probability levels: p₍ⱼ₎ = (j − ½)/n
3. Find theoretical quantiles: q₍ⱼ₎ = Φ⁻¹(p₍ⱼ₎) where Φ is standard normal CDF
4. Plot (q₍ⱼ₎, x₍ⱼ₎) — theoretical vs sample quantiles

**Interpretation:**
| Pattern | Meaning |
|---------|---------|
| Straight line | Data consistent with normal distribution |
| S-curve | Heavy tails (more extreme values than normal) |
| Inverted S | Light tails (fewer extreme values than normal) |
| Curved (bow) | Skewed distribution |
| Points deviating at ends | Outliers or non-normal tails |

### Detailed Example: Small Sample (n=10)

**Data (sorted):** −1.00, −0.10, 0.25, 0.42, 0.62, 0.81, 1.05, 1.30, 1.71, 2.30

**Q-Q Plot Construction:**

| j | x₍ⱼ₎ | p₍ⱼ₎=(j−0.5)/10 | q₍ⱼ₎ (z-score) |
|---|------|------------------|----------------|
| 1 | −1.00 | 0.05 | −1.645 |
| 2 | −0.10 | 0.15 | −1.036 |
| 3 | 0.25 | 0.25 | −0.674 |
| 4 | 0.42 | 0.35 | −0.385 |
| 5 | 0.62 | 0.45 | −0.125 |
| 6 | 0.81 | 0.55 | +0.125 |
| 7 | 1.05 | 0.65 | +0.385 |
| 8 | 1.30 | 0.75 | +0.674 |
| 9 | 1.71 | 0.85 | +1.036 |
| 10 | 2.30 | 0.95 | +1.645 |

**Plot Analysis:**
- Points roughly follow line y = x (or slightly steeper)
- No systematic curvature
- End points don't deviate excessively

**Conclusion:** Sample consistent with normality despite small n=10.

**Multivariate Extension:** Check each marginal distribution with Q-Q plots, and check Mahalanobis distances (X−X̄)ᵀS⁻¹(X−X̄) against χ² quantiles.

---

## 📌 Master Summary Table

| Concept | Key Formula | Interpretation |
|---------|-------------|----------------|
| **Joint CDF** | F(x,y) = P(X≤x, Y≤y) | Probability in lower-left quadrant |
| **Joint PMF** | p(x,y) = P(X=x, Y=y) | Probability mass at point (x,y) |
| **Joint PDF** | f(x,y) = ∂²F/∂x∂y | Density at (x,y), integrates to probability |
| **Marginal** | f_X(x) = ∫ f(x,y)dy | Remove other variable by integration |
| **Conditional** | f_{X|Y} = f(x,y)/f_Y(y) | Density of X given specific Y=y |
| **Conditional Expectation** | E[X|Y=y] = ∫x·f_{X|Y}dx | Best prediction of X given Y |
| **Law of Total Expectation** | E[X] = E[E[X|Y]] | Tower property, marginal from conditional |
| **Bivariate Normal** | f ∝ exp(−Q/2(1−ρ²)) | Elliptical contours, 5 parameters |
| **Conditional Mean** | µ_X + ρ(σ_X/σ_Y)(y−µ_Y) | Linear regression function |
| **Conditional Variance** | σ_X²(1−ρ²) | Reduction in uncertainty |
| **Independence** | ρ=0 ⟺ independent | Unique to normal distributions |
| **Multivariate Normal** | X ~ Nₚ(µ, Σ) | Linear combos are univariate normal |
| **Mahalanobis** | (x−µ)ᵀΣ⁻¹(x−µ) | Distance accounting for covariance |
| **Sample Mean** | X̄ = (1/n)ΣXᵢ | Unbiased estimator of µ |
| **Sample Cov** | S = 1/(n−1)Σ(Xᵢ−X̄)(Xᵢ−X̄)ᵀ | Unbiased estimator of Σ |
| **Wishart** | (n−1)S ~ Wishartₚ(n−1, Σ) | Sampling distribution of covariance |
| **MLE** | µ̂=X̄, Σ̂=(n−1)S/n | Biased but asymptotically optimal |
| **Hotelling T²** | n(X̄−µ₀)ᵀS⁻¹(X̄−µ₀) | Multivariate distance test statistic |
| **Q-Q Plot** | Plot (Φ⁻¹(pⱼ), x₍ⱼ₎) | Visual normality check |

---

## 🔗 The Unifying Thread: The Covariance Matrix Σ

Every concept in multivariate statistics revolves around **Σ**:

| Role of Σ | Manifestation |
|-----------|---------------|
| **Shape** | Controls elliptical contours of bivariate normal (eigenvectors = axes, eigenvalues = spreads) |
| **Independence** | Zero off-diagonal blocks ⟺ independent subvectors |
| **Precision** | Cov(X̄) = (1/n)Σ — determines uncertainty in sample mean |
| **Sampling** | (n−1)S follows Wishart — the "randomness" of sample covariance |
| **Testing** | Hotelling's T² uses S⁻¹ — inverse covariance defines Mahalanobis distance |
| **Reduction** | Eigenvectors of Σ (or S) give principal components for dimensionality reduction |

**Understanding Σ** — its estimation (MLE vs unbiased), its structure (independence blocks), its eigen-decomposition (principal directions), and its geometry (ellipsoids) — is the foundation of all multivariate analysis.
