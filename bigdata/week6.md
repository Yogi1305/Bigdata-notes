
# 📘 Complete Guide: Linear Modelling & Regression Analysis (Week 6)

---

## 🔷 CONCEPT 1: What is Regression?

### Explanation
Regression analysis is a statistical methodology used to establish a relationship between a **dependent variable** (response/outcome) and one or more **independent variables** (predictors/features). It quantifies how changes in independent variables affect the dependent variable, allowing for prediction and inference.

**Key Purposes:**
1. **Description:** Understand how variables relate to each other
2. **Prediction:** Forecast future values of the dependent variable
3. **Control:** Adjust independent variables to achieve desired outcomes
4. **Inference:** Test hypotheses about relationships between variables

### Detailed Example: Educational Performance

**Scenario:** A university wants to understand factors affecting student performance.

**Variables:**
- **Dependent Variable (Y):** Final Exam Score (0-100 scale)
- **Independent Variable (X):** Hours Studied per Week

**Observed Data (n=10 students):**
| Student | Hours Studied (X) | Exam Score (Y) |
|---------|-------------------|----------------|
| 1 | 2 | 45 |
| 2 | 4 | 55 |
| 3 | 5 | 60 |
| 4 | 6 | 65 |
| 5 | 8 | 72 |
| 6 | 10 | 78 |
| 7 | 12 | 85 |
| 8 | 14 | 88 |
| 9 | 15 | 92 |
| 10 | 18 | 95 |

**Visual Pattern:** As hours studied increases, exam scores tend to increase linearly. Regression helps us find the "best fit" line through this data to predict scores for any study time.

**Regression Question:** "For every additional hour studied, how much does the exam score increase on average?"

---

## 🔷 CONCEPT 2: The Simple Linear Regression Model

### Explanation
The simple linear regression model assumes a linear relationship between X and Y with random error:

**Mathematical Form:**

Y = a + bX + ε


**Component Breakdown:**
- **Y:** Dependent/Response variable (what we measure)
- **X:** Independent/Explanatory variable (what we control or observe)
- **a:** Intercept parameter (expected value of Y when X=0)
- **b:** Slope parameter (change in Y for a 1-unit increase in X)
- **ε:** Error term (random disturbance, assumed ε ~ N(0, σ²))

**Assumptions:**
1. **Linearity:** The true relationship is linear
2. **Independence:** Errors are independent across observations
3. **Homoscedasticity:** Constant variance σ² (homogeneity of variance)
4. **Normality:** Errors are normally distributed (for inference)
5. **Exogeneity:** E(ε|X) = 0 (errors have mean zero conditional on X)

### Detailed Example: House Price Prediction

**Scenario:** Real estate pricing model.

**Model Specification:**

Price (₹ lakhs) = a + b × Area (sq ft) + ε


**Interpretation of Parameters:**
- **a = 50:** Base price (₹50 lakhs) for a house with 0 sq ft (theoretical intercept, represents land value + fixed costs)
- **b = 0.02:** Each additional square foot adds ₹20,000 to the price
- **σ² = 25:** Variance of prices around the line (standard deviation ₹5 lakhs)

**Prediction Examples:**
- 1000 sq ft house: Expected Price = 50 + 0.02(1000) = ₹70 lakhs
- 2000 sq ft house: Expected Price = 50 + 0.02(2000) = ₹90 lakhs
- Actual observed price might be ₹88 lakhs or ₹95 lakhs due to ε (other factors like location, age, amenities)

**Error Realization:** For a 1500 sq ft house sold at ₹75 lakhs:
- Predicted: 50 + 0.02(1500) = ₹80 lakhs
- Error (ε): 75 - 80 = -₹5 lakhs (sold below trend line)

---

## 🔷 CONCEPT 3: Least Squares Estimation (OLS)

### Explanation
**Ordinary Least Squares (OLS)** finds the line that minimizes the sum of squared vertical distances (residuals) between observed Y values and predicted Ŷ values.

**Objective Function:**

Minimize S(a,b) = Σᵢ₌₁ⁿ (Yᵢ - Ŷᵢ)² = Σᵢ₌₁ⁿ (Yᵢ - a - bXᵢ)²


**Derivation (Calculus Approach):**
Taking partial derivatives and setting to zero:

