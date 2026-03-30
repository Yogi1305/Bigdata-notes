```markdown
# 📘 Complete Guide: Multivariate Probability & Statistical Inference

---

# PART 1: MULTIVARIATE DISTRIBUTIONS — FUNDAMENTALS

---

## 🔷 CONCEPT 1: Joint Cumulative Distribution Function (CDF) in Rⁿ

### Explanation
For a random vector **X** = (X₁, X₂, ..., Xₙ) in n-dimensional space, the **joint CDF** gives the probability that each component falls at or below specified values simultaneously:

```
F(x₁, x₂, ..., xₙ) = P(X₁ ≤ x₁, X₂ ≤ x₂, ..., Xₙ ≤ xₙ)
```

**Four Essential Properties:**

1. **Monotonicity:** F is non-decreasing in each argument. If xᵢ increases (holding others fixed), F cannot decrease.

2. **Right-Continuity:** F is continuous from the right in each variable. Small increases in any xᵢ don't cause jumps downward.

3. **Boundary Conditions:**
   - If any xᵢ → −∞, then F → 0
   - If all xᵢ → +∞, then F → 1

4. **Non-negative Increment:** For any hyper-rectangle [a₁,b₁] × ... × [aₙ,bₙ], the probability is non-negative:
   ```
   P(a₁ < X₁ ≤ b₁, ..., aₙ < Xₙ ≤ bₙ) ≥ 0
   ```

### Detailed Example: Die and Coin Experiment

**Scenario:** Roll a fair die (X = face value 1-6) and flip a fair coin (Y = 0 for tails, 1 for heads).

**Sample Space:** 12 equally likely outcomes, each with probability 1/12.

**Computing F(3.5, 0.5):**
```
F(3.5, 0.5) = P(X ≤ 3.5, Y ≤ 0.5)
            = P(X ∈ {1,2,3}, Y = 0)
            = P({(1,0), (2,0), (3,0)})
            = 3/12 = 1/4 = 0.25
```

**Piecewise CDF Structure:**
```
F(x,y) = 0                          if x < 1 or y < 0
       = (1/12)⌊x⌋                 if 0 ≤ y < 1 and 1 ≤ x < 7
       = (1/6)⌊x⌋                  if y ≥ 1 and 1 ≤ x < 7
       = 1                          if x ≥ 6 and y ≥ 1
```

**Verification at boundary points:**
- F(6, 1) = P(X ≤ 6, Y ≤ 1) = P(entire sample space) = 1 ✓
- F(0.5, 0) = P(X ≤ 0.5) = 0 (impossible die roll) ✓

**Visualization in 2D:**
```
Y (Coin)
1 |████████████████████████████████  F = 6/6 = 1
  |████████████████████████████████  
0 |░░░░░░░░░░░░▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  F increases with X
  |            1  2  3  4  5  6
  +----------------------------→ X (Die)
    At Y=0, F increases in steps of 1/6 as X passes 1,2,3,4,5,6
