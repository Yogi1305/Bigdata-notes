```markdown
# 📘 Complete Guide: Machine Learning Fundamentals — Bias-Variance, Cross-Validation, Classification & Inference

---

# PART 1: BIAS-VARIANCE TRADEOFF

---

## 🔷 CONCEPT 1: The Statistical Learning Setup

### Explanation
In supervised learning, we observe a dataset **S = {(x₁, y₁), ..., (xₙ, yₙ)}** drawn independently and identically distributed (i.i.d.) from a joint probability distribution P(X, Y). We apply a learning algorithm **A** to obtain a hypothesis (model) **hₛ = A(S)**.

**Critical Insight:** Since the training set S is random (different samples yield different models), the learned hypothesis **hₛ is itself a random variable**. If you collect a different sample tomorrow, you get a different model.

**Expected Test Error:** We care about performance not just on our specific sample, but averaged over all possible samples:
```
ε(h) = Eₛ[E_{(x,y)}[(hₛ(x) − y)²]]
```

### Detailed Example: Medical Diagnosis Model

**Scenario:** Predicting diabetes (y) from blood sugar levels (x).

**Sample 1 (n=100):** Mostly young patients → Model h₁ predicts diabetes only at very high sugar levels
**Sample 2 (n=100):** Mostly elderly patients → Model h₂ predicts diabetes at moderate sugar levels
**Sample 3 (n=100):** Balanced age → Model h₃ is more conservative

**Key Point:** Each sample gives a different hₛ. We want to know: what is the "average" performance across all possible samples we could have drawn?

---

## 🔷 CONCEPT 2: Key Definitions for Decomposition

### Explanation
To understand prediction error, we define three fundamental quantities:

**1. Expected Prediction (Average Model):**
```
h̄(x) = Eₛ[hₛ(x)]
```
The average prediction at point x if we trained on infinitely many datasets. Think of this as the "consensus" model.

**2. True Regression Function (Bayes Optimal):**
```
g(x) = E[y|x]
```
The best possible prediction at x — the expected value of y given x. No model can predict better than this on average.

**3. Irreducible Noise:**
```
ε = y − g(x),  where E[ε|x] = 0, Var(ε) = σ²
```
Random variation in y that cannot be explained by x (measurement error, unobserved factors).

---

## 🔷 CONCEPT 3: The Bias-Variance-Noise Decomposition (Core Theorem)

### Explanation
The expected squared error at any point x decomposes into three interpretable components:

```
E[(hₛ(x) − y)²] = Variance + Bias² + Noise
```

**Mathematically:**
```
E[(hₛ(x) − y)²] = E[(hₛ(x) − h̄(x))²] + (h̄(x) − g(x))² + E[(g(x) − y)²]
                  \______________/   \______________/   \___________/
                       Variance          Bias²            Noise
```

**Component Breakdown:**

| Component | Formula | Meaning | Analogy |
|-----------|---------|---------|---------|
| **Variance** | E[(hₛ − h̄)²] | How much the model changes with different training samples | Darts scattered widely (inconsistent) |
| **Bias²** | (h̄ − g)² | Systematic error: how far average model is from truth | Darts consistently off-center (wrong aim) |
| **Noise** | σ² | Irreducible randomness in data | Wind blowing darts off target (uncontrollable) |

**Intuition with Dartboard Analogy:**

1. **Low Bias, Low Variance:** Darts cluster tightly at bullseye ✅ Perfect model
2. **High Bias, Low Variance:** Darts cluster tightly but far from bullseye (e.g., aiming at wrong spot consistently)
3. **Low Bias, High Variance:** Darts centered on bullseye but scattered widely (unreliable)
4. **High Bias, High Variance:** Darts scattered everywhere and off-center (worst case)

### Detailed Example: Polynomial Regression

**True Function:** g(x) = sin(x) (nonlinear)
**Data:** Noisy samples y = sin(x) + ε, ε ~ N(0, 0.1²)

**Model 1: Linear (Degree 1)**
- High bias: line cannot capture sine wave curvature
- Low variance: line is stable across different samples

**Model 2: Degree 3 Polynomial**
- Low bias: can approximate sine wave reasonably
- Moderate variance: some flexibility but constrained

**Model 3: Degree 20 Polynomial**
- Very low bias: fits training points perfectly (including noise)
- Very high variance: wild oscillations between points, changes drastically with new samples

**The Tradeoff:** As model complexity increases, bias decreases but variance increases. There is a "sweet spot" minimizing total error.

---

## 🔷 CONCEPT 4: Bias-Variance in Linear Regression

### Explanation
For simple linear regression Y = a + bX + ε with OLS estimators:

**Prediction at point x₀:** ŷ(x₀) = â + b̂x₀

**MSE Decomposition:**
```
MSE(x₀) = E[(â + b̂x₀ − y₀)²]
        = Var(â + b̂x₀) + [Bias(â + b̂x₀)]² + σ²