∂S/∂a = -2Σ(Yᵢ - a - bXᵢ) = 0
∂S/∂b = -2ΣXᵢ(Yᵢ - a - bXᵢ) = 0


**Closed-Form Solutions:**

b̂ = sXY / sXX = Σ(Xᵢ - X̄)(Yᵢ - Ȳ) / Σ(Xᵢ - X̄)²
â = Ȳ - b̂X̄


Where:
- **sXY:** Sample covariance between X and Y (sum of cross-products)
- **sXX:** Sample variance of X (sum of squared deviations)
- **X̄, Ȳ:** Sample means

### Detailed Worked Example: Complete Calculation

**Dataset (n=5):**
| i | Xᵢ | Yᵢ | Xᵢ - X̄ | Yᵢ - Ȳ | (Xᵢ-X̄)(Yᵢ-Ȳ) | (Xᵢ-X̄)² |
|---|----|----|---------|---------|---------------|----------|
| 1 | 1 | 2 | -2 | -2 | 4 | 4 |
| 2 | 2 | 3 | -1 | -1 | 1 | 1 |
| 3 | 3 | 5 | 0 | 1 | 0 | 0 |
| 4 | 4 | 4 | 1 | 0 | 0 | 1 |
| 5 | 5 | 6 | 2 | 2 | 4 | 4 |
| **Sum** | 15 | 20 | 0 | 0 | **9** | **10** |

**Calculations:**

X̄ = 15/5 = 3
Ȳ = 20/5 = 4

sXY = Σ(Xᵢ-X̄)(Yᵢ-Ȳ) = 9
sXX = Σ(Xᵢ-X̄)² = 10

b̂ = 9/10 = 0.9
â = 4 - (0.9)(3) = 4 - 2.7 = 1.3


**Fitted Regression Line:**

Ŷ = 1.3 + 0.9X


**Predictions & Residuals:**
| X | Y (Observed) | Ŷ (Predicted) | Residual (e=Y-Ŷ) | Residual² |
|---|--------------|---------------|------------------|-----------|
| 1 | 2 | 2.2 | -0.2 | 0.04 |
| 2 | 3 | 3.1 | -0.1 | 0.01 |
| 3 | 5 | 4.0 | 1.0 | 1.00 |
| 4 | 4 | 4.9 | -0.9 | 0.81 |
| 5 | 6 | 5.8 | 0.2 | 0.04 |
| **Sum** | | | **0** | **1.90** |

**Verification:** Sum of residuals = 0 (always true for OLS with intercept).

**Visualization Concept:**
- Scatter plot shows points (1,2), (2,3), (3,5), (4,4), (5,6)
- Line Ŷ = 1.3 + 0.9X passes through the cloud of points
- Red vertical dashed lines represent residuals (gaps between points and line)
- OLS makes the sum of squared lengths of these dashed lines as small as possible

---

## 🔷 CONCEPT 4: Properties of OLS Estimators

### 4.1 Unbiasedness
**Property:** E(â) = a and E(b̂) = b

**Explanation:** On average across many samples, the estimators hit the true parameter values. The sampling distribution of b̂ is centered at the true slope b.

**Intuition:** If you repeated the experiment 1000 times with different random samples and averaged all 1000 b̂ values, you'd get approximately b.

### 4.2 Variances of Estimators
**Formulas:**

Var(b̂) = σ² / sXX
Var(â) = σ²(1/n + X̄²/sXX)


**Interpretation:**
- **Precision increases with X-spread:** Larger sXX (X values more spread out) → Smaller Var(b̂) → More precise slope estimate
- **Precision increases with sample size:** As n increases, variance decreases
- **Intercept precision:** Depends on both n and how far X̄ is from zero

**Example:** Comparing two experimental designs for studying temperature (X) vs reaction yield (Y):

**Design A (Narrow):** X = {20, 21, 22, 23, 24}°C
- sXX = 10
- Var(b̂) = σ²/10

**Design B (Wide):** X = {10, 15, 20, 25, 30}°C  
- sXX = 250
- Var(b̂) = σ²/250 (25× smaller!)

**Conclusion:** Design B provides much more precise slope estimates. Always maximize the range of X values when possible.

### 4.3 Covariance between â and b̂
**Formula:**

Cov(â, b̂) = -X̄σ² / sXX