```

---

## 🔷 CONCEPT 2: Discrete Multivariate Distributions & Joint PMF

### Explanation
A random vector **X** = (X₁, ..., Xₙ) is **discrete** if it takes values from a countable set (finite or countably infinite). The **Joint Probability Mass Function (PMF)** assigns positive probability to each "jump point":

```
p_{i₁i₂...iₙ} = P(X₁ = x₁ᵢ₁, X₂ = x₂ᵢ₂, ..., Xₙ = xₙᵢₙ)
```

**Requirements:**
- p_{i₁...iₙ} ≥ 0 for all combinations
- Σ_{all combinations} p_{i₁...iₙ} = 1 (normalization)

### Detailed Example: Three Coin Tosses

**Scenario:** Toss a fair coin 3 times. Define:
- **X** = number of heads (0, 1, 2, 3)
- **Y** = |heads − tails| = |2X − 3| (possible values: 1 or 3)

**Sample Space Analysis:**

| Outcome | X (Heads) | Y = |2X-3| | Probability |
|---------|-----------|----------------|-------------|
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
- Zero entries indicate impossible combinations (e.g., X=0 and Y=1 cannot happen)
- Row totals give marginal distribution of Y
- Column totals give marginal distribution of X
- P(X=1, Y=1) = 3/8 represents probability of exactly 1 head (and thus |2(1)-3|=1)

**Verification:** Sum of all entries = 0+3/8+3/8+0+1/8+0+0+1/8 = 8/8 = 1 ✓

---

## 🔷 CONCEPT 3: Continuous Multivariate Distributions & Joint PDF

### Explanation
A random vector **X** = (X₁, ..., Xₙ) is **continuous** if there exists a non-negative **Joint Probability Density Function (PDF)** f(x₁, ..., xₙ) such that:

```
F(x₁, ..., xₙ) = ∫_{-∞}^{x₁} ... ∫_{-∞}^{xₙ} f(u₁, ..., uₙ) duₙ...du₁
```

**Properties:**
- f(x₁, ..., xₙ) ≥ 0 everywhere
- ∫_{-∞}^{∞} ... ∫_{-∞}^{∞} f(x₁, ..., xₙ) dx₁...dxₙ = 1 (total probability)
- P(X ∈ A) = ∫_A f(x) dx (probability as volume under density surface)

### Detailed Example: Triangular Region PDF

**Specification:**
```
f(x, y) = 2   for 0 < x < y < 1
        = 0   elsewhere
```

**Geometric Interpretation:** The support is the upper-triangle of the unit square where y > x.

```
Y
1 |      /|
  |     / |  Region: 0 < x < y < 1
  |    /  |  (Triangle above diagonal)
  |   /   |
  |  /    |
  | /     |
  |/______|
  0        1    X
```

**Verification of Normalization:**
```
∫∫ f(x,y) dx dy = ∫₀¹ ∫₀ʸ 2 dx dy
                = ∫₀¹ [2x]₀ʸ dy
                = ∫₀¹ 2y dy
                = [y²]₀¹
                = 1  ✓
```

**Probability Calculation:** Find P(X < 0.3, Y > 0.5)

```
Region: 0 < x < 0.3 and 0.5 < y < 1, with constraint x < y

Since x < 0.3 and y > 0.5, the constraint x < y is automatically satisfied.

P = ∫_{0.5}^{1} ∫_{0}^{0.3} 2 dx dy
  = ∫_{0.5}^{1} 0.6 dy
  = 0.6 × 0.5
  = 0.3
```

---

## 🔷 CONCEPT 4: Marginal Distributions

### Explanation
The **marginal distribution** describes the probability distribution of a subset of variables, ignoring the others. Obtained by "summing out" (discrete) or "integrating out" (continuous) the remaining variables.

**Discrete:**
```
P(Xₖ = xₖ) = Σ_{all other indices} p(i₁, ..., iₖ, ..., iₙ)
```

**Continuous:**
```
fₖ(xₖ) = ∫_{-∞}^{∞} ... ∫_{-∞}^{∞} f(x₁, ..., xₙ) dx₁...dxₖ₋₁ dxₖ₊₁...dxₙ
```

### Detailed Example 1: Discrete (Coin Toss)

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

### Detailed Example 2: Continuous (Triangular PDF)

**Marginal PDF of X:**
```
f₁(x) = ∫_{x}^{1} 2 dy = 2(1-x)   for 0 < x < 1
      = 0                         elsewhere
```

**Check:**
```
∫₀¹ 2(1-x) dx = [2x - x²]₀¹ = 2 - 1 = 1 ✓
```

**Marginal PDF of Y:**
```
f₂(y) = ∫_{0}^{y} 2 dx = 2y   for 0 < y < 1
      = 0                     elsewhere
