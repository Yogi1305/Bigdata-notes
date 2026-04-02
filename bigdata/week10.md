
# 📘 Module 10: Principal Component Analysis — Complete Reference Guide (NPTEL)

---

# LECTURE 1: POPULATION VS SAMPLE PCA — FOUNDATIONS

---

## 🔷 CONCEPT 1: The Setup — Sample Mean and Covariance Matrix

### Explanation
Before performing PCA, we center the data and compute the sample covariance structure.

**Given:** n observations on p variables, arranged as an n×p data matrix **X**.

**Sample Mean Vector:**

X̄ = (1/n) Σᵢ₌₁ⁿ Xᵢ = (X̄₁, X̄₂, ..., X̄ₚ)ᵀ


**Centered Data Matrix:**

X̃ = X − 1X̄ᵀ   (subtract mean from each column)


**Sample Covariance Matrix:**

S = (1/(n−1)) X̃ᵀX̃ = (1/(n−1)) Σᵢ₌₁ⁿ (Xᵢ − X̄)(Xᵢ − X̄)ᵀ


**Sample Correlation Matrix:**

R = D⁻¹/² S D⁻¹/²

where D = diag(s₁₁, s₂₂, ..., sₚₚ) contains the sample variances.

### Detailed Example: Bivariate Dataset (n=5, p=2)

**Raw Data:**
| Observation | X₁ (Height) | X₂ (Weight) |
|-------------|-------------|-------------|
| 1 | 160 | 55 |
| 2 | 170 | 65 |
| 3 | 165 | 60 |
| 4 | 180 | 75 |
| 5 | 175 | 70 |

**Sample Mean:**

X̄₁ = (160+170+165+180+175)/5 = 170
X̄₂ = (55+65+60+75+70)/5 = 65
X̄ = [170, 65]ᵀ


**Centered Data:**
| Obs | X̃₁ | X̃₂ |
|-----|-----|-----|
| 1 | −10 | −10 |
| 2 | 0 | 0 |
| 3 | −5 | −5 |
| 4 | +10 | +10 |
| 5 | +5 | +5 |

**Sample Covariance:**

s₁₁ = (100+0+25+100+25)/4 = 62.5
s₂₂ = (100+0+25+100+25)/4 = 62.5
s₁₂ = (100+0+25+100+25)/4 = 62.5

S = [ 62.5  62.5 ]
    [ 62.5  62.5 ]


**Interpretation:** Perfect sample correlation (ρ̂ = 1) because X₂ = X₁ − 105 exactly in this constructed example.

---

## 🔷 CONCEPT 2: The Goal of PCA — Variance Maximization

### Explanation
PCA seeks linear combinations of variables that capture maximum variance in successive, orthogonal directions.

**Principal Components (PCs):**
The k-th PC is:

Yₖ = eₖᵀX̃ = eₖ₁X̃₁ + eₖ₂X̃₂ + ... + eₖₚX̃ₚ

where **eₖ** is the k-th eigenvector of S (or Σ for population PCA).

**Optimization Problem for PC1:**

Maximize: Var(Y₁) = e₁ᵀSe₁
Subject to: e₁ᵀe₁ = 1 (unit length)


**Solution:** By Rayleigh-Ritz theorem, the maximum is the largest eigenvalue λ₁ of S, achieved when e₁ is the corresponding eigenvector.

**Optimization for PC2:**

Maximize: Var(Y₂) = e₂ᵀSe₂
Subject to: e₂ᵀe₂ = 1 and e₂ᵀe₁ = 0 (orthogonal to PC1)


**Solution:** The second largest eigenvalue λ₂ and its eigenvector e₂.

### Detailed Example: Finding PC1 and PC2

**From previous example:**

S = [ 62.5  62.5 ]
    [ 62.5  62.5 ]


**Eigen-decomposition:**