**Interpretation:** The estimators are negatively correlated when X̄ > 0. If you overestimate the slope, you tend to underestimate the intercept to keep the line passing through (X̄, Ȳ).

### 4.4 Residual Properties (Algebraic Identities)
The OLS residuals eᵢ = Yᵢ - Ŷᵢ always satisfy:

1. **Sum to zero:** Σeᵢ = 0
   - Result of including intercept in model
   
2. **Orthogonal to X:** ΣXᵢeᵢ = 0
   - Result of first-order condition for b̂
   
3. **Orthogonal to fitted values:** ΣŶᵢeᵢ = 0
   
4. **Line passes through centroid:** The fitted line always passes through (X̄, Ȳ)
   - Since Ŷ(X̄) = â + b̂X̄ = (Ȳ - b̂X̄) + b̂X̄ = Ȳ

**Proof of Σeᵢ = 0:**

Σeᵢ = Σ(Yᵢ - â - b̂Xᵢ) = ΣYᵢ - nâ - b̂ΣXᵢ = nȲ - n(Ȳ - b̂X̄) - b̂nX̄ = nȲ - nȲ + nb̂X̄ - nb̂X̄ = 0


---

## 🔷 CONCEPT 5: Residual Sum of Squares (SSres) and Error Variance

### Explanation
**SSres (Sum of Squared Residuals)** measures the total unexplained variation after fitting the regression line.

**Computational Formula:**

SSres = Σ(Yᵢ - Ŷᵢ)² = sYY - b̂·sXY = sYY - (sXY)²/sXX


Where sYY = Σ(Yᵢ - Ȳ)² (total sum of squares for Y).

**Estimate of Error Variance (σ²):**

s² = SSres / (n - 2)


**Why (n-2)?** We lose 2 degrees of freedom because we estimated 2 parameters (â and b̂) from the data.

**Standard Error of Regression (s):**

s = √s² = √[SSres/(n-2)]

This estimates the standard deviation of the error term ε, representing typical prediction error magnitude.

### Detailed Example: Calculating s²

**From previous example:**
- SSres = 1.90 (calculated from residual table)
- n = 5
- n - 2 = 3


s² = 1.90 / 3 = 0.6333
s = √0.6333 = 0.796


**Interpretation:** Typical prediction error is about 0.8 units. When we predict Y using this regression, we expect to be off by roughly ±0.8 on average.

**Standard Errors of Coefficients:**

SE(b̂) = √(s²/sXX) = √(0.6333/10) = √0.0633 = 0.252
SE(â) = √[s²(1/n + X̄²/sXX)] = √[0.6333(0.2 + 9/10)] = √[0.6333(1.1)] = √0.6966 = 0.835


---

## 🔷 CONCEPT 6: BLUE and the Gauss-Markov Theorem

### Explanation
**BLUE = Best Linear Unbiased Estimator**

**The Gauss-Markov Theorem states:** Under the classical assumptions (linearity, independence, homoscedasticity, exogeneity), the OLS estimators â and b̂ have the **smallest variance** among all **linear unbiased estimators** of a and b.

**Breakdown:**
- **B (Best):** Minimum variance (most precise)
- **L (Linear):** Estimators are linear functions of Y
- **U (Unbiased):** Expected value equals true parameter
- **E (Estimator):** Statistical estimator of population parameters

**Mathematical Proof Sketch:**
Consider any other linear unbiased estimator β̃ = CY where C is some matrix/vector.

We can decompose: C = (X⊤X)⁻¹X⊤ + D = A + D

For unbiasedness, we need DX = 0 (zero matrix).

Then:

Var(β̃) = Var(CY) = CVar(Y)C⊤ = σ²CC⊤
       = σ²(A+D)(A+D)⊤
       = σ²(AA⊤ + AD⊤ + DA⊤ + DD⊤)
       = σ²AA⊤ + σ²DD⊤  (since AX = I and DX = 0 implies AD⊤ = 0)
       = Var(β̂) + σ²DD⊤


Since DD⊤ is positive semi-definite, Var(β̃) ≥ Var(β̂).

**Implications:**
- You cannot find a better linear unbiased estimator than OLS
- Any other linear unbiased estimator has larger variance (wider confidence intervals)
- This justifies using OLS as the "gold standard" for linear regression

**Important Caveat:** "Best" among linear unbiased estimators. Nonlinear or biased estimators (like ridge regression) might have lower mean squared error in some cases.