```

**Check:**
```
∫₀¹ 2y dy = [y²]₀¹ = 1 ✓
```

**Shape Interpretation:**
- f₁(x) = 2(1-x): Linear decrease from 2 (at x=0) to 0 (at x=1) — X tends to be small
- f₂(y) = 2y: Linear increase from 0 (at y=0) to 2 (at y=1) — Y tends to be large
- This makes sense given the constraint 0 < x < y < 1 (X is "below" Y)

---

## 🔷 CONCEPT 5: Conditional Distributions & Conditional Expectation

### Explanation
The **conditional distribution** describes the behavior of some variables given that other variables take specific values.

**Conditional PMF (Discrete):**
```
P(X = x | Y = y) = P(X = x, Y = y) / P(Y = y)   if P(Y=y) > 0
```

**Conditional PDF (Continuous):**
```
f_{X|Y}(x|y) = f(x,y) / f_Y(y)   if f_Y(y) > 0
```

**Conditional Expectation:**
```
E[X | Y = y] = ∫ x · f_{X|Y}(x|y) dx   (continuous)
             = Σ x · P(X=x | Y=y)     (discrete)
```

**Key Properties:**
1. **Law of Total Expectation:** E[E[X|Y]] = E[X]
2. **Linearity:** E[aX + bZ | Y] = aE[X|Y] + bE[Z|Y]
3. **Tower Property:** E[E[X|Y,Z] | Y] = E[X|Y]
4. **Independence:** If X ⊥ Y, then E[X|Y] = E[X] (constant)

### Detailed Example 1: Discrete (Two Coin Flips)

**Scenario:** Flip a coin twice. X = total heads, Y = result of first flip (1=Head, 0=Tail).

**Given Y=1 (first is Head):**
Possible outcomes: HT (X=1), HH (X=2)
```
E[X|Y=1] = (1 + 2)/2 = 1.5
```

**Given Y=0 (first is Tail):**
Possible outcomes: TT (X=0), TH (X=1)
```
E[X|Y=0] = (0 + 1)/2 = 0.5
```

**Law of Total Expectation Verification:**
```
E[X] = E[X|Y=1]·P(Y=1) + E[X|Y=0]·P(Y=0)
     = 1.5 × 0.5 + 0.5 × 0.5
     = 0.75 + 0.25
     = 1.0  ✓
```
(Actual E[X] for 2 fair coins = 1)

### Detailed Example 2: Continuous (Triangular Region)

**Given:** f(x,y) = 2 for 0 < x < y < 1

**Step 1:** Find marginal f_Y(y) = 2y (from Concept 4)

**Step 2:** Find conditional PDF
```
f_{X|Y}(x|y) = f(x,y) / f_Y(y) = 2 / (2y) = 1/y   for 0 < x < y
```

**Interpretation:** Given Y=y, X is **Uniform(0, y)**!

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
E[X] = E[Y/2] = (1/2)E[Y]
E[Y] = ∫₀¹ y · 2y dy = 2/3
Therefore: E[X] = (1/2)(2/3) = 1/3  ✓
```

**Verification via marginal:** E[X] = ∫₀¹ x · 2(1-x) dx = 2[1/2 - 1/3] = 1/3 ✓

---

# PART 2: BIVARIATE & MULTIVARIATE NORMAL DISTRIBUTIONS

---

## 🔷 CONCEPT 6: Bivariate Normal Distribution

### Explanation
The **bivariate normal** distribution models two jointly normal random variables with linear dependence. It is the foundation of multivariate statistical analysis.

**PDF:**
```
f(x,y) = 1/(2πσ_X σ_Y √(1−ρ²)) · exp{−Q(x,y)/[2(1−ρ²)]}
```

where the **quadratic form** is:
```
Q(x,y) = [(x−μ_X)/σ_X]² − 2ρ[(x−μ_X)/σ_X][(y−μ_Y)/σ_Y] + [(y−μ_Y)/σ_Y]²
```

**Five Parameters:**
| Parameter | Symbol | Meaning |
|-----------|--------|---------|
| Mean of X | μ_X | Center location in x-direction |
| Mean of Y | μ_Y | Center location in y-direction |
| Std dev X | σ_X | Spread in x-direction |
| Std dev Y | σ_Y | Spread in y-direction |
| Correlation | ρ | Linear dependence (−1 ≤ ρ ≤ 1) |

**Covariance Matrix:**
```
Σ = [ σ_X²      ρσ_Xσ_Y  ]
    [ ρσ_Xσ_Y   σ_Y²     ]
```