Characteristic equation: det(S − λI) = (62.5−λ)² − 62.5² = 0
(62.5−λ)² = 62.5²
62.5−λ = ±62.5

λ₁ = 125, λ₂ = 0


**Eigenvectors:**
- For λ₁ = 125: [62.5−125, 62.5; 62.5, 62.5−125] = [−62.5, 62.5; ...]
  → e₁ = [1/√2, 1/√2]ᵀ ≈ [0.707, 0.707]ᵀ
  
- For λ₂ = 0: [62.5, 62.5; ...] 
  → e₂ = [1/√2, −1/√2]ᵀ ≈ [0.707, −0.707]ᵀ

**Principal Components:**

Y₁ = 0.707(X̃₁) + 0.707(X̃₂) = 0.707(Height_c) + 0.707(Weight_c)
   = 0.707(X̃₁ + X̃₂)  [Sum of standardized variables]

Y₂ = 0.707(X̃₁) − 0.707(X̃₂) = 0.707(X̃₁ − X̃₂)  [Difference]


**Variance Captured:**
- PC1 captures λ₁ = 125 (100% of total variance 125+0)
- PC2 captures λ₂ = 0 (redundant direction)

---

## 🔷 CONCEPT 3: Population PCA vs Sample PCA

### Explanation
| Aspect | Population PCA | Sample PCA |
|--------|---------------|------------|
| **Data** | Entire population | Sample of size n |
| **Parameters** | True mean µ, true covariance Σ | Sample mean X̄, sample covariance S |
| **Eigen-decomposition** | Σ = EΛEᵀ | S = ÊΛ̂Êᵀ |
| **PCs** | Y = Eᵀ(X − µ) | Ŷ = Êᵀ(X − X̄) |
| **Properties** | Exact, theoretical | Estimated, random |
| **Convergence** | Fixed | As n → ∞, sample → population |

**Key Insight:** Sample PCs are random variables that converge to population PCs as sample size increases (Law of Large Numbers).

### Detailed Example: Bivariate Normal Simulation

**True Population:** X ~ N₂(µ, Σ) with

µ = [0, 0]ᵀ
Σ = [ 1    0.8 ]
    [ 0.8  1   ]  (ρ = 0.8)


**True Eigen-decomposition:**

λ₁ = 1.8,  e₁ = [1/√2, 1/√2]ᵀ  (major axis)
λ₂ = 0.2,  e₂ = [1/√2, −1/√2]ᵀ (minor axis)


**Simulation Study:**

| Sample Size n | λ̂₁ (est.) | λ̂₂ (est.) | Angle Error | Proportion λ̂₁/Σλ̂ |
|---------------|-----------|-----------|-------------|------------------|
| 10 | 2.1 | 0.15 | 12° | 93% |
| 50 | 1.75 | 0.22 | 4° | 89% |
| 200 | 1.82 | 0.19 | 1.5° | 90.5% |
| 1000 | 1.798 | 0.198 | 0.3° | 90.1% |
| ∞ (True) | 1.8 | 0.2 | 0° | 90% |

**Observation:** As n increases, sample eigenvalues converge to population eigenvalues (1.8, 0.2) and sample eigenvectors align with true directions (45° and −45°).

---

# LECTURE 2: MATHEMATICAL FORMULATION — THREE CORE THEOREMS

---

## 🔷 THEOREM 1: Sample PCs are Uncorrelated with Variances = Eigenvalues

### Statement
For the sample principal components Ŷₖ = êₖᵀ(X − X̄):

1. **Var(Ŷₖ) = λ̂ₖ** (the k-th sample eigenvalue)
2. **Cov(Ŷⱼ, Ŷₖ) = 0** for j ≠ k (sample PCs are uncorrelated)

### Proof/Explanation
Since S is symmetric, eigenvectors êₖ are orthonormal: êⱼᵀêₖ = δⱼₖ (1 if j=k, 0 otherwise).

**Variance:**