```

**Key Property:** OLS is unbiased, so E[â] = a and E[b̂] = b, making the bias term zero when the model is correctly specified.

**Thus:**
```
MSE(x₀) = Var(â + b̂x₀) + σ²
        = σ²[1/n + (x₀ − X̄)²/sXX] + σ²
```

**Interpretation:**
- Prediction variance increases as x₀ moves farther from the mean X̄
- Precision is highest near the center of the data
- Total error cannot go below σ² (irreducible noise)

---

## 🔷 CONCEPT 5: Three Worked Examples from Literature

### Example 1: True f(x) = x (Linear Truth)

**Setup:** Data generated from y = x + ε, ε ~ N(0, 4), n=20

**Results across 100 simulations:**

| Model Complexity | Avg Bias² | Avg Variance | Total Error | Dominant Source |
|------------------|-----------|--------------|-------------|-----------------|
| **Degree 1** (Correct) | ~0.001 | 0.12 | **4.12** | Noise (σ²=4) |
| **Degree 3** | ~0.002 | 0.25 | **4.25** | Noise + Variance |
| **Degree 6** | ~0.005 | 0.56 | **4.56** | High Variance |

**Analysis:** Since truth is linear, all models have near-zero bias. Higher-degree polynomials overfit, increasing variance without improving bias.

**Visual:** All models follow the line y=x, but degree 6 wiggles more between points.

---

### Example 2: True f(x) = x² (Quadratic Truth)

**Setup:** y = x² + ε, same noise level

**Results:**

| Model | Avg Bias² | Avg Variance | Total Error |
|-------|-----------|--------------|-------------|
| **Degree 1** (Linear) | **1.82 × 10¹⁴** | 7.12 × 10¹² | ~10¹⁴ (Massive!) |
| **Degree 3** | **2.38 × 10¹¹** | 2.89 × 10¹⁰ | ~10¹¹ |
| **Degree 6** | **1.14 × 10⁴** | ~0 | ~11,400 |

**Analysis:** 
- Linear model has **catastrophic bias** — trying to fit a parabola with a straight line creates huge systematic errors at the extremes.
- Degree 3 (cubic) reduces bias dramatically but still insufficient.
- Degree 6 captures the curvature with negligible bias, leaving only noise (~σ²=4, plus small variance).

**Lesson:** When truth is complex, simple models fail due to bias, not variance.

---

### Example 3: True f(x) = x⁴ (Highly Nonlinear)

**Setup:** Quartic truth with multiple curves

**Pattern Confirmation:**
- Low-degree models (1-2): Massive bias, small variance
- Medium-degree (3-4): Balanced but still biased
- Degree 6: Optimal — bias near zero, variance controlled
- Degree >10: Overfitting begins (variance increases)

**General Principle:** Model complexity should match the "complexity" of the true underlying function. The bias-variance tradeoff guides this selection.

---

## 🔷 CONCEPT 6: Training vs. Test Error Dynamics

### Explanation
As we collect more data (increase n):

**Regime 1 — Small Data:**
- Training error: Low (model memorizes noise)
- Test error: High (poor generalization)
- **Diagnosis:** High variance (overfitting)

**Regime 2 — Large Data:**
- Training error increases toward true error (less overfitting)
- Test error decreases toward Bayes error (irreducible noise)
- Both converge to: **Noise + Bias** (variance eliminated by data volume)

**The Floor:** Even with infinite data, error cannot go below σ² (irreducible noise) + Bias² (if model is misspecified).

### Detailed Example: Learning Curves

**Scenario:** Neural network training on image classification.

**n = 100 samples:**
- Training accuracy: 95% (memorized)
- Test accuracy: 60% (fails on new images)
- **Action:** Need more data or regularization

**n = 10,000 samples:**
- Training accuracy: 85%
- Test accuracy: 82%
- Gap closed → good generalization
- **Status:** Bias dominates (model capacity insufficient for 100% accuracy)

**n = 1,000,000 samples:**
- Training: 80%, Test: 79.5%
- Diminishing returns reached
- **Status:** Near Bayes optimal (inherent ambiguity in images limits performance)

---

# PART 2: CROSS-VALIDATION

---

## 🔷 CONCEPT 7: Why Cross-Validation?

### Explanation
Since we cannot literally draw multiple datasets to estimate expected error (we only have one dataset!), **cross-validation (CV)** provides a resampling method to approximate this expectation.

**Core Idea:** Partition the single available dataset into multiple training/test splits, train and evaluate on each, then average the results.

**Primary Uses:**
1. **Model Selection:** Compare different algorithms or hyperparameters
2. **Error Estimation:** Get unbiased estimate of test error
3. **Tuning:** Select regularization parameters (λ in ridge regression, k in k-NN)

**The Problem with Single Split:** A single train/test split may be unlucky (all hard examples in test set). CV reduces this variance.

---

## 🔷 CONCEPT 8: Seven Cross-Validation Methods

### Method 1: Hold-Out Validation (Simple Split)

**Procedure:**
- Randomly split data: 70% training, 30% testing (or 80/20)
- Train on training set, evaluate on test set once

**Pros:** Fast, simple, no repeated computation
**Cons:** High variance in estimate; wasteful if data is scarce

**Example:** With 1000 samples and 70/30 split, 300 samples are never used for training.

---

### Method 2: Leave-One-Out Cross-Validation (LOOCV)

**Procedure:**
- For each observation i (from 1 to n):
  - Train on all data except (xᵢ, yᵢ)
  - Test on the left-out observation (xᵢ, yᵢ)
  - Record error eᵢ
- Final estimate: Average of all n errors

**Formula:** CV₍ₙ₎ = (1/n) Σᵢ ℓ(yᵢ, ĥ₍₋ᵢ₎(xᵢ))

**Pros:** 
- Nearly unbiased estimate of true error
- Deterministic (no randomness in splitting)

**Cons:**
- Computationally expensive: requires n model fits
- For n=1000, train 1000 models!
- High variance (estimates from similar training sets are correlated)

**Best for:** Small datasets (n < 100) where bias reduction is crucial.

---

### Method 3: k-Fold Cross-Validation

**Procedure:**
1. Randomly partition data into k equal-sized folds (typically k=5 or k=10)
2. For each fold j (from 1 to k):
   - Train on all folds except j
   - Test on fold j
   - Compute error R̂⁽ʲ⁾
3. Final estimate: Average across folds
   ```
   CVₖ = (1/k) Σⱼ₌₁ᵏ R̂⁽ʲ⁾
   ```

**Example with k=5:**
```
Fold 1: Test, Folds 2-5: Train → Error R̂⁽¹⁾
Fold 2: Test, Folds 1,3,4,5: Train → Error R̂⁽²⁾
...
Fold 5: Test, Folds 1-4: Train → Error R̂⁽⁵⁾