---

## 🔷 CONCEPT 7: The Centered Model

### Explanation
**Centering** means subtracting the mean from X before regression:

X̃ᵢ = Xᵢ - X̄


**Centered Model Specification:**

Yᵢ = a* + bX̃ᵢ + εᵢ = a* + b(Xᵢ - X̄) + εᵢ


**Relationship to Original Parameters:**

a* = a + bX̄


When X = X̄ (centered zero), Y = a*, so **a* represents the expected Y at the mean of X** (often more interpretable than a, which is Y at X=0).

**Key Benefit:**
In the centered model, **Cov(â*, b̂) = 0** — the intercept and slope estimates are uncorrelated (statistically independent under normality).

**Proof of Zero Covariance:**

Cov(â*, b̂) = Cov(Ȳ, b̂) = 0  (since b̂ depends on X deviations and Ȳ is independent of X deviations in OLS)


### Detailed Example: Years of Experience

**Original Model:** Salary = a + b(Years) + ε
- Intercept a = salary at 0 years (meaningless for entry-level jobs requiring degrees)

**Centered Model:** Salary = a* + b(Years - 5) + ε  
(assuming mean experience in sample is 5 years)
- Intercept a* = salary at 5 years (mean experience) — much more interpretable!
- Slope b remains exactly the same (0.9 in our prior example)

**Calculation Verification:**
If original â = 1.3, b̂ = 0.9, X̄ = 3:

â* = 1.3 + 0.9(3) = 1.3 + 2.7 = 4.0 = Ȳ ✓


---

## 🔷 CONCEPT 8: Multiple Linear Regression (MLR) — Matrix Form

### Explanation
When we have k predictors (X₁, X₂, ..., Xₖ), we extend to Multiple Linear Regression using matrix notation for compactness and computation.

**Model:**

Y = Xβ + ε


**Matrix Dimensions:**
- **Y:** n×1 vector of responses
- **X:** n×(k+1) design matrix (first column all 1s for intercept, then k predictor columns)
- **β:** (k+1)×1 vector of coefficients [a, b₁, b₂, ..., bₖ]⊤
- **ε:** n×1 vector of errors ~ N(0, σ²Iₙ)

**OLS Solution (Normal Equations):**

β̂ = (X⊤X)⁻¹X⊤Y


**Fitted Values:**

Ŷ = Xβ̂ = HY

where H = X(X⊤X)⁻¹X⊤ is the "Hat Matrix" (projects Y onto column space of X).

### Detailed Worked Example: Matrix Calculation

**Data (n=3, simple case for illustration):**

X = [1, 1]
    [1, 2]
    [1, 3]

Y = [2]
    [3]
    [5]


**Step 1: Compute X⊤X**

X⊤X = [1 1 1] [1 1]   [3   6 ]
      [1 2 3] [1 2] = [6  14 ]
              [1 3]


**Step 2: Compute (X⊤X)⁻¹**

Determinant = (3)(14) - (6)(6) = 42 - 36 = 6

(X⊤X)⁻¹ = (1/6) [14  -6]
                 [-6   3]


**Step 3: Compute X⊤Y**

X⊤Y = [1 1 1][2]   [10]
      [1 2 3][3] = [23]
             [5]


**Step 4: Compute β̂ = (X⊤X)⁻¹X⊤Y**

β̂ = (1/6) [14  -6][10] = (1/6)[140-138] = (1/6)[2]  = [0.333]
          [-6   3][23]        [-60+69]        [9]    [1.500]


**Result:** β̂ = [0.333, 1.5]⊤
- Intercept â = 0.333
- Slope b̂ = 1.5

**Fitted Line:** Ŷ = 0.333 + 1.5X

**Verification:**
- X=1: Ŷ = 0.333 + 1.5 = 1.833 ≈ 2 (observed: 2, residual -0.167)
- X=2: Ŷ = 0.333 + 3 = 3.333 ≈ 3 (observed: 3, residual -0.333)
- X=3: Ŷ = 0.333 + 4.5 = 4.833 ≈ 5 (observed: 5, residual +0.167)

---

## 🔷 CONCEPT 9: Maximum Likelihood Estimation (MLE)

### Explanation
Under the assumption that errors are normally distributed (εᵢ ~ N(0, σ²)), we can derive the Maximum Likelihood Estimators (MLE). MLE finds the parameter values that make the observed data most probable.