Var(Ŷₖ) = êₖᵀ S êₖ = êₖᵀ (λ̂ₖ êₖ) = λ̂ₖ (êₖᵀêₖ) = λ̂ₖ


**Covariance:**

Cov(Ŷⱼ, Ŷₖ) = êⱼᵀ S êₖ = êⱼᵀ (λ̂ₖ êₖ) = λ̂ₖ (êⱼᵀêₖ) = 0  (for j≠k)


### Detailed Example: Verifying Uncorrelatedness

**From Lecture 1 example (n=5):**

Centered data matrix X̃:
[ −10  −10 ]
[   0    0 ]
[  −5   −5 ]
[  10   10 ]
[   5    5 ]

Eigenvectors:
ê₁ = [0.707, 0.707]ᵀ, ê₂ = [0.707, −0.707]ᵀ

Compute PC scores:
Ŷ₁ = X̃ ê₁ = [−14.14, 0, −7.07, 14.14, 7.07]ᵀ
Ŷ₂ = X̃ ê₂ = [0, 0, 0, 0, 0]ᵀ  (zero because data is perfectly correlated)

Sample variances:
Var(Ŷ₁) = (200+0+50+200+50)/4 = 125 = λ₁ ✓
Var(Ŷ₂) = 0 = λ₂ ✓

Sample covariance:
Cov(Ŷ₁, Ŷ₂) = 0 (since Ŷ₂ is constant zero)


---

## 🔷 THEOREM 2: Proportion of Variance Explained

### Statement
The proportion of **total sample variance** explained by the k-th sample PC is:

λ̂ₖ / (λ̂₁ + λ̂₂ + ... + λ̂ₚ) = λ̂ₖ / tr(S)


where tr(S) = Σ sⱼⱼ is the sum of sample variances (total variance).

### Explanation
Since PCs are uncorrelated, their variances add up to the total variance in the standardized space. The trace of S equals the sum of eigenvalues.

**Cumulative Proportion:**

(λ̂₁ + ... + λ̂ₖ) / tr(S)

tells us how much variance is captured by the first k PCs.

### Detailed Example: Variance Decomposition

**Blood Chemistry Data (p=8 variables, n=180):**

| PC | Eigenvalue λ̂ | Individual % | Cumulative % |
|----|---------------|--------------|--------------|
| 1 | 3.34 | 41.8% | 41.8% |
| 2 | 1.54 | 19.3% | 61.1% |
| 3 | 0.95 | 11.9% | 73.0% |
| 4 | 0.77 | 9.6% | 82.6% |
| 5 | 0.55 | 6.9% | 89.5% |
| 6 | 0.35 | 4.4% | 93.9% |
| 7 | 0.27 | 3.4% | 97.3% |
| 8 | 0.22 | 2.8% | 100.0% |
| **Total** | **7.99** | **100%** | |

**Interpretation:** The first 2 PCs capture 61% of total variance; first 4 capture 83%. We might retain 4 PCs for dimensionality reduction.

---

## 🔷 THEOREM 3: Correlation Between PC and Original Variable

### Statement
The sample correlation between the k-th PC Ŷₖ and the i-th original variable Xᵢ is:

r_{Ŷₖ, Xᵢ} = êₖᵢ √λ̂ₖ / √sᵢᵢ


where:
- êₖᵢ = i-th component of k-th eigenvector (loading)
- λ̂ₖ = eigenvalue of k-th PC
- sᵢᵢ = sample variance of Xᵢ

### Explanation
This shows how much each original variable contributes to each PC. High absolute correlation means the variable is important for that component.

**Loading vs Correlation:**
- **Loading (êₖᵢ):** Coefficient in the linear combination
- **Correlation:** Loading scaled by relative variance of PC vs variable

### Detailed Example: Blood Chemistry Interpretation

**Variable:** NEUT (Neutrophils), variance sᵢᵢ = 1.0 (standardized)

**PC1 loadings and correlations:**