CV₅ = (R̂⁽¹⁾ + ... + R̂⁽⁵⁾)/5
```

**Pros:** 
- Computationally feasible (k=5 or 10)
- Lower variance than LOOCV
- Each point used for training (k-1)/k of the time

**Cons:** Randomness in fold assignment can affect results

---

### Method 4: Stratified k-Fold Cross-Validation

**Problem with Standard k-Fold:** Random partitioning might create imbalanced folds (e.g., all positive examples in one fold for classification).

**Solution:** Ensure each fold has approximately the same proportion of class labels as the full dataset.

**Procedure:**
1. Split data by class label
2. Within each class, create k folds
3. Combine folds across classes to ensure stratification

**Example:** 
- Dataset: 100 samples, 20% positive (20 pos, 80 neg)
- Standard 5-Fold might give: Fold 1 has 0 positives, Fold 2 has 8 positives (unbalanced!)
- Stratified 5-Fold ensures: Each fold has exactly 4 positives and 16 negatives

**Critical for:** Imbalanced classification (medical diagnosis, fraud detection, rare events)

---

### Method 5: Leave-p-Out Cross-Validation (LpO CV)

**Procedure:**
- Leave out every possible combination of p observations as test set
- Train on remaining n-p, test on the p left out
- Average over all C(n,p) combinations

**Formula:** CVₚ = (1/C(n,p)) Σ_{|S|=p} ℓ(yₛ, ĥ₍₋ₛ₎(xₛ))

**Example:** n=10, p=2
- Number of combinations: C(10,2) = 45
- Each pair of points serves as test set once
- Train on 8, test on 2, repeat 45 times

**Pros:** Exhaustive, less biased than single split
**Cons:** Computationally infeasible for large n (C(100,10) ≈ 1.73 × 10¹³ combinations!)

**Usage:** Mainly theoretical; rarely practical for n > 20.

---

### Method 6: Repeated k-Fold Cross-Validation

**Procedure:**
1. Perform k-Fold CV multiple times (e.g., 10 repeats)
2. Each time with different random partition (different random seed)
3. Average all k × repeat scores

**Example:** 10-Fold repeated 3 times = 30 total error estimates averaged

**Pros:** 
- Reduces variance from random fold assignment
- More stable estimate of performance
- Useful for small datasets where single k-fold has high variance

**Cons:** Computationally expensive (k × repeats model fits)

**Best practice:** Use when reporting final performance metrics; compare with single k-fold during development for speed.

---

### Method 7: Time Series Cross-Validation (Rolling/Forward Chaining)

**Problem with Standard CV:** Random shuffling destroys temporal structure and causes **data leakage** (using future to predict past).

**Solution:** Respect temporal ordering.

**Procedures:**

**Rolling Window (Fixed Size):**
```
Train: [t₁...t₁₀₀], Test: [t₁₀₁...t₁₁₀]
Train: [t₁₁...t₁₁₀], Test: [t₁₁₁...t₁₂₀]
...
```
Window slides forward, maintaining constant training size.

**Expanding Window:**
```
Train: [t₁...t₁₀₀], Test: [t₁₀₁...t₁₁₀]
Train: [t₁...t₁₁₀], Test: [t₁₁₁...t₁₂₀]
...
```
Training set grows over time (uses all available history).

**Example:** Predicting tomorrow's stock price.
- **Wrong:** Shuffle 2020-2024 data randomly, train on 2022+2024, test on 2020
- **Right:** Train on Jan-Mar 2024, predict April 2024; then train on Jan-Apr, predict May, etc.

---

## 🔷 CONCEPT 9: Loss Functions in Classification

### Explanation
The **loss function** ℓ(y, h(x)) quantifies the cost of predicting h(x) when the true label is y.

**Common Loss Functions:**

| Loss | Formula | Use Case | Properties |
|------|---------|----------|------------|
| **0-1 Loss** | ℓ = 0 if y = ĥ, 1 otherwise | Misclassification rate | Discontinuous, hard to optimize |
| **Squared Loss** | ℓ = (y − ĥ)² | Regression | Penalizes large errors heavily |
| **Absolute Loss** | ℓ = \|y − ĥ\| | Robust regression | Less sensitive to outliers |
| **Log Loss (Cross-Entropy)** | ℓ = −[y log ĥ + (1−y) log(1−ĥ)] | Binary classification | Differentiable, probabilistic interpretation |

**Empirical Risk:**
```
R̂(h) = (1/n) Σᵢ₌₁ⁿ ℓ(yᵢ, h(xᵢ))
```
The average loss over the training set — what we minimize during training.

**Example Comparison:**

**Scenario:** Medical test, y=1 (disease), y=0 (healthy), prediction ĥ = 0.9

**0-1 Loss:** If threshold 0.5, ĥ > 0.5 → predict 1 → correct if y=1, loss=0

**Log Loss:** 
- If y=1: ℓ = −log(0.9) ≈ 0.105
- If y=0: ℓ = −log(0.1) ≈ 2.303 (heavy penalty for wrong confidence!)

Log loss penalizes confident wrong predictions much more than 0-1 loss.

---

# PART 3: CLASSIFICATION & LOGISTIC REGRESSION

---

## 🔷 CONCEPT 10: What is Classification?

### Explanation
**Classification** assigns inputs **x** to discrete **class labels** from a finite set Y = {1, 2, ..., K}.

**Types:**
- **Binary:** K=2 (spam/not spam, sick/healthy)
- **Multiclass:** K>2 (digit recognition: 0-9, species identification)

**Probabilistic Approach:**
Rather than just predicting the label, we estimate **conditional probabilities**:
```
P(y = c | x) for each class c ∈ {1, ..., K}
```

**Decision Rule:** Pick the class with highest probability:
```
ŷ = argmax_c P(y = c | x)
```

**Advantages of Probabilistic Output:**
- Confidence quantification (P=0.99 vs P=0.51)
- Risk-sensitive decision making (threshold adjustment)
- Combining with other information (Bayesian updating)

### Detailed Example: Email Classification

**Input x:** Bag of words representation (count of "free", "winner", "meeting", etc.)
**Output y:** 1 (spam) or 0 (ham)

**Model Output:**
- Email A: P(spam|x) = 0.95 → Classify as Spam
- Email B: P(spam|x) = 0.45 → Classify as Ham (but borderline)
- Email C: P(spam|x) = 0.99 → Very confident Spam

**Threshold Adjustment:**
- Standard: threshold = 0.5
- Conservative (avoid missing important emails): threshold = 0.8 (only flag if P > 0.8)
- Aggressive (catch all spam): threshold = 0.2 (flag if P > 0.2)

---

## 🔷 CONCEPT 11: Why Linear Regression Fails for Classification

### Explanation
**The Problem:** Linear regression outputs values in (−∞, +∞), but probabilities must be in [0, 1].

**Example:** Predicting P(disease|age):
- Linear regression might predict 1.7 (nonsensical, >100% probability) or −0.3 (negative probability)
- Even if clamped to [0,1], the linear model assumes constant marginal effects (same slope everywhere), which is inappropriate for probabilities

**The Sigmoid Solution:**
The **logistic function** (sigmoid) maps any real number to (0,1):
```
σ(z) = 1 / (1 + e^(−z))
```

**Properties:**
- σ(0) = 0.5
- σ(z) → 1 as z → +∞
- σ(z) → 0 as z → −∞
- Symmetric: σ(−z) = 1 − σ(z)
- Differentiable: σ'(z) = σ(z)(1 − σ(z)) [convenient for optimization]

**Visual:**
```
z:    -6    -4    -2     0     2     4     6
σ(z): 0.00  0.02  0.12  0.50  0.88  0.98  1.00
       \__________________/|\________________/
                S-curve shape
```

---

## 🔷 CONCEPT 12: Logistic Regression — Step-by-Step Derivation

### Step 1: The Model Specification
```
P(y=1|x) = σ(wᵀx + b) = 1 / (1 + e^(−(wᵀx+b)))
```
Where:
- **w:** Weight vector (coefficients for each feature)
- **b:** Bias term (intercept)
- **wᵀx + b:** Linear combination (log-odds or "logit")

**Odds Interpretation:**
```
P/(1-P) = e^(wᵀx+b)
log(P/(1-P)) = wᵀx + b  (linear in x!)
```

### Step 2: The Likelihood Function
For binary labels yᵢ ∈ {0, 1}:
```
P(yᵢ|xᵢ) = P̂ᵢ^yᵢ × (1−P̂ᵢ)^(1−yᵢ)
```
Where P̂ᵢ = σ(wᵀxᵢ + b)

**Interpretation:**
- If yᵢ = 1: contribution is P̂ᵢ (probability assigned to positive class)
- If yᵢ = 0: contribution is (1−P̂ᵢ) (probability assigned to negative class)

**Joint Likelihood (i.i.d. assumption):**
```
L(w,b) = ∏ᵢ₌₁ⁿ P̂ᵢ^yᵢ (1−P̂ᵢ)^(1−yᵢ)
```

### Step 3: Log-Likelihood (Easier to Optimize)
```
ℓ(w,b) = log L(w,b) = Σᵢ [yᵢ log P̂ᵢ + (1−yᵢ) log(1−P̂ᵢ)]
```

**Goal:** Maximize ℓ(w,b) — find parameters making observed data most probable.

**Equivalent:** Minimize negative log-likelihood (cross-entropy loss):
```
J(w,b) = −ℓ(w,b) = −Σᵢ [yᵢ log P̂ᵢ + (1−yᵢ) log(1−P̂ᵢ)]
```

### Detailed Example: 2-Data-Point Calculation

**Data:**
- x₁ = [0, 1], y₁ = 0
- x₂ = [1, 1], y₂ = 1
- Initialize: w = [0, 0], b = 0

**Initial Predictions:**
```
z₁ = 0·0 + 0·1 + 0 = 0 → P̂₁ = σ(0) = 0.5
z₂ = 0·1 + 0·1 + 0 = 0 → P̂₂ = σ(0) = 0.5
```

**Loss Calculation:**
```
J = −[y₁ log P̂₁ + (1−y₁) log(1−P̂₁) + y₂ log P̂₂ + (1−y₂) log(1−P̂₂)]
  = −[0·log(0.5) + 1·log(0.5) + 1·log(0.5) + 0·log(0.5)]
  = −[log(0.5) + log(0.5)]
  = −[−0.693 + (−0.693)]
  = 1.386
```

**After one gradient descent step (see Concept 13), loss decreases.**

### Step 4: Gradient Derivation (Chain Rule)
Using σ'(z) = σ(z)(1−σ(z)):

**For weight wⱼ:**
```
∂J/∂wⱼ = −Σᵢ (yᵢ − P̂ᵢ) xᵢⱼ
```

**For bias b:**
```
∂J/∂b = −Σᵢ (yᵢ − P̂ᵢ)
```

**Intuition:** (yᵢ − P̂ᵢ) is the prediction error. If yᵢ=1 but P̂ᵢ=0.3 (error +0.7), gradient pushes weights to increase P̂ᵢ for this xᵢ.

### Step 5: Gradient Descent Update
```
wⱼ := wⱼ − α · ∂J/∂wⱼ = wⱼ + α · Σᵢ (yᵢ − P̂ᵢ) xᵢⱼ
b := b − α · ∂J/∂b = b + α · Σᵢ (yᵢ − P̂ᵢ)
```
Where α is the learning rate.

---

## 🔷 CONCEPT 13: Gradient Descent Optimization

### Explanation
Gradient descent is an iterative algorithm to find the minimum of a function (here, the loss J).

**Algorithm:**
1. Initialize parameters w⁰, b⁰ (often zeros or small random values)
2. For t = 1, 2, ..., T:
   - Compute gradient ∇J(wᵗ, bᵗ)
   - Update: wᵗ⁺¹ = wᵗ − α · ∇J(wᵗ)
   - Stop when ‖∇J‖ < ε or maximum iterations reached

**Learning Rate α:**
- **Too small:** Slow convergence, many iterations
- **Too large:** Oscillates, may diverge
- **Just right:** Steady decrease toward minimum

**Variations:**
- **Batch GD:** Use all n samples per step (accurate but slow)
- **Stochastic GD (SGD):** Use 1 sample at a time (fast but noisy)
- **Mini-batch GD:** Use m samples (32, 64, 128) per step (balance)

### Detailed Example: Hill Descent Analogy

**Scenario:** Blindfolded person on a mountain (loss landscape) trying to reach the valley (minimum).

**At each step:**
1. Feel the ground to determine which way is steepest downhill (compute gradient)
2. Take a step of size α in that direction (update parameters)
3. Repeat until flat ground reached (gradient ≈ 0)

**Problems:**
- **Local minima:** May get stuck in small valley when global valley exists (mitigated by random initialization in practice)
- **Saddle points:** Flat in some directions, curved in others (common in high dimensions)
- **Plateaus:** Flat regions where progress is slow (use momentum or adaptive learning rates)

---

## 🔷 CONCEPT 14: Decision Boundary

### Explanation
The **decision boundary** separates regions where different classes are predicted. For binary logistic regression with threshold 0.5:

**Boundary Condition:**
```
P(y=1|x) = 0.5
σ(wᵀx + b) = 0.5
wᵀx + b = 0  (since σ(0) = 0.5)
```

**Geometric Interpretation:**
- In 2D: w₁x₁ + w₂x₂ + b = 0 is a **straight line**
- In 3D: w₁x₁ + w₂x₂ + w₃x₃ + b = 0 is a **plane**
- In p-D: **Hyperplane** separating the space

**Classification Rule:**
- wᵀx + b > 0 → Predict Class 1 (P > 0.5)
- wᵀx + b < 0 → Predict Class 0 (P < 0.5)
- wᵀx + b = 0 → On boundary (P = 0.5, ambiguous)

### Detailed Example: 2D Decision Boundary

**Parameters:** w = [1, −2], b = 3

**Boundary Equation:**
```
1·x₁ + (−2)·x₂ + 3 = 0
x₁ − 2x₂ + 3 = 0
x₂ = (x₁ + 3)/2 = 0.5x₁ + 1.5
```

**Visualization:**
```
x₂ (vertical)
↑
5 |        / Predict 1 (P>0.5)
4 |       /
3 |      /  ● (point [1,3]: 1−6+3=−2<0 → Class 0)
2 |     /
1 |    / ● (point [2,1]: 2−2+3=3>0 → Class 1)
0 +---/----------→ x₁ (horizontal)
  0   1   2   3   4
      |
   Boundary line: x₂ = 0.5x₁ + 1.5
```

**Point Tests:**
- **Point A (x₁=4, x₂=1):** 4 − 2(1) + 3 = 5 > 0 → Predict Class 1 with P = σ(5) ≈ 0.993
- **Point B (x₁=1, x₂=3):** 1 − 2(3) + 3 = −2 < 0 → Predict Class 0 with P = σ(−2) ≈ 0.119

---

# PART 4: LIKELIHOOD RATIO TEST

---

## 🔷 CONCEPT 15: The Likelihood Ratio Test (LRT) Framework

### Explanation
The LRT compares **nested models** to determine if additional parameters significantly improve fit.

**Nested Models:** The simpler model (null) can be obtained from the complex model (alternative) by setting some parameters to zero.

**Hypothesis Setup:**
- **H₀ (Reduced/Null):** Parameters in Θ₀ (dimension r₀) — simpler model
- **H₁ (Full/Alternative):** Parameters in Θ (dimension r) — complex model
- **Constraint:** Θ₀ ⊂ Θ, and typically r = r₀ + k (k additional parameters)

**Test Statistic:**
```
D = −2 log Λ = 2(ℓ₁ − ℓ₀)
```
Where:
- ℓ₁ = maximized log-likelihood under full model (H₁)
- ℓ₀ = maximized log-likelihood under reduced model (H₀)
- Λ = L₀/L₁ is the likelihood ratio

**Distribution Under H₀:**
```
D ~ χ²(k)  asymptotically
```
Where k = r − r₀ = number of parameters restricted under H₀ (degrees of freedom).

**Decision Rule:**
- If D > χ²ₖ,₁₋α (critical value), **reject H₀**
- Conclusion: The additional k parameters significantly improve the model

**Intuition:** If the complex model fits much better (much higher likelihood), the likelihood ratio is small, −2log(Λ) is large, and we reject the simpler model.

---

## 🔷 CONCEPT 16: LRT for Logistic Regression — Complete Worked Example

### Problem Setup
**Research Question:** Does Blood Pressure improve prediction of Heart Disease beyond what Age alone provides?

**Data (n=5 patients):**

| Patient | Age (x₁) | Blood Pressure (x₂) | Disease (y) |
|---------|----------|---------------------|-------------|
| 1 | 30 | 120 | 0 |
| 2 | 40 | 130 | 0 |
| 3 | 50 | 140 | 1 |
| 4 | 60 | 150 | 1 |
| 5 | 70 | 160 | 1 |

**Model Specifications:**

**Full Model (H₁):** 
```
log(P/(1-P)) = b + w₁·Age + w₂·BP
```
Parameters: θ = (b, w₁, w₂), dimension r = 3

**Reduced Model (H₀):**
```
log(P/(1-P)) = b + w₁·Age   (w₂ = 0, BP excluded)
```
Parameters: θ₀ = (b, w₁), dimension r₀ = 2

**Hypothesis:** H₀: w₂ = 0 vs H₁: w₂ ≠ 0

### Fitting Results

After maximum likelihood estimation (via gradient descent or numerical optimization):

**Full Model Fit:**
- Estimated parameters: b̂ ≈ −7.5, ŵ₁ ≈ 0.12, ŵ₂ ≈ 0.03
- Maximized log-likelihood: **ℓ₁ = −0.005018**

**Reduced Model Fit:**
- Estimated parameters: b̂₀ ≈ −4.2, ŵ₁₀ ≈ 0.08 (w₂ forced to 0)
- Maximized log-likelihood: **ℓ₀ = −3.365058**

**Likelihood Ratio:**
```
Λ = L₀/L₁ = exp(ℓ₀ − ℓ₁) = exp(−3.365058 − (−0.005018)) = exp(−3.36) ≈ 0.035
```
(The reduced model is ~3% as likely as the full model given the data)

### Test Statistic Calculation

```
D = −2 log Λ = 2(ℓ₁ − ℓ₀)
  = 2(−0.005018 − (−3.365058))
  = 2(3.36004)
  = **6.720**
```

**Degrees of Freedom:**
```
k = r − r₀ = 3 − 2 = 1
```
(One additional parameter: w₂)

**Critical Value:**
```
χ²₁,₀.₉₅ = 3.841  (from chi-squared table, α=0.05)
```

### Decision and Conclusion

**Comparison:** 6.720 > 3.841

**Decision:** **Reject H₀** at α = 0.05 significance level.

**Interpretation:**
- The test statistic (6.72) exceeds the critical value (3.84)
- p-value = P(χ²₁ > 6.72) ≈ 0.0095 < 0.05
- **Conclusion:** Blood Pressure provides significant additional predictive power for Heart Disease beyond Age alone. The full model (including BP) is statistically significantly better than the reduced model (Age only).

**Practical Implication:** Doctors should consider both Age and Blood Pressure when assessing heart disease risk, not just Age.

---

## 📌 Master Summary Table

| Concept | Key Formula/Definition | When to Use |
|---------|---------------------|-------------|
| **Bias²** | (h̄(x) − g(x))² | Measure of systematic error |
| **Variance** | E[(hₛ−h̄)²] | Measure of instability across samples |
| **Noise** | σ² = E[(g−y)²] | Irreducible error |
| **Hold-Out** | Single 70/30 split | Large datasets, quick evaluation |
| **LOOCV** | n fits, leave one out | Small n, unbiased estimate |
| **k-Fold CV** | k fits, rotate folds | Standard choice (k=5,10) |
| **Stratified CV** | Preserve class proportions | Imbalanced classification |
| **Sigmoid** | σ(z) = 1/(1+e⁻ᶻ) | Map scores to probabilities |
| **Log-Likelihood** | Σ[y log p̂ + (1−y)log(1−p̂)] | Objective for logistic regression |
| **Gradient** | ∂J/∂wⱼ = −Σ(yᵢ−p̂ᵢ)xᵢⱼ | Direction of steepest descent |
| **Decision Boundary** | wᵀx + b = 0 | Classification threshold |
| **LRT Statistic** | D = 2(ℓ₁−ℓ₀) ~ χ²ₖ | Compare nested models |
| **LRT Decision** | Reject H₀ if D > χ²ₖ,₁₋α | Test if extra parameters help |

---

## 🔗 Complete Workflow Diagram

```
SUPERVISED LEARNING PIPELINE
│
├── 1. PROBLEM DEFINITION
│   ├── Regression (continuous y) OR Classification (discrete y)
│   └── Identify features x and target y
│
├── 2. MODEL SELECTION (Bias-Variance)
│   ├── Simple models (high bias, low variance): Linear, small trees
│   ├── Complex models (low bias, high variance): Deep nets, high-degree polynomials
│   └── Select complexity matching true function complexity
│
├── 3. TRAINING & EVALUATION (Cross-Validation)
│   ├── Split data: k-Fold CV or Stratified CV
│   ├── Train on (k-1) folds, validate on 1 fold
│   └── Average performance across folds
│
├── 4. ALGORITHM IMPLEMENTATION
│   ├── Regression: OLS, Ridge, Lasso
│   ├── Classification: Logistic Regression
│   │   ├── Define sigmoid σ(z)
│   │   ├── Set up log-likelihood ℓ(w,b)
│   │   ├── Compute gradients ∂ℓ/∂w, ∂ℓ/∂b
│   │   └── Optimize via Gradient Descent
│   └── Find decision boundary wᵀx+b=0
│
├── 5. INFERENCE (Likelihood Ratio Test)
│   ├── Fit full model (all features): ℓ₁
│   ├── Fit reduced model (subset): ℓ₀
│   ├── Compute D = 2(ℓ₁−ℓ₀)
│   └── Compare to χ² critical value → Retain significant features
│
└── 6. DEPLOYMENT
    ├── Final model with selected features
    └── Monitor bias-variance tradeoff on new data
```

**Key Insight:** The bias-variance tradeoff guides model complexity selection, cross-validation provides reliable performance estimates, logistic regression with gradient descent solves classification problems probabilistically, and the likelihood ratio test provides rigorous statistical justification for including or excluding features.