**Key Properties:**
1. **Marginals are normal:** X ~ N(μ_X, σ_X²), Y ~ N(μ_Y, σ_Y²)
2. **Conditional is normal:** X|Y=y ~ N(μ_X + ρ(σ_X/σ_Y)(y−μ_Y), σ_X²(1−ρ²))
3. **Linear conditional mean:** E[X|Y] is linear in Y
4. **ρ = 0 ⇔ Independence** (unique to normal distributions!)
5. **Variance reduction:** Knowing Y reduces variance of X by factor (1−ρ²)

### Detailed Example: Height and Weight

**Parameters for adult males:**
- μ_X = 170 cm (height), σ_X = 10 cm
- μ_Y = 70 kg (weight), σ_Y = 15 kg
- ρ = 0.7 (positive correlation)

**Prediction:** Person weighs Y = 85 kg (1 std dev above mean). Predict height:

```
E[X|Y=85] = μ_X + ρ(σ_X/σ_Y)(Y−μ_Y)
          = 170 + 0.7×(10/15)×(85−70)
          = 170 + 0.7×0.667×15
          = 170 + 7
          = 177 cm
```

**Uncertainty reduction:**
- Marginal variance: σ_X² = 100
- Conditional variance: σ_X²(1−ρ²) = 100(1−0.49) = 51
- Standard deviation: √51 ≈ 7.1 cm (vs 10 cm marginally)

**Without knowing weight:** Best guess 170±10 cm
**Knowing weight=85kg:** Best guess 177±7.1 cm (more precise!)

---

## 🔷 CONCEPT 7: Constant Density Contours (Ellipses)

### Explanation
For a fixed value c, the set {(x,y): f(x,y) = c} forms an **ellipse** centered at (μ_X, μ_Y).

**Ellipse Geometry:**
- **Center:** (μ_X, μ_Y)
- **Axes directions:** Eigenvectors of Σ
- **Axes lengths:** Proportional to √λ₁, √λ₂ (square roots of eigenvalues of Σ)
- **Tilt angle:** tan(2θ) = 2ρσ_Xσ_Y / (σ_X² − σ_Y²)

**Special Cases:**

| Correlation | Shape | Interpretation |
|-------------|-------|----------------|
| ρ = 0 | Axis-aligned (circle if σ_X=σ_Y) | No linear relationship |
| ρ > 0 | Tilted up-right | Y increases with X |
| ρ < 0 | Tilted up-left | Y decreases as X increases |
| ρ = ±1 | Degenerate ellipse (line) | Perfect linear dependence |

### Detailed Example: Visual Comparison

**Case 1: ρ = 0.8, σ_X = σ_Y**
```
    Y
    |    ╱──╲
    |   ╱    ╲   Major axis: y = x (45° line)
    |  ╱  ●   ╲  Points cluster along diagonal
    | ╱        ╲
    |╱__________╲
    +----------→ X
```

**Case 2: ρ = −0.8, σ_X = σ_Y**
```
    Y
    |╲          ╱
    | ╲        ╱   Major axis: y = −x (−45° line)
    |  ╲  ●   ╱    Negative correlation
    |   ╲    ╱
    |    ╲──╱
    +----------→ X
```

**Case 3: ρ = 0, σ_X = 2σ_Y (stretched horizontally)**
```
    Y
    |   ◯◯◯◯◯
    |  ◯     ◯   Wider in X direction
    | ◯   ●   ◯
    |  ◯     ◯
    |   ◯◯◯◯◯
    +----------→ X
```

---

## 🔷 CONCEPT 8: Multivariate Normal Distribution Nₚ(μ, Σ)

### Explanation
Generalizes bivariate normal to p dimensions. A random vector **X** = (X₁, ..., Xₚ)ᵀ follows **Nₚ(μ, Σ)** if every linear combination aᵀX follows a univariate normal distribution.

**PDF (when Σ is positive definite):**
```
f(x) = (2π)^(−p/2) |Σ|^(−1/2) exp{−½(x−μ)ᵀΣ⁻¹(x−μ)}
```