| Variable | ê₁ᵢ (loading) | √λ̂₁ | Correlation r |
|----------|---------------|-----|---------------|
| NEUT | 0.42 | √3.34≈1.83 | 0.42×1.83/1 = **0.77** |
| LYMPH | −0.38 | 1.83 | **−0.70** |
| PLATE | 0.35 | 1.83 | **0.64** |
| HCT | 0.32 | 1.83 | **0.59** |

**Interpretation:** PC1 is positively correlated with NEUT, PLATE, HCT and negatively with LYMPH. This represents a "inflammatory response" factor (high neutrophils, low lymphocytes typical of bacterial infection).

---

# LECTURE 3: COVARIANCE VS CORRELATION MATRIX — THE SCALING ISSUE

---

## 🔷 CONCEPT 4: When to Standardize — The Blood Chemistry Example

### Explanation
PCA on covariance matrix S is dominated by variables with large variances. PCA on correlation matrix R treats all variables equally (standardized to variance 1).

**Critical Rule:** 
- Use **Covariance PCA** when variables share the same scale/units (e.g., all gene expression levels, all test scores)
- Use **Correlation PCA** when variables have different scales/units (e.g., height in cm vs weight in kg vs income in $)

### Detailed Example: Blood Chemistry (8 Variables)

**Raw Variances (Covariance PCA):**
| Variable | Meaning | Variance |
|----------|---------|----------|
| PLATE | Platelet count | **1701** |
| RBC | Red blood cell count | 0.90 |
| HGB | Hemoglobin | 1.20 |
| HCT | Hematocrit | 1.50 |
| NEUT | Neutrophils | 1.80 |
| LYMPH | Lymphocytes | 2.10 |
| MONO | Monocytes | 0.75 |
| EOS | Eosinophils | 0.45 |

**Problem:** PLATE variance (1701) is 1000× larger than other variables!

**Covariance PCA Results:**
- PC1 is essentially just **PLATE** (correlation ≈ 0.99 with PLATE)
- PC2, PC3, etc. capture remaining variance
- Biological structure (NEUT-LYMPH opposition) hidden in minor components

**Correlation PCA (Standardized Variables):**
- All variables have variance 1
- PLATE no longer dominates
- PC1 reveals biological pattern: NEUT (+) vs LYMPH (−) opposition
- PC2 captures RBC-HGB-HCT cluster (red cell indices)
- PC3 captures MONO-EOS (other white cells)

**Comparison:**

| Aspect | Covariance PCA | Correlation PCA |
|--------|---------------|-----------------|
| PC1 | PLATE only | NEUT vs LYMPH |
| PC2 | PLATE residual | RBC-HGB-HCT |
| Interpretation | Artifact of scale | Biological structure |
| Total Variance | 1701 + others | 8 (equal) |

**Conclusion:** Always use correlation PCA when variances differ by orders of magnitude!

---

# LECTURE 4: EXAMPLES — INTERPRETING PCA OUTPUT

---

## 🔷 CONCEPT 5: Example 1 — Blood Chemistry (8 Variables)

### Detailed Analysis

**Data:** n=180 blood samples, p=8 chemical measurements.

**Correlation Structure (Key findings):**
1. **NEUT ↔ LYMPH:** r = −0.75 (strong negative)
   - Biological reality: neutrophils and lymphocytes are inversely regulated
2. **RBC ↔ HGB ↔ HCT:** r ≈ 0.9 (strong positive cluster)
   - These measure similar aspect of red blood cells
3. **PLATE:** Relatively independent (r ≈ 0.2 with others)

**PC1 (41.8% variance):**

Loadings: NEUT(0.42), LYMPH(−0.38), PLATE(0.35), HCT(0.32), ...

**Interpretation:** "Acute phase reaction" — high neutrophils + low lymphocytes indicate bacterial infection/inflammation; platelets also rise in inflammation.

**PC2 (19.3% variance):**