**Likelihood Function:**

L(a, b, σ²) = ∏ᵢ₌₁ⁿ (1/√(2πσ²)) exp[-(Yᵢ-a-bXᵢ)²/(2σ²)]


**Log-Likelihood:**

ln L = -(n/2)ln(2π) - (n/2)ln(σ²) - (1/(2σ²))Σ(Yᵢ-a-bXᵢ)²


**Maximization:**
- With respect to **a** and **b:** Minimize Σ(Yᵢ-a-bXᵢ)² — exactly the OLS criterion!
- With respect to **σ²:** Take derivative and set to zero

**MLE Results:**

â_MLE = OLS intercept
b̂_MLE = OLS slope
σ̂²_MLE = (1/n)Σ(Yᵢ-Ŷᵢ)² = SSres/n


**Key Insight:** Under normality, OLS = MLE for the regression coefficients. However, the MLE for σ² is biased (divides by n instead of n-2).

**Unbiased Correction:**

s² = SSres/(n-2)  [Unbiased, preferred for inference]
σ̂²_MLE = SSres/n  [Biased, smaller by factor (n-2)/n]


---

## 🔷 CONCEPT 10: Hypothesis Testing for the Slope (b)

### Explanation
We often want to test whether X has a significant linear effect on Y:

H₀: b = 0 (X has no effect)
H₁: b ≠ 0 (X has a linear effect)


**Test Statistic depends on whether σ² is known:**

### Case 1: σ² Known (Rare in Practice)
**Test Statistic:**

Z₁ = b̂ / √(σ²/sXX) ~ N(0,1) under H₀


**Decision Rule:** Reject H₀ if |Z₁| > Zα/₂ (e.g., 1.96 for α=0.05)

### Case 2: σ² Unknown (Standard Practice)
**Test Statistic:**

t₀ = b̂ / SE(b̂) = b̂ / √(s²/sXX) ~ t(n-2) under H₀


**Decision Rule:** Reject H₀ if |t₀| > t(n-2, α/₂)

**Standard Error:** SE(b̂) = √(s²/sXX)

### Detailed Example: Testing Significance

**From earlier example:**
- b̂ = 0.9
- s² = 0.6333
- sXX = 10
- n = 5, so df = 3

**Calculate:**

SE(b̂) = √(0.6333/10) = √0.06333 = 0.2517

t₀ = 0.9 / 0.2517 = 3.576


**Critical Value:** t(3, 0.025) = 3.182 (from t-table)

**Decision:** 3.576 > 3.182 → **Reject H₀**

**Conclusion:** There is significant evidence (at α=0.05) that X affects Y. The slope is statistically different from zero.

**p-value Approach:** For t=3.576 with 3 df, p-value ≈ 0.037 < 0.05, confirming rejection.

---

## 🔷 CONCEPT 11: Hypothesis Testing for the Intercept (a)

### Explanation
Testing whether the intercept equals a specific value a₀:

H₀: a = a₀
H₁: a ≠ a₀


**Test Statistic (σ² unknown):**

t₀ = (â - a₀) / SE(â) ~ t(n-2)

where SE(â) = √[s²(1/n + X̄²/sXX)]


### Detailed Example: Testing if Intercept is Zero

**Scenario:** Test H₀: a = 0 vs H₁: a ≠ 0

**From earlier:**
- â = 1.3
- s² = 0.6333
- n = 5, X̄ = 3, sXX = 10

**Calculate SE(â):**

SE(â) = √[0.6333(1/5 + 9/10)] 
      = √[0.6333(0.2 + 0.9)]
      = √[0.6333 × 1.1]
      = √0.6966
      = 0.8346


**Test Statistic:**

t₀ = (1.3 - 0) / 0.8346 = 1.558


**Critical Value:** t(3, 0.025) = 3.182

**Decision:** 1.558 < 3.182 → **Fail to reject H₀**

**Conclusion:** There is insufficient evidence to conclude the intercept differs from zero. The data is consistent with a line passing through the origin (though our estimate is 1.3, the uncertainty is large enough that zero is plausible).

---

## 🔷 CONCEPT 12: The General Linear Hypothesis and RSS Distribution

### Explanation
For inference in the general linear model Y = Xβ + ε with rank(X) = r (where r = k+1 including intercept):

**Distribution of Residual Sum of Squares:**

RSS/σ² = SSres/σ² ~ χ²(n - r)


**Key Properties:**
- **RSS (Residual Sum of Squares):** Σ(Yᵢ - Ŷᵢ)² = SSres
- **Degrees of freedom:** n - r (n observations minus r estimated parameters)
- **Chi-squared distribution:** Under normality of errors

**This underpins all F-tests in regression:**
The F-statistic for testing multiple coefficients simultaneously is based on comparing two RSS values (restricted vs unrestricted model) divided by their respective χ² degrees of freedom.

**F-Test General Form:**

F = [(RSS_R - RSS_U)/q] / [RSS_U/(n-r)] ~ F(q, n-r)

where:
- RSS_R = Residual SS from restricted model (under H₀)
- RSS_U = Residual SS from unrestricted model
- q = number of restrictions (coefficients being tested)

**Implication:** We can test any linear hypothesis about the coefficients (e.g., H₀: b₁ = b₂ = 0, testing if two predictors can be dropped simultaneously).

---

## 📌 Master Summary Table

| Concept | Formula/Definition | Key Insight |
|---------|-------------------|-------------|
| **Simple Model** | Y = a + bX + ε | Linear relationship with random noise |
| **OLS Slope** | b̂ = sXY/sXX | Covariance divided by variance of X |
| **OLS Intercept** | â = Ȳ - b̂X̄ | Line passes through (X̄, Ȳ) |
| **Var(b̂)** | σ²/sXX | Precision improves with spread of X |
| **Var(â)** | σ²(1/n + X̄²/sXX) | Depends on sample size and X location |
| **Cov(â,b̂)** | -X̄σ²/sXX | Negative correlation when X̄ > 0 |
| **Residuals** | eᵢ = Yᵢ - Ŷᵢ | Sum to zero, orthogonal to X |
| **SSres** | sYY - b̂·sXY | Unexplained variation |
| **s² estimate** | SSres/(n-2) | Unbiased estimate of error variance |
| **BLUE** | Gauss-Markov Theorem | OLS is best linear unbiased estimator |
| **Centered Model** | Y = a* + b(X-X̄) + ε | Makes intercept and slope uncorrelated |
| **Matrix OLS** | β̂ = (X⊤X)⁻¹X⊤Y | Generalizes to multiple predictors |
| **MLE** | Same as OLS for β | MLE σ̂² = SSres/n (biased) |
| **t-test for b** | t = b̂/SE(b̂) ~ t(n-2) | Test if X significantly affects Y |
| **t-test for a** | t = (â-a₀)/SE(â) ~ t(n-2) | Test if intercept equals specific value |
| **RSS/σ²** | ~ χ²(n-r) | Basis for F-tests and variance estimation |

---

## 🔗 The Complete Regression Workflow


1. MODEL SPECIFICATION
   ├── Define dependent variable Y
   ├── Identify independent variable(s) X
   └── Assume linear form: Y = a + bX + ε

2. DATA COLLECTION & EXPLORATION
   ├── Gather n observations (Xᵢ, Yᵢ)
   ├── Calculate descriptive statistics (X̄, Ȳ, sXX, sYY, sXY)
   └── Plot scatter diagram (check linearity)

3. ESTIMATION (OLS)
   ├── Calculate b̂ = sXY/sXX
   ├── Calculate â = Ȳ - b̂X̄
   └── Compute fitted values Ŷᵢ = â + b̂Xᵢ

4. DIAGNOSTICS & VALIDATION
   ├── Calculate residuals eᵢ = Yᵢ - Ŷᵢ
   ├── Verify Σeᵢ = 0 (check calculations)
   ├── Compute SSres and s² = SSres/(n-2)
   └── Assess fit (R² = 1 - SSres/SSTotal)

5. INFERENCE
   ├── Test significance of slope (H₀: b=0)
   ├── Test significance of intercept (H₀: a=0)
   ├── Construct confidence intervals: b̂ ± t(α/2)·SE(b̂)
   └── Make predictions with prediction intervals

6. INTERPRETATION
   ├── Explain slope: "For each 1-unit increase in X, Y increases by b̂ units"
   ├── Explain intercept: "Baseline Y when X=0 is â"
   └── Report reliability: "Standard error of estimate is s"