**Parameters:**
- **μ:** p×1 mean vector
- **Σ:** p×p positive definite covariance matrix
- **|Σ|:** Determinant of Σ (measures generalized variance)

**Connection to 1D:** When p=1, this reduces to univariate normal with (x−μ)²/σ² in the exponent. The term (x−μ)ᵀΣ⁻¹(x−μ) is the **Mahalanobis distance** squared.

### Detailed Example: 4-Variate Normal with Independence

**Given PDF:**
```
f(x) = (1/48π²) exp{−½[(x₁−2)²/6 + (x₂+1)²/3 + x₃²/4 + (x₄−4)²/2]}
```

**Identification:**
- No cross-terms (xᵢxⱼ) → independent components
- Diagonal covariance matrix: Σ = diag(6, 3, 4, 2)
- Mean vector: μ = (2, −1, 0, 4)ᵀ

**Verification of constant:**
```
(2π)^(4/2) = (2π)² = 4π²
|Σ|^(1/2) = √(6×3×4×2) = √144 = 12
Constant = 1/(4π² × 12) = 1/(48π²)  ✓
```

**Independent Components:**
- X₁ ~ N(2, 6)
- X₂ ~ N(−1, 3)
- X₃ ~ N(0, 4)
- X₄ ~ N(4, 2)

---

## 🔷 CONCEPT 9: Key Properties of Multivariate Normal

### Explanation

**Property 1: Linear Combinations**
```
If X ~ Nₚ(μ, Σ), then AX ~ N_q(Aμ, AΣAᵀ)
```
for any q×p matrix A. Any linear combination of components is univariate normal.

**Property 2: Marginal Normality**
Any subset of components is multivariate normal. Partition X = [X₁, X₂]ᵀ, then:
```
X₁ ~ N_q(μ₁, Σ₁₁)
```

**Property 3: Zero Covariance ⇔ Independence**
Subsets X₁ and X₂ are independent if and only if Σ₁₂ = 0 (off-diagonal block is zero matrix). This is **unique** to the multivariate normal family!

**Property 4: Conditional Distributions**
The conditional distribution of X₁ given X₂ = x₂ is:
```
X₁|X₂=x₂ ~ N_q(μ₁ + Σ₁₂Σ₂₂⁻¹(x₂−μ₂), Σ₁₁ − Σ₁₂Σ₂₂⁻¹Σ₂₁)
```

**Property 5: Quadratic Form**
```
(X−μ)ᵀΣ⁻¹(X−μ) ~ χ²ₚ
```
(Chi-squared with p degrees of freedom). Defines confidence ellipsoids.

### Detailed Example: Independence Check

**Given:** X = (X₁, X₂, X₃)ᵀ ~ N₃(μ, Σ) with:
```
Σ = [ 4  1  0 ]
    [ 1  3  0 ]
    [ 0  0  2 ]
```

**Partition:** X₁ = (X₁, X₂)ᵀ, X₂ = X₃

**Check Σ₁₂:**
```
Σ₁₂ = [ 0 ]
      [ 0 ]  (2×1 zero vector)
```

**Conclusion:** Since Σ₁₂ = 0, (X₁, X₂) and X₃ are **independent**.

**But:** X₁ and X₂ have σ₁₂ = 1 ≠ 0, so they are **not independent**.

**Practical Implication:** We can model X₃ separately from (X₁, X₂), but must model X₁ and X₂ jointly.

**Counterexample (Non-normal):**
Let X ~ N(0,1), W ~ Bernoulli(0.5), Y = (2W−1)X. Both X and Y are marginally N(0,1), Cov(X,Y)=0, but (X,Y) is NOT bivariate normal (concentrated on two lines y=±x). This shows that **marginals being normal + zero covariance does not imply independence** unless joint normality holds.

---

# PART 3: SAMPLING DISTRIBUTIONS & INFERENCE

---

## 🔷 CONCEPT 10: Sample Mean Vector and Covariance Matrix

### Explanation
For multivariate data X₁, ..., Xₙ (each a p×1 vector), the sample statistics estimate population parameters.

**Sample Mean Vector:**
```
X̄ = (1/n) Σᵢ₌₁ⁿ Xᵢ = (1/n) Xᵀ**1**
```
where X is n×p data matrix, **1** is n×1 vector of ones.

**Centered Data:**
```
X̃ = X − **1**X̄ᵀ
```

**Sample Covariance Matrix:**
```
S = (1/(n−1)) X̃ᵀX̃ = (1/(n−1)) Σᵢ₌₁ⁿ (Xᵢ − X̄)(Xᵢ − X̄)ᵀ
```

**Entry (j,k):**
```
sⱼₖ = (1/(n−1)) Σᵢ₌₁ⁿ (xᵢⱼ − X̄ⱼ)(xᵢₖ − X̄ₖ)
```

**Properties:**
- E[X̄] = μ (unbiased)
- Cov(X̄) = (1/n)Σ (variance decreases with n)
- E[S] = Σ (unbiased)
- MLE of Σ is (n−1)S/n (biased, divides by n not n−1)

### Detailed Example: 2D Calculation

**Data (n=4 students):**
| Student | Height (X₁) | Weight (X₂) |
|---------|-------------|-------------|
| 1 | 160 | 55 |
| 2 | 170 | 65 |
| 3 | 165 | 60 |
| 4 | 180 | 75 |

**Sample Mean:**
```
X̄₁ = (160+170+165+180)/4 = 168.75
X̄₂ = (55+65+60+75)/4 = 63.75
X̄ = [168.75, 63.75]ᵀ
```

**Centered Data:**
```
[ −8.75  −8.75 ]
[  1.25   1.25 ]
[ −3.75  −3.75 ]
[ 11.25  11.25 ]
```

**Sample Covariance:**
```
s₁₁ = (76.56 + 1.56 + 14.06 + 126.56)/3 = 218.75/3 = 72.92
s₂₂ = (76.56 + 1.56 + 14.06 + 126.56)/3 = 72.92
s₁₂ = (76.56 + 1.56 + 14.06 + 126.56)/3 = 72.92

S = [ 72.92  72.92 ]
    [ 72.92  72.92 ]
```

**Interpretation:** Perfect sample correlation (ρ̂ = 1) because weight = height − 105 in this constructed example.

---

## 🔷 CONCEPT 11: Wishart Distribution & Sampling Properties

### Explanation
When X₁, ..., Xₙ are i.i.d. Nₚ(μ, Σ):

**Sampling Distributions:**
1. **X̄ ~ Nₚ(μ, (1/n)Σ)** exactly
2. **(n−1)S ~ Wishartₚ(n−1, Σ)** — the multivariate chi-squared
3. **X̄ and S are independent** (analogous to X̄ and s² independent in univariate normal)

**Wishart Distribution:**
The distribution of Σᵢ₌₁ⁿ ZᵢZᵢᵀ where Zᵢ ~ Nₚ(0, Σ) i.i.d. When p=1, this reduces to σ²χ²ₙ₋₁.

**Quadratic Form:**
```
n(X̄ − μ)ᵀΣ⁻¹(X̄ − μ) ~ χ²ₚ
```

**Confidence Ellipsoid:**
The set {μ : n(X̄ − μ)ᵀS⁻¹(X̄ − μ) ≤ χ²ₚ,₁₋α} contains the true mean with probability 1−α.

---

## 🔷 CONCEPT 12: Maximum Likelihood Estimation (MLE)

### Explanation
For X₁, ..., Xₙ ~ Nₚ(μ, Σ) i.i.d., find parameters maximizing likelihood.

**Log-Likelihood:**
```
ln L(μ, Σ) = −(np/2)ln(2π) − (n/2)ln|Σ| − ½Σᵢ₌₁ⁿ(Xᵢ−μ)ᵀΣ⁻¹(Xᵢ−μ)
```

**Using trace trick:**
```
Σ(Xᵢ−μ)ᵀΣ⁻¹(Xᵢ−μ) = tr[Σ⁻¹Σ(Xᵢ−X̄)(Xᵢ−X̄)ᵀ] + n(X̄−μ)ᵀΣ⁻¹(X̄−μ)
```

**MLE Solutions:**
- **μ̂ = X̄** (sample mean)
- **Σ̂ = (1/n)Σ(Xᵢ−X̄)(Xᵢ−X̄)ᵀ = (n−1)S/n**

**Comparison:**
| Estimator | Formula | Bias | Use |
|-----------|---------|------|-----|
| **S (unbiased)** | (1/(n−1))Σ(Xᵢ−X̄)(Xᵢ−X̄)ᵀ | E[S] = Σ | Hypothesis testing, confidence intervals |
| **Σ̂ (MLE)** | (1/n)Σ(Xᵢ−X̄)(Xᵢ−X̄)ᵀ | E[Σ̂] = (n−1)/n Σ | Large samples, likelihood-based methods |

---

## 🔷 CONCEPT 13: Hotelling's T² Test

### Explanation
The multivariate generalization of the one-sample t-test for testing:
```
H₀: μ = μ₀ vs H₁: μ ≠ μ₀
```

**Test Statistic:**
```
T² = n(X̄ − μ₀)ᵀ S⁻¹ (X̄ − μ₀)
```

**Distribution under H₀:**
```
T² ~ [(n−1)p/(n−p)] · F_{p, n−p}
```

**Decision Rule:** Reject H₀ at level α if:
```
T² > [(n−1)p/(n−p)] · F_{p, n−p}(α)
```

**Intuition:** Measures squared Mahalanobis distance between sample mean and hypothesized mean, scaled by sample covariance. Large T² indicates significant deviation.

### Detailed Example: Testing Mean Vector

**Scenario:** Test if average exam scores in Math, Physics, Chemistry equal (70, 65, 75).

**Data (n=50 students, p=3):**
- Sample mean: X̄ = (72, 68, 73)ᵀ
- Sample covariance: S = [10  5  3; 5  12  4; 3  4  8]
- Hypothesized: μ₀ = (70, 65, 75)ᵀ

**Calculate:**
```
X̄ − μ₀ = [2, 3, −2]ᵀ

S⁻¹ = (compute inverse or use software)

T² = 50 × [2,3,−2] S⁻¹ [2,3,−2]ᵀ
    = 50 × (computed quadratic form)
    ≈ 50 × 0.85 = 42.5
```

**Critical Value:**
```
p=3, n=50, α=0.05
[(49×3)/47] × F_{3,47}(0.05) ≈ 3.13 × 2.80 ≈ 8.76
```

**Decision:** 42.5 > 8.76 → **Reject H₀**

**Conclusion:** The mean exam score vector significantly differs from (70, 65, 75). Students perform differently than hypothesized across subjects.

---

## 🔷 CONCEPT 14: Q-Q Plot for Assessing Normality

### Explanation
A **Quantile-Quantile (Q-Q) plot** compares empirical quantiles of data against theoretical quantiles of a reference distribution (usually normal) to assess distributional fit.

**Construction:**
1. Sort data: x₍₁₎ ≤ x₍₂₎ ≤ ... ≤ x₍ₙ₎
2. Compute probability levels: p₍ⱼ₎ = (j − ½)/n  (or j/(n+1))
3. Find theoretical quantiles: q₍ⱼ₎ = Φ⁻¹(p₍ⱼ₎) where Φ is standard normal CDF
4. Plot points (q₍ⱼ₎, x₍ⱼ₎)

**Interpretation:**
| Pattern | Diagnosis |
|---------|-----------|
| Points on straight line | Data approximately normal |
| S-curve (curved up then down) | Heavy tails (more extreme values than normal) |
| Inverted S-curve | Light tails (fewer extreme values than normal) |
| Bow shape (curved) | Skewness (asymmetric distribution) |
| Points deviating at ends | Outliers or non-normal tail behavior |

### Detailed Example: Small Sample (n=10)

**Data (sorted):** −1.00, −0.10, 0.25, 0.42, 0.62, 0.81, 1.05, 1.30, 1.71, 2.30

**Q-Q Plot Construction:**