Loadings: RBC(0.48), HGB(0.50), HCT(0.45), NEUT(−0.20)...

**Interpretation:** "Red blood cell volume" — opposite to white cell activity.

**PC3 (11.9% variance):**

Loadings: MONO(0.60), EOS(0.55), LYMPH(0.25)...

**Interpretation:** "Monocyte-Eosinophil axis" — chronic inflammation/allergy.

**Scree Plot Decision:** Elbow at PC3 or PC4 → retain 3-4 components for 73-83% variance.

---

## 🔷 CONCEPT 6: Example 2 — Reflex Measurements (10 Variables)

### Detailed Analysis

**Data:** n=100 individuals, p=10 reflex measurements (reaction times).

**Structure:** Variables come in **blocked pairs** (left/right limbs):
- V1, V2: Right/Left hand (visual stimulus)
- V3, V4: Right/Left hand (auditory stimulus)
- V5, V6: Right/Left foot (visual)
- V7, V8: Right/Left foot (auditory)
- V9, V10: Right/Left hand (tactile)

**Expected Pattern:** Within-pair correlations high (r ≈ 0.8), between-pair lower (r ≈ 0.3-0.5).

**PC1 (35% variance):** "General reflex speed"
- All loadings positive, roughly equal (0.3-0.35)
- Represents overall neural processing speed

**PC2 (18% variance):** "Upper vs Lower body"
- V1-V4 (hands): positive loadings
- V5-V8 (feet): negative loadings
- V9-V10 (hands): positive
- Interpretation: Some people have fast hands but slow feet, or vice versa

**PC3 (12% variance):** "Visual/Auditory vs Tactile"
- V1-V8 (visual/auditory): moderate positive
- V9-V10 (tactile): strong negative
- Interpretation: Tactile reflexes dissociate from visual/auditory

**PC4-PC5:** "Left vs Right asymmetry" (within pairs)

**Hierarchy Interpretation:**
The blocked pair structure creates a natural hierarchy:
1. Overall speed (PC1)
2. Body region (PC2)
3. Sensory modality (PC3)
4. Laterality (PC4-5)

This makes physiological sense and validates the PCA structure.

---

# LECTURE 5: INFERENCE — STATISTICAL JUSTIFICATION AND TESTING

---

## 🔷 CONCEPT 7: MLE Justification for Sample PCA

### Explanation
If we assume the data comes from Nₚ(µ, Σ), the sample PCs are the Maximum Likelihood Estimates (MLE) of the population PCs.

**Likelihood Function:**

L(µ, Σ) ∝ |Σ|^(−n/2) exp{−½ Σᵢ (Xᵢ−µ)ᵀΣ⁻¹(Xᵢ−µ)}


**MLE Results:**
- µ̂ = X̄ (sample mean)
- Σ̂ = (n−1)S/n = (1/n)Σ(Xᵢ−X̄)(Xᵢ−X̄)ᵀ

**Eigen-decomposition of Σ̂:**
Since Σ̂ is proportional to S, it has the same eigenvectors as S, and eigenvalues scaled by (n−1)/n.

**Implication:** Sample PCs êₖ are MLEs of population PCs eₖ (up to sign ambiguity). As n → ∞, êₖ → eₖ almost surely.

---

## 🔷 CONCEPT 8: Testing the Number of Components to Retain

### Explanation
How many PCs are "significant"? We test whether the smallest (p−k) eigenvalues are equal (indicating isotropic noise).

**Hypothesis:**

H₀: λₖ₊₁ = λₖ₊₂ = ... = λₚ (remaining eigenvalues equal)
H₁: At least two of the trailing eigenvalues differ