| j | x₍ⱼ₎ | p₍ⱼ₎=(j−0.5)/10 | q₍ⱼ₎ (z-score) |
|---|------|------------------|----------------|
| 1 | −1.00 | 0.05 | −1.645 |
| 2 | −0.10 | 0.15 | −1.036 |
| 3 | 0.25 | 0.25 | −0.674 |
| 4 | 0.42 | 0.35 | −0.385 |
| 5 | 0.62 | 0.45 | −0.126 |
| 6 | 0.81 | 0.55 | +0.126 |
| 7 | 1.05 | 0.65 | +0.385 |
| 8 | 1.30 | 0.75 | +0.674 |
| 9 | 1.71 | 0.85 | +1.036 |
| 10 | 2.30 | 0.95 | +1.645 |

**Plot Analysis:**
- Points roughly follow line y = x (or slight positive intercept)
- No systematic curvature
- End points don't deviate excessively

**Conclusion:** Data consistent with normal distribution (though n=10 is small for definitive assessment).

**Multivariate Extension:** Check Mahalanobis distances dᵢ² = (Xᵢ−X̄)ᵀS⁻¹(Xᵢ−X̄) against χ²ₚ quantiles. If multivariate normal, these should follow χ²ₚ.

---

## 📌 Master Summary Table

| Concept | Key Formula/Result | Interpretation |
|---------|-------------------|----------------|
| **Joint CDF** | F(x) = P(X≤x) | Probability in lower-left orthant |
| **Joint PMF** | p(x) = P(X=x) | Probability mass at discrete point |
| **Joint PDF** | f(x) = ∂ⁿF/∂x₁...∂xₙ | Density, integrates to probability |
| **Marginal** | Integrate/sum over others | Distribution of subset |
| **Conditional** | f(x\|y) = f(x,y)/f(y) | Distribution given information |
| **Cond. Expectation** | E[X\|Y] | Best predictor of X given Y |
| **Law Total Exp** | E[E[X\|Y]] = E[X] | Tower property |
| **Bivariate Normal** | f ∝ exp(−Q/2(1−ρ²)) | Elliptical contours |
| **Conditional Normal** | X\|Y ~ N(μ_X+ρ(σ_X/σ_Y)(Y−μ_Y), σ_X²(1−ρ²)) | Linear mean, reduced variance |
| **Independence** | ρ=0 ⟺ independent | Unique to normal |
| **Multivariate Normal** | X ~ Nₚ(μ, Σ) | Linear combos are normal |
| **Mahalanobis** | (x−μ)ᵀΣ⁻¹(x−μ) | Distance accounting for covariance |
| **Sample Mean** | X̄ = (1/n)ΣXᵢ | Unbiased for μ |
| **Sample Covariance** | S = (1/(n−1))Σ(Xᵢ−X̄)(Xᵢ−X̄)ᵀ | Unbiased for Σ |
| **Wishart** | (n−1)S ~ Wishartₚ(n−1, Σ) | Sampling distribution |
| **Hotelling T²** | n(X̄−μ₀)ᵀS⁻¹(X̄−μ₀) | Multivariate distance test |
| **Q-Q Plot** | Plot (Φ⁻¹(pⱼ), x₍ⱼ₎) | Visual normality check |

---

## 🔗 The Unifying Thread: The Covariance Matrix Σ

Every multivariate concept revolves around **Σ**:

| Role | Manifestation |
|------|---------------|
| **Shape** | Controls elliptical contours (eigenvectors=axes, eigenvalues=spreads) |
| **Dependence** | Off-diagonal entries encode correlations |
| **Independence** | Zero off-diagonal blocks ⟺ independent subvectors |
| **Precision** | Cov(X̄) = Σ/n — determines uncertainty |
| **Sampling** | (n−1)S follows Wishart — randomness of sample covariance |
| **Inference** | Hotelling's T² uses S⁻¹ — inverse covariance weights distances |
| **Geometry** | Σ⁻¹ defines Mahalanobis metric |

**Understanding Σ** — its spectral decomposition (PCA), its role in conditional distributions, and its estimation properties — is the foundation of multivariate statistical analysis.
```