**Test Statistic (Bartlett's Test):**

Λ = (arithmetic mean of last m eigenvalues) / (geometric mean of last m eigenvalues)
  = (λ̂ₖ₊₁ + ... + λ̂ₚ)/m / (λ̂ₖ₊₁ × ... × λ̂ₚ)^(1/m)


**Or using log form:**

T = −(n−1 − (2p+4m+11)/6) × ln(Λ) ~ χ² with (m−1)(m+2)/2 df

where m = p − k (number of eigenvalues being tested for equality).

### Detailed Example: Blood Chemistry (p=8)

**Testing if last 4 eigenvalues are equal (k=4 retained, m=4):**

| PC | Eigenvalue λ̂ |
|----|---------------|
| 5 | 0.55 |
| 6 | 0.35 |
| 7 | 0.27 |
| 8 | 0.22 |

**Calculate:**

Arithmetic mean = (0.55+0.35+0.27+0.22)/4 = 0.3475
Geometric mean = (0.55×0.35×0.27×0.22)^(1/4) = 0.312

Λ = 0.3475/0.312 = 1.114
ln(Λ) = 0.108

Test statistic T:
n=180, p=8, m=4
Correction factor = 180−1 − (16+16+11)/6 = 179 − 43/6 = 179 − 7.17 = 171.83

T = 171.83 × 0.108 = 18.56

Degrees of freedom = (4−1)(4+2)/2 = 3×6/2 = 9

Critical value χ²₉(0.05) = 16.92


**Decision:** T = 18.56 > 16.92 → **Reject H₀**

**Conclusion:** The last 4 eigenvalues are not all equal; we might need to retain more than 4 components, or at least PC5 is significant.

**Testing last 3 (m=3):** λ₆, λ₇, λ₈

Arithmetic mean = 0.280
Geometric mean = 0.275
Λ = 1.018, ln(Λ) = 0.018
df = (2)(5)/2 = 5
Critical χ²₅ = 11.07
T ≈ small → Fail to reject


**Conclusion:** PCs 6,7,8 may be considered "noise" level (isotropic). Retain first 5 components.

---

## 📌 Master Summary Table

| Concept | Formula/Key Point | When to Use |
|---------|-------------------|-------------|
| **Sample Mean** | X̄ = (1/n)ΣXᵢ | Centering data before PCA |
| **Sample Covariance** | S = (1/(n−1))X̃ᵀX̃ | Covariance PCA (same scales) |
| **Sample Correlation** | R = D⁻¹/²SD⁻¹/² | Correlation PCA (different scales) |
| **PC Definition** | Ŷₖ = êₖᵀ(X−X̄) | Linear combination with max variance |
| **Variance of PC** | Var(Ŷₖ) = λ̂ₖ | Equal to k-th eigenvalue |
| **Proportion Variance** | λ̂ₖ/tr(S) or λ̂ₖ/p | For correlation matrix |
| **Correlation with PC** | êₖᵢ√λ̂ₖ/√sᵢᵢ | Interpreting variable importance |
| **Covariance vs Correlation** | Covariance dominated by large variances | Use correlation when variances differ >10× |
| **MLE Justification** | Sample PCs are MLEs under normality | Theoretical foundation |
| **Bartlett's Test** | Test equality of trailing eigenvalues | Deciding how many PCs to retain |

---

## 🔗 The Complete PCA Workflow


1. DATA PREPARATION
   ├── Check scales of variables
   ├── Decide: Covariance (similar scales) or Correlation (different scales)
   └── Center data (subtract mean)

2. EIGENDECOMPOSITION
   ├── Compute S or R
   ├── Find eigenvalues λ̂₁ ≥ λ̂₂ ≥ ... ≥ λ̂ₚ
   └── Find eigenvectors ê₁, ê₂, ..., êₚ

3. INTERPRETATION
   ├── Scree plot (elbow method)
   ├── Variance proportions (Theorem 2)
   ├── Correlations with variables (Theorem 3)
   └── Biological/theoretical meaning of loadings

4. VALIDATION
   ├── Bartlett's test (significant components)
   ├── Cross-validation (stability)
   └── Check for outliers via Mahalanobis distance

