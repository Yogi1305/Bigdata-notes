# 📘 Complete Guide: Dimensionality Reduction, PCA & Matrix Methods (NPTEL Module)

---

## 🔷 CONCEPT 1: High-Dimensional Data & Curse of Dimensionality

### Explanation
When datasets have thousands of features (columns), analysis becomes computationally expensive and statistically unreliable. As dimensions grow, data points become increasingly sparse in the vast space — this is the **"curse of dimensionality."**

### Detailed Example: Gene Expression Data
**Scenario:** Patient data with 10,000 gene expression readings per patient, but only 100 patients.

**The Problem:**
- Each patient exists as a point in 10,000-dimensional space
- With only 100 points, they are essentially isolated — no "nearby" patients to compare
- Distance-based algorithms (KNN, clustering) become meaningless because all distances become similar

**Visual Intuition:**
```
2D space: 100 points fill the space reasonably
    • •    •
  •   ••     •
    •  • • •

10000D space: 100 points are isolated dots in vast emptiness
    •                          •
                      •
           •
```

**Key Impacts:**
| Impact | Explanation |
|--------|-------------|
| Overfitting | Models memorize noise rather than learn patterns |
| Poor generalization | Fails on new, unseen patients |
| Visualization impossibility | Humans can only perceive 2D/3D |
| Computational explosion | Operations scale as O(p²) or worse |
| Data sparsity | "Effective sample size" shrinks exponentially |

**Mathematical Insight:** In p dimensions, to maintain the same data density, you need n ∝ 2^p samples — impossible for large p.

---

## 🔷 CONCEPT 2: Dimensionality Reduction

### Explanation
The process of reducing the number of features while preserving as much important information as possible. It simplifies datasets, speeds up computation, reduces overfitting, and enables visualization.

### Detailed Example: House Price Prediction

**Original Features (100 total):**
- Size (sq ft), Bedrooms, Bathrooms, Age, Lot size, Garage spaces, Distance to school, Crime rate, Income in zip code, ... [90 more]

**Problem:** Many features are **correlated:**
- Bigger houses → more bedrooms, more bathrooms
- Wealthy zip codes → better schools, lower crime

**Dimensionality Reduction Approach:**

```
Step 1: Find correlated groups
    Group A: Size, Bedrooms, Bathrooms, Garage → "House Capacity"
    Group B: School rating, Crime, Income → "Neighborhood Quality"
    Group C: Age, Renovation year → "Property Condition"

Step 2: Create "super-features" (principal components)
    PC1 = 0.6×Size + 0.5×Bedrooms + 0.4×Bathrooms + ... (House Capacity)
    PC2 = 0.7×Income + 0.6×School − 0.3×Crime (Neighborhood Quality)
    PC3 = ...

Step 3: Use 10 PCs instead of 100 original features
    → 90% reduction in dimensions
    → 95% of variance preserved
```

**Benefits Achieved:**
| Before | After |
|--------|-------|
| 100 features | 10 features |
| Risk of overfitting | Better generalization |
| Cannot visualize | Can plot in 2D/3D |
| Slow training | Fast computation |
| Hard to interpret | Clear "capacity/quality/condition" story |

---

## 🔷 CONCEPT 3: Data Centering

### Explanation
Before PCA, data must be **centered** by subtracting the population mean (µ) from each observation: **X̃ = X − µ**. This shifts the origin to the center of the data cloud, ensuring variance is measured relative to the true center, not some arbitrary point.

### Detailed Example: Exam Score Centering

**Raw Scores:**
| Student | Math | Science | English |
|---------|------|---------|---------|
| A | 85 | 78 | 82 |
| B | 55 | 62 | 58 |
| C | 70 | 70 | 70 |
| D | 90 | 85 | 88 |
| E | 60 | 65 | 62 |

**Calculate Means:**
- µ_Math = (85+55+70+90+60)/5 = 72
- µ_Science = (78+62+70+85+65)/5 = 72
- µ_English = (82+58+70+88+62)/5 = 72

**Centered Data (X̃ = X − µ):**
| Student | Math | Science | English |
|---------|------|---------|---------|
| A | +13 | +6 | +10 |
| B | −17 | −10 | −14 |
| C | −2 | −2 | −2 |
| D | +18 | +13 | +16 |
| E | −12 | −7 | −10 |

**Why This Matters:**

```
Before centering: Origin at (0,0,0) — meaningless
    D at (90,85,88)
    B at (55,62,58)
    Distance from origin dominated by arbitrary zero point

After centering: Origin at mean student (72,72,72)
    D at (+18,+13,+16) → "above average in all"
    B at (−17,−10,−14) → "below average in all"
    C at (−2,−2,−2) → "average student"
    A at (+13,+6,+10) → "strong in math"

Now distances and variances measure meaningful deviations!
```

**Key Property:** After centering, the new mean is zero: E[X̃] = 0.

---

## 🔷 CONCEPT 4: Covariance Matrix (Σ)

### Explanation
A p×p matrix capturing how every pair of features varies together. Diagonal entries give each feature's variance; off-diagonal entries give covariance between pairs.

### Detailed Example: Height, Weight, Age

**Dataset (centered):**
| Person | Height (in) | Weight (lb) | Age (yr) |
|--------|-------------|-------------|----------|
| 1 | +2 | +15 | −5 |
| 2 | −3 | −20 | +2 |
| 3 | +1 | +8 | 0 |
| 4 | 0 | −5 | +3 |

**Calculate Covariances:**
- Var(Height) = (4+9+1+0)/4 = 3.5
- Var(Weight) = (225+400+64+25)/4 = 178.5
- Var(Age) = (25+4+0+9)/4 = 9.5
- Cov(Height,Weight) = (2×15 + (−3)×(−20) + 1×8 + 0×(−5))/4 = (30+60+8+0)/4 = 24.5
- Cov(Height,Age) = (2×(−5) + (−3)×2 + 1×0 + 0×3)/4 = (−10−6+0+0)/4 = −4
- Cov(Weight,Age) = (15×(−5) + (−20)×2 + 8×0 + (−5)×3)/4 = (−75−40+0−15)/4 = −32.5

**Covariance Matrix:**
```
        Height   Weight    Age
      ┌  3.5     24.5    −4   ┐
Σ =   │ 24.5    178.5   −32.5 │
      └ −4      −32.5     9.5 ┘
```

**Interpretation:**
| Entry | Meaning |
|-------|---------|
| Σ₁₁ = 3.5 | Height varies with SD ≈ 1.87 inches |
| Σ₂₂ = 178.5 | Weight varies with SD ≈ 13.36 lbs |
| Σ₁₂ = 24.5 | **Positive:** Taller people tend to weigh more |
| Σ₁₃ = −4 | **Negative:** Older people in this sample tend to be shorter (maybe children + adults?) |
| Σ₂₃ = −32.5 | **Negative:** Older people tend to weigh less (young adults gaining weight?) |

**Key Formula:** Σ = E[(X−µ)(X−µ)ᵀ] = E[X̃X̃ᵀ]

---

## 🔷 CONCEPT 5: Bivariate Normal Distribution

### Explanation
A probability distribution for two correlated variables. Density contours form **ellipses** whose shape and tilt are determined by the covariance matrix Σ.

### Detailed Example: Height vs Weight

**Parameters:**
- µ = [67, 150] (mean height 67 inches, weight 150 lbs)
- Σ = [[9, 45], [45, 400]] (variances 9 and 400, covariance 45)
- Correlation ρ = 45/√(9×400) = 45/60 = 0.75

**Visual Contours:**

```
                    Weight (lb)
                       ↑
    ρ = −0.8          200├    ╱──╲    ρ = +0.8
    (negative)        175├   ╱    ╲      (positive)
         ╲╱         150├──●────────     (strong)
        ╱  ╲        125├   ╲    ╱
       ╱    ╲       100├    ╲──╱
      ─────────→        └──┬──┬──┬──┬──┬→ Height (in)
      60  62  64  66  68  70  72  74

    ρ = 0 (independent)
         ◯◯◯
        ◯   ◯   (circular/axis-aligned ellipses)
       ◯  ●  ◯
        ◯   ◯
         ◯◯◯
```

**Ellipse Geometry:**
| Correlation | Shape | Interpretation |
|-------------|-------|----------------|
| ρ = +0.9 | Tall thin ellipse, tilted up-right | Strong positive: tall heavy, short light |
| ρ = 0 | Perfect circle | No relationship: all weight-height combos equally likely at same Mahalanobis distance |
| ρ = −0.9 | Tall thin ellipse, tilted up-left | Strong negative: tall light, short heavy |
| ρ = 0.5 | Fat ellipse, tilted | Moderate positive relationship |

**Density Formula:**
f(x₁,x₂) = (1/2π|Σ|½) exp(−½(x−µ)ᵀΣ⁻¹(x−µ))

---

## 🔷 CONCEPT 6: Matrix as Linear Transformation

### Explanation
A matrix A (m×n) is a **function** that takes input vector x ∈ ℝⁿ and produces output y = Ax ∈ ℝᵐ. It transforms space through rotation, stretching, shearing, and/or projection.

### Detailed Example: Multiple Transformation Matrices

**Matrix 1: Scaling (Stretching)**
```
        ┌2  0┐
A =     └0  3┘

Input: x = [1, 1]ᵀ
Output: y = Ax = [2×1 + 0×1, 0×1 + 3×1]ᵀ = [2, 3]ᵀ

Effect: x-coordinate ×2, y-coordinate ×3
        Unit square → Rectangle 2×3
```

**Matrix 2: Rotation by θ = 30°**
```
        ┌ cos(30°)  −sin(30°)┐   ┌√3/2   −1/2┐
R =     └ sin(30°)   cos(30°)┘ = └1/2    √3/2┘

Input: x = [1, 0]ᵀ (point on x-axis)
Output: Rx = [√3/2, 1/2]ᵀ ≈ [0.866, 0.5]ᵀ

Effect: Rotated 30° counterclockwise, length preserved
```

**Matrix 3: Projection onto x-axis**
```
        ┌1  0┐
P =     └0  0┘

Input: x = [3, 4]ᵀ
Output: Px = [3, 0]ᵀ

Effect: Flattens everything onto x-axis (loses y-information!)
```

**Matrix 4: Shear**
```
        ┌1  1┐
S =     └0  1┘

Input: x = [1, 1]ᵀ
Output: Sx = [2, 1]ᵀ

Effect: Slants the square into a parallelogram
        Top edge shifts right by its height
```

**Composition:** Applying A then B is matrix product BA (note order!).

---

## 🔷 CONCEPT 7: Eigenvalues & Eigenvectors

### Explanation
For square matrix A, a **non-zero vector v** is an **eigenvector** if applying A only **scales** it (no rotation): **Av = λv**, where λ is the **eigenvalue** (scaling factor).

### Detailed Example: Social Media Spread Model

**Scenario:** Content spreads between Twitter and Instagram.

**Spread Matrix A:** If content starts with amounts [T, I], next cycle becomes:
```
        ┌0.6  0.2┐        Twitter keeps 60%, gets 20% from IG
A =     └0.4  0.8┘        IG keeps 80%, gets 40% from Twitter
```

**Finding Eigenvectors:**

**Eigenvalue λ₁ = 1:**
Solve (A − I)v = 0:
```
┌−0.4  0.2┐┌v₁┐ = 0
└ 0.4 −0.2┘└v₂┘

−0.4v₁ + 0.2v₂ = 0  →  v₂ = 2v₁
Eigenvector: v₁ = [1, 2]ᵀ (or any multiple)
Check: A[1,2]ᵀ = [0.6+0.4, 0.4+1.6]ᵀ = [1, 2]ᵀ = 1×[1,2]ᵀ ✓
```

**Interpretation:** The ratio [1 Twitter : 2 Instagram] is **stable** — if content starts in this proportion, it stays in this proportion forever (equilibrium).

**Eigenvalue λ₂ = 0.4:**
Eigenvector: v₂ = [1, −1]ᵀ
Check: A[1,−1]ᵀ = [0.6−0.2, 0.4−0.8]ᵀ = [0.4, −0.4]ᵀ = 0.4×[1,−1]ᵀ ✓

**Interpretation:** The "difference mode" [1, −1] shrinks by 40% each cycle. Over time, this component dies out, leaving only the stable [1, 2] ratio.

**Long-term behavior:** Any starting content [T₀, I₀] = a[1,2] + b[1,−1] evolves to a[1,2] + (0.4)^n b[1,−1] → a[1,2] as n→∞. The system converges to 1/3 Twitter, 2/3 Instagram!

**Key Properties:**
| Property | Statement |
|----------|-----------|
| Scaling | cv is also eigenvector for any scalar c |
| Sum (same λ) | v₁ + v₂ also eigenvector if same eigenvalue |
| Distinct λ | Eigenvectors for distinct eigenvalues are linearly independent |
| Symmetric A | All eigenvalues real, eigenvectors orthogonal |

---

## 🔷 CONCEPT 8: Eigenspace

### Explanation
For fixed eigenvalue λ, the **eigenspace E_λ** is the set of all vectors v satisfying Av = λv. It includes the zero vector plus all eigenvectors for λ. Closed under addition and scalar multiplication.

### Detailed Example: Rotation Matrix

**Matrix R (90° rotation in 3D around z-axis):**
```
        ┌0  −1  0┐
R =     │1   0  0│
        └0   0  1┘
```

**Eigenvalue λ = 1:**
Solve Rv = v:
```
−v₂ = v₁,  v₁ = v₂,  v₃ = v₃
→ v₁ = v₂ = 0, v₃ free
```

Eigenspace E₁ = {[0, 0, z]ᵀ : z ∈ ℝ} = **z-axis**

**Geometric meaning:** Points on the z-axis don't move when rotated around z-axis — they are fixed!

**Eigenvalues λ = ±i (complex):**
For 2D rotation [ [0,−1], [1,0] ], eigenvalues are i and −i. **No real eigenspace** — no real direction is preserved under 90° rotation!

**Dimension of Eigenspace (Geometric Multiplicity):**
- Can be 1 (single line), 2 (plane), etc.
- Never exceeds algebraic multiplicity (root multiplicity in characteristic polynomial)

---

## 🔷 CONCEPT 9: Characteristic Polynomial & Equation

### Explanation
To find eigenvalues, solve **det(A − tI) = 0**. This degree-n polynomial in t has roots equal to the n eigenvalues (counting multiplicities, possibly complex).

### Detailed Example 1: Simple 2×2

**A = [[2, 1], [1, 2]]**

```
A − tI = ┌2−t   1 ┐
         └ 1   2−t┘

det(A−tI) = (2−t)(2−t) − 1 = 4 − 4t + t² − 1 = t² − 4t + 3 = 0
```

Roots: t = (4 ± √(16−12))/2 = (4 ± 2)/2 → **t = 1 or t = 3**

**Eigenvalues:** λ₁ = 3, λ₂ = 1

---

### Detailed Example 2: Rotation Matrix (No Real Eigenvalues)

**A = [[0, −1], [1, 0]]** (90° rotation)

```
det(A−tI) = det┌−t  −1┐ = (−t)(−t) − (−1)(1) = t² + 1 = 0
              └ 1  −t┘
```

Roots: **t = ±i** (purely imaginary!)

**Interpretation:** No real eigenvector exists — no direction is preserved. This is why continuous rotation never aligns with original orientation.

---

### Detailed Example 3: 3×3 Matrix

**A = [[2, −1, 0], [−1, 2, −1], [0, −1, 2]]**

```
det(A−tI) = det┌2−t  −1    0 ┐
              │−1   2−t   −1 │
              └ 0    −1   2−t┘

= (2−t)[(2−t)² − 1] + 1[−(2−t)] + 0
= (2−t)(t² − 4t + 3) − (2−t)
= (2−t)(t² − 4t + 2) = ... actually let's expand:

= (2−t)³ − 2(2−t) = (2−t)[(2−t)² − 2] = (2−t)(4−4t+t²−2) = (2−t)(t²−4t+2)
```

Wait, correct calculation:
```
= (2−t)[(2−t)² − 1] − (−1)[−(2−t)] 
= (2−t)[(2−t)² − 1] − (2−t)
= (2−t)[(2−t)² − 2]
= (2−t)[t² − 4t + 4 − 2]
= (2−t)(t² − 4t + 2) = 0
```

Roots: t = 2, or t = (4 ± √(16−8))/2 = (4 ± 2√2)/2 = **2 ± √2**

**Eigenvalues:** λ₁ = 2 + √2 ≈ 3.414, λ₂ = 2, λ₃ = 2 − √2 ≈ 0.586

**Key Insights:**
| Property | Meaning |
|----------|---------|
| det(A) = product of eigenvalues | 3.414 × 2 × 0.586 ≈ 4 = det(A) |
| tr(A) = sum of eigenvalues | 3.414 + 2 + 0.586 = 6 = 2+2+2 |
| Real symmetric | All eigenvalues real ✓ |
| Positive definite | All eigenvalues > 0 ✓ |

---

## 🔷 CONCEPT 10: Orthonormal Vectors

### Explanation
A set {v₁, v₂, …, vₖ} is **orthonormal** if: (1) every pair is perpendicular (dot product = 0), and (2) every vector has unit length (‖vᵢ‖ = 1).

### Detailed Example: Multiple Orthonormal Sets

**Set 1: Standard Basis (R³)**
```
e₁ = [1, 0, 0]ᵀ,  e₂ = [0, 1, 0]ᵀ,  e₃ = [0, 0, 1]ᵀ

Checks:
• e₁·e₂ = 0, e₁·e₃ = 0, e₂·e₃ = 0 ✓ (orthogonal)
• ‖e₁‖ = ‖e₂‖ = ‖e₃‖ = 1 ✓ (normalized)
```

**Set 2: Rotated Basis (45° in xy-plane)**
```
u₁ = [1/√2,  1/√2, 0]ᵀ  ≈ [0.707, 0.707, 0]ᵀ
u₂ = [1/√2, −1/√2, 0]ᵀ  ≈ [0.707, −0.707, 0]ᵀ
u₃ = [0,     0,    1]ᵀ

Checks:
• u₁·u₂ = ½ − ½ + 0 = 0 ✓
• ‖u₁‖² = ½ + ½ + 0 = 1 ✓
• u₃ same as e₃, perpendicular to both
```

**Set 3: Verification of Non-Orthonormal**
```
v₁ = [1, 1, 0]ᵀ,  v₂ = [1, 2, 0]ᵀ

Problems:
• Not orthogonal: v₁·v₂ = 1+2+0 = 3 ≠ 0
• Not normalized: ‖v₁‖ = √2 ≠ 1, ‖v₂‖ = √5 ≠ 1
```

**Creating Orthonormal Set via Normalization:**
From v₁, v₂ above:
```
u₁ = v₁/‖v₁‖ = [1/√2, 1/√2, 0]ᵀ

w₂ = v₂ − (v₂·u₁)u₁ = [1,2,0] − 3[1/√2,1/√2,0]/√2
    = [1,2,0] − [1.5, 1.5, 0] = [−0.5, 0.5, 0]

u₂ = w₂/‖w₂‖ = [−1/√2, 1/√2, 0]ᵀ
```

Now {u₁, u₂} is orthonormal!

---

## 🔷 CONCEPT 11: Diagonalization

### Explanation
Matrix A is **diagonalizable** if A = PDP⁻¹ where P has eigenvectors as columns and D is diagonal with eigenvalues. This makes matrix powers trivial: Aⁿ = PDⁿP⁻¹.

### Detailed Example: Computing A¹⁰⁰

**Matrix A = [[4, 1], [2, 3]]**

**Step 1: Find eigenvalues**
```
det(A−tI) = (4−t)(3−t) − 2 = 12 − 7t + t² − 2 = t² − 7t + 10 = (t−5)(t−2) = 0
λ₁ = 5, λ₂ = 2
```

**Step 2: Find eigenvectors**
For λ₁ = 5: (A−5I)v = 0 → [[−1, 1], [2, −2]] → v₁ = [1, 1]ᵀ
For λ₂ = 2: (A−2I)v = 0 → [[2, 1], [2, 1]] → v₂ = [1, −2]ᵀ

**Step 3: Form P and D**
```
        ┌1   1 ┐         ┌5  0┐
P =     │      │,   D =  │    │
        └1  −2┘          └0  2┘
```

**Step 4: Verify A = PDP⁻¹**
```
P⁻¹ = (1/(−2−1)) ┌−2  −1┐ = ┌2/3   1/3┐
                 └−1   1┘   └1/3  −1/3┘

PDP⁻¹ = ┌1  1┐┌5 0┐┌2/3  1/3┐ = ┌5  2┐┌2/3  1/3┐ = ┌4  1┐ = A ✓
        │    ││    ││         │      ││        │    │
        └1 −2┘└0 2┘└1/3 −1/3┘   └5 −4┘└1/3 −1/3┘   └2  3┘
```

**Step 5: Compute A¹⁰⁰**
```
D¹⁰⁰ = ┌5¹⁰⁰     0 ┐
       └  0    2¹⁰⁰┘

A¹⁰⁰ = PD¹⁰⁰P⁻¹ = ┌1  1┐┌5¹⁰⁰    0   ┐┌2/3  1/3┐
                  │    ││            ││         │
                  └1 −2┘└  0   2¹⁰⁰┘└1/3 −1/3┘

     = (1/3)┌1  1┐┌2·5¹⁰⁰      5¹⁰⁰    ┐
            │    ││                     │
            └1 −2┘└  2¹⁰⁰    −2¹⁰⁰    ┘

     = (1/3)┌2·5¹⁰⁰+2¹⁰⁰     5¹⁰⁰−2¹⁰⁰┐
            │                             │
            └2·5¹⁰⁰−2·2¹⁰⁰   5¹⁰⁰+2·2¹⁰⁰┘
```

Without diagonalization, this would require 99 matrix multiplications!

---

### Detailed Example 2: Symmetric Matrix (Spectral Theorem)

**A = [[5, 2], [2, 2]]** (symmetric, so diagonalizable with orthogonal P)

Eigenvalues: λ = 6, 1
Eigenvectors: [2, 1]ᵀ and [1, −2]ᵀ — **already orthogonal!**

Normalized:
```
        ┌2/√5   1/√5┐
Q =     │           │  (QᵀQ = I, so Q⁻¹ = Qᵀ)
        └1/√5  −2/√5┘
```

A = QDQᵀ where D = diag(6, 1)

**Advantage:** Qᵀ is easier than computing P⁻¹!

---

## 🔷 CONCEPT 12: Positive Definite Matrix

### Explanation
Real symmetric A is **positive definite** if xᵀAx > 0 for all non-zero x. Equivalently: all eigenvalues > 0.

### Detailed Example: Covariance Matrix

**Data:** Heights (in) and weights (lb) of 4 people, centered:
```
X̃ = ┌ 2   15┐
    │−3  −20│
    │ 1    8│
    └ 0   −5┘
```

**Covariance matrix:**
```
        1    ┌14   105┐   ┌3.5   26.25┐
Σ = ───── X̃ᵀX̃ = │        │ = │           │
      3    └105  850┘   └26.25 212.5 ┘


**Check positive definiteness:**

**Method 1: Eigenvalues**
`
det(Σ−tI) = (3.5−t)(212.5−t) − 26.25² = t² − 216t + 743.75 − 689.06
          = t² − 216t + 54.69 = 0

t = (216 ± √(46656 − 218.75))/2 ≈ (216 ± 215.5)/2
λ₁ ≈ 215.75, λ₂ ≈ 0.25  →  both positive! ✓


**Method 2: Principal minors**
- det([3.5]) = 3.5 > 0 ✓
- det(Σ) = 3.5×212.5 − 26.25² ≈ 743.75 − 689.06 = 54.7 > 0 ✓

**Method 3: Direct xᵀΣx test**
For any [a,b] ≠ [0,0]:

xᵀΣx = 3.5a² + 52.5ab + 212.5b²
     = 3.5(a + 7.5b)² + (212.5 − 3.5×56.25)b²
     = 3.5(a + 7.5b)² + 15.6b² > 0 unless a=b=0 ✓


**Physical meaning:** Variance is always non-negative; Σ represents "spread" which can't be negative in any direction.

**Not positive definite example:** A = [[1, 2], [2, 1]] has eigenvalues 3 and −1. For x = [1, −1]ᵀ: xᵀAx = 1 − 2 − 2 + 1 = −2 < 0.

---

## 🔷 CONCEPT 13: Spectral Theorem

### Explanation
Every real symmetric matrix can be **orthogonally diagonalized**: **A = QDQᵀ** where Q has orthonormal columns (QQᵀ = I). Two key facts: (1) symmetric matrices have real eigenvalues, (2) eigenvectors for distinct eigenvalues are orthogonal.

### Detailed Example: Complete Spectral Decomposition

**A = [[3, 2, 0], [2, 3, 0], [0, 0, 1]]** (block diagonal, symmetric)

**Step 1: Eigenvalues**

det(A−tI) = (1−t) × det┌3−t  2 ┐ = (1−t)[(3−t)² − 4]
                       └ 2  3−t┘
         = (1−t)(t² − 6t + 5) = (1−t)(t−5)(t−1) = (1−t)²(t−5)

λ₁ = 5, λ₂ = 1 (multiplicity 2)

**Step 2: Eigenvectors**

For λ₁ = 5:

┌−2  2  0┐    Row reduce: ┌1  −1  0┐
│ 2 −2  0│  →             │0   0  0│
└ 0  0 −4┘                └0   0  1┘
v₁ = [1, 1, 0]ᵀ, normalized: q₁ = [1/√2, 1/√2, 0]ᵀ


For λ₂ = 1:

┌2  2  0┐    Row reduce: ┌1  1  0┐
│2  2  0│  →            │0  0  0│
└0  0  0┘                └0  0  0┘
Eigenspace: a[−1, 1, 0]ᵀ + b[0, 0, 1]ᵀ

Choose orthonormal basis:
q₂ = [−1/√2, 1/√2, 0]ᵀ  (perpendicular to q₁: dot = −½+½+0=0 ✓)
q₃ = [0, 0, 1]ᵀ           (perpendicular to both: dots = 0 ✓)


**Step 3: Assemble Q and D**

        ┌1/√2  −1/√2   0┐
Q =     │1/√2   1/√2   0│,    D = diag(5, 1, 1)
        └  0      0    1┘


**Verification:** QDQᵀ should recover A. Check QᵀQ = I:
- Column norms: ½+½+0=1, ½+½+0=1, 0+0+1=1 ✓
- Dot products: q₁·q₂ = −½+½+0=0, q₁·q₃=0, q₂·q₃=0 ✓

**Why Spectral Theorem Matters for PCA:**
| Feature | Implication |
|---------|-------------|
| Real eigenvalues | Variance amounts are real numbers |
| Orthogonal eigenvectors | Principal components are uncorrelated |
| Q is rotation | PCA = rotate to align with natural axes |
| D shows importance | Eigenvalues = variance in each PC direction |



## 🔷 CONCEPT 14: Gram–Schmidt Process

### Explanation
Given any linearly independent set, Gram–Schmidt constructs an orthonormal set with the same span. Iterative: subtract projections onto all previous vectors, then normalize.

### Detailed Example: Complete Gram–Schmidt

**Input vectors (R³):**

v₁ = [1, 1, 0]ᵀ,  v₂ = [1, 0, 1]ᵀ,  v₃ = [0, 1, 1]ᵀ


**Step 1: u₁ from v₁**

‖v₁‖ = √(1+1+0) = √2
u₁ = v₁/√2 = [1/√2, 1/√2, 0]ᵀ ≈ [0.707, 0.707, 0]ᵀ


**Step 2: Orthogonalize v₂ against u₁**

Projection of v₂ onto u₁: (v₂·u₁)u₁ = (1/√2)[1/√2, 1/√2, 0] = [0.5, 0.5, 0]

w₂ = v₂ − projection = [1,0,1] − [0.5,0.5,0] = [0.5, −0.5, 1]

Normalize: ‖w₂‖ = √(0.25+0.25+1) = √1.5 = √(3/2)
u₂ = w₂/√1.5 = [0.5/√1.5, −0.5/√1.5, 1/√1.5]
   = [1/√6, −1/√6, 2/√6] ≈ [0.408, −0.408, 0.816]


**Step 3: Orthogonalize v₃ against u₁ and u₂**

Projection onto u₁: (v₃·u₁)u₁ = (1/√2)[1/√2,1/√2,0] = [0.5, 0.5, 0]

Projection onto u₂: (v₃·u₂)u₂ = (1/√6)[1/√6,−1/√6,2/√6] = [1/6, −1/6, 2/6]

w₃ = v₃ − proj₁ − proj₂ = [0,1,1] − [0.5,0.5,0] − [1/6,−1/6,1/3]
   = [−2/3, 2/3, 2/3]

Normalize: ‖w₃‖ = √(4/9+4/9+4/9) = √(12/9) = 2/√3
u₃ = [−2/3, 2/3, 2/3] / (2/√3) = [−1/√3, 1/√3, 1/√3] ≈ [−0.577, 0.577, 0.577]


**Final Orthonormal Set:**

u₁ = [0.707,  0.707, 0   ]ᵀ
u₂ = [0.408, −0.408, 0.816]ᵀ  
u₃ = [−0.577, 0.577, 0.577]ᵀ


**Verification:**
| Check | Result |
|-------|--------|
| ‖u₁‖ | √(0.5+0.5+0) = 1 ✓ |
| ‖u₂‖ | √(0.167+0.167+0.667) ≈ 1 ✓ |
| ‖u₃‖ | √(0.333+0.333+0.333) ≈ 1 ✓ |
| u₁·u₂ | 0.289 − 0.289 + 0 = 0 ✓ |
| u₁·u₃ | −0.408 + 0.408 + 0 = 0 ✓ |
| u₂·u₃ | −0.236 − 0.236 + 0.471 ≈ 0 ✓ |

**Span preservation:** Any [x,y,z] can be written as a₁u₁ + a₂u₂ + a₃u₃.

---

## 🔷 CONCEPT 15: Principal Component Analysis (PCA) — Full Pipeline

### Explanation
PCA rotates data to a new coordinate system where axes (principal components) align with directions of maximum variance, and all components are uncorrelated.

### Detailed Example: 3D Data Reduction to 2D

**Covariance Matrix:**

        ┌ 1   −2    0┐
Σ =     │−2    5    0│
        └ 0    0    2┘


**Step 1: Find eigenvalues**

det(Σ−tI) = (2−t) × det┌1−t  −2 ┐ = (2−t)[(1−t)(5−t) − 4]
                       └−2  5−t┘
          = (2−t)[t² − 6t + 5 − 4] = (2−t)(t² − 6t + 1) = 0


From t² − 6t + 1 = 0: t = (6 ± √32)/2 = 3 ± 2√2 ≈ 5.83, 0.17

**Eigenvalues:** λ₁ ≈ 5.83, λ₂ = 2, λ₃ ≈ 0.17

**Total variance:** tr(Σ) = 1 + 5 + 2 = 8 = 5.83 + 2 + 0.17 ✓

**Step 2: Find eigenvectors**

For λ₁ = 5.83 ≈ 3+2√2:

┌−4.83  −2     0┐    Solve: −4.83q₁ = 2q₂ → q₂ ≈ −2.42q₁
│ −2   −0.83   0│    And q₃ = 0 (from third row)
└  0     0   −3.83┘
v₁ ≈ [1, −2.42, 0]ᵀ → normalized: q₁ ≈ [0.38, −0.92, 0]ᵀ


For λ₂ = 2: obvious from matrix structure — [0, 0, 1]ᵀ (the z-direction has its own variance)

For λ₃ = 0.17: perpendicular to both, ≈ [0.92, 0.38, 0]ᵀ

**Step 3: Principal Components**

| PC | Eigenvalue | Direction | Variance % |
|----|-----------|-----------|-----------|
| 1 | 5.83 | [0.38, −0.92, 0] — "height vs width" contrast | 5.83/8 = **73%** |
| 2 | 2 | [0, 0, 1] — pure "depth" | 2/8 = **25%** |
| 3 | 0.17 | [0.92, 0.38, 0] — "height+width" sum | 0.17/8 = **2%** |

**Step 4: Dimensionality Reduction**

Keep only PC1 and PC2 → capture **98% of variance** with 2/3 of dimensions!

**Original vs Transformed:**

Original point x = [x₁, x₂, x₃]ᵀ

PC scores: y₁ = 0.38x₁ − 0.92x₂        (contrast component)
           y₂ = x₃                     (depth component)
           y₃ = 0.92x₁ + 0.38x₂        (sum component — discard)

Reduced representation: [y₁, y₂] captures 98% of information!


**Visualization:** Plot all data points in (y₁, y₂) coordinates — effectively a 2D projection that preserves nearly all structure.

---

## 🔷 CONCEPT 16: Population PCA

### Explanation
PCA using theoretical population parameters: true mean µ = E[X] and true covariance Σ = Cov(X). The i-th principal component is **Yᵢ = qᵢᵀ(X − µ)** where qᵢ is the i-th eigenvector of Σ.

### Three Key Theorems with Proofs

#### **Theorem 1: Variance and Covariance of PCs**

**Statement:** Var(Yᵢ) = λᵢ and Cov(Yᵢ, Yⱼ) = 0 for i ≠ j

**Proof:**

Var(Yᵢ) = Var(qᵢᵀX̃) = qᵢᵀVar(X̃)qᵢ = qᵢᵀΣqᵢ = qᵢᵀ(λᵢqᵢ) = λᵢqᵢᵀqᵢ = λᵢ

Cov(Yᵢ,Yⱼ) = E[qᵢᵀX̃ · X̃ᵀqⱼ] = qᵢᵀE[X̃X̃ᵀ]qⱼ = qᵢᵀΣqⱼ = qᵢᵀ(λⱼqⱼ) = λⱼ(qᵢ·qⱼ) = 0  ✓

(since eigenvectors of symmetric Σ are orthogonal)

---

#### **Theorem 2: Proportion of Variance Explained**

**Statement:** Proportion by PC k = λₖ / (λ₁ + … + λₚ) = λₖ/tr(Σ)

**Example from before:**
- PC1: 5.83/8 = **73%**
- PC2: 2/8 = **25%**  
- PC3: 0.17/8 = **2%**

Cumulative: PC1+PC2 = **98%**

---

#### **Theorem 3: Correlation Between PC and Original Variable**

**Statement:** Corr(Yᵢ, Xₖ) = qᵢₖ√λᵢ / √σₖₖ

**Interpretation:** How much does original variable k contribute to PC i?

**Example:** In our 3D example, for PC1 (λ₁=5.83, q₁≈[0.38,−0.92,0]):

| Variable | σₖₖ | q₁ₖ | Correlation with PC1 |
|----------|-----|-----|----------------------|
| X₁ (height) | 1 | 0.38 | 0.38×√5.83/√1 ≈ 0.92 |
| X₂ (width) | 5 | −0.92 | −0.92×√5.83/√5 ≈ −0.99 |
| X₃ (depth) | 2 | 0 | 0 |

PC1 is almost perfectly negatively correlated with width, strongly positively with height — a "tall-narrow vs short-wide" contrast!

---

### Detailed Example: Stock Portfolio

**3 assets with covariance:**

        ┌0.04  0.02  0.01┐
Σ =     │0.02  0.03  0.015│ × 100 (percentages squared)
        └0.01 0.015  0.02┘


**Eigenvalues:** λ₁ = 5.5%, λ₂ = 1.8%, λ₃ = 0.7% (total = 8%)

**Interpretation:**
| PC | Eigenvalue | % Variance | Interpretation |
|----|-----------|-----------|----------------|
| 1 | 5.5% | **69%** | "Market factor" — all stocks move together |
| 2 | 1.8% | **22%** | "Tech vs Energy" sector contrast |
| 3 | 0.7% | **9%** | Idiosyncratic noise |

**Investment insight:** A portfolio loading on PC1 is "beta" (market exposure). Loading on PC2 is a sector bet. PC3 is diversifiable risk — can be eliminated.

---

## 🔷 CONCEPT 17: PCA for Multivariate Normal Distribution

### Explanation
When X ~ Nₚ(µ, Σ), constant-density contours are **ellipsoids**: (x−µ)ᵀΣ⁻¹(x−µ) = c². PCA eigenvectors define ellipsoid axes; eigenvalues define axis lengths.

### Detailed Example: Bivariate Normal Geometry

**Parameters:** µ = [0, 0]ᵀ, Σ = [[4, 2], [2, 2]] (correlation ρ ≈ 0.71)

**Eigen-decomposition:**

det(Σ−tI) = (4−t)(2−t) − 4 = t² − 6t + 4 = 0
t = 3 ± √5 ≈ 5.24, 0.76

λ₁ ≈ 5.24:  q₁ ≈ [0.85, 0.52]ᵀ  (major axis, tilted)
λ₂ ≈ 0.76:  q₂ ≈ [−0.52, 0.85]ᵀ (minor axis, perpendicular)


**Ellipsoid at c = 1:**

Points where (x−µ)ᵀΣ⁻¹(x−µ) = 1

In PC coordinates y = Qᵀx:  y₁²/λ₁ + y₂²/λ₂ = 1
                            y₁²/5.24 + y₂²/0.76 = 1

Semi-axes: √5.24 ≈ 2.29 along q₁,  √0.76 ≈ 0.87 along q₂
```

**Visual:**
```
        y₂ (PC2, minor)
           ↑
           │    ╱╲
           │   ╱  ╲  ← ellipse: stretched 2.29× vs 0.87×
           │  ╱    ╲     (aspect ratio ≈ 2.6:1)
           │ ╱      ╲
    ───────┼/────────╲──────→ y₁ (PC1, major)
           │           ╲
           │            ╲
           
Original x₁,x₂ coordinates: ellipse tilted ~32° from horizontal
```

**PCA transforms this to:** Circle in (y₁/√λ₁, y₂/√λ₂) coordinates — whitening the data.

---

## 🔷 CONCEPT 18: PCA on Standardized Variables

### Explanation
When features have different units/scales, standardize first: **Zᵢ = (Xᵢ − µᵢ)/√σᵢᵢ**. Then perform PCA on the **correlation matrix ρ** (covariance of Z).

### Detailed Example: Income vs Age

**Raw data (unscaled):**
| Person | Income ($) | Age (years) |
|--------|-----------|-------------|
| A | 50,000 | 35 |
| B | 30,000 | 25 |
| C | 80,000 | 55 |
| D | 40,000 | 30 |

**Problem:** Income variance ≈ 433 million; age variance ≈ 150. PCA on covariance would find "income direction" as PC1 regardless of actual predictive power!

**Standardization:**
```
Z_income = (Income − 50,000) / 20,833
Z_age = (Age − 36.25) / 12.4
```

**Standardized data:**
| Person | Z_income | Z_age |
|--------|---------|-------|
| A | 0 | −0.1 |
| B | −0.96 | −0.91 |
| C | +1.44 | +1.51 |
| D | −0.48 | −0.5 |

Now both variables have mean 0, variance 1 — **equal footing**.

**Correlation matrix vs Covariance matrix:**

| | Income variance | Age variance | Correlation |
|---|---------------|-------------|-------------|
| Covariance | 433×10⁶ | 150 | 0.95 |
| Correlation | 1 | 1 | 0.95 |

PCA on correlation matrix finds directions based on **relationship strength**, not measurement scale.

**Key difference:**
| Aspect | Covariance PCA | Correlation PCA |
|--------|---------------|-----------------|
| Total variance | tr(Σ) = sum of individual variances | p (number of variables, each = 1) |
| Variance explained | λₖ/tr(Σ) | λₖ/p |
| Sensitive to units? | Yes | No |
| Best when | Variables same units, comparable scales | Mixed units, different scales |



## 📌 Master Summary Table

| Concept | Core Formula | Key Intuition |
|---------|-----------|---------------|
| Curse of dimensionality | n ∝ 2^p for constant density | High dimensions = sparse, isolated data |
| Data centering | X̃ = X − µ | Shift origin to data center |
| Covariance matrix | Σ = E[X̃X̃ᵀ] | How features vary together |
| Bivariate normal | Elliptical contours | Correlation tilts the ellipse |
| Matrix as function | y = Ax | Transformation: rotate, stretch, project |
| Eigenvalue/vector | Av = λv | Special directions that only scale |
| Eigenspace E_λ | {v : Av = λv} | All vectors with same scaling behavior |
| Characteristic equation | det(A−tI) = 0 | Recipe to find eigenvalues |
| Orthonormal | vᵢ·vⱼ = δᵢⱼ | Perpendicular unit vectors |
| Diagonalization | A = PDP⁻¹ | Decompose into simple scalings |
| Spectral theorem | A = QDQᵀ (symmetric) | Always possible for symmetric matrices |
| Positive definite | xᵀAx > 0, λᵢ > 0 | Like a covariance matrix — always "spread" |
| Gram–Schmidt | wₖ = vₖ − Σproj, uₖ = wₖ/‖wₖ‖ | Build orthonormal basis iteratively |
| PCA | Yᵢ = qᵢᵀ(X−µ) | Rotate to variance-maximizing axes |
| Variance explained | λₖ/Σλᵢ | How much information each PC captures |
| Standardized PCA | Z = diag(Σ)⁻½(X−µ) | Equalize feature scales first |

---

## The Unifying Thread

> **The covariance matrix Σ encodes all variance structure. Its eigenvectors (principal components) reveal the natural axes of that structure — letting us compress data with minimal information loss.**

| Step | Mathematical Operation | Geometric Meaning |
|------|------------------------|-------------------|
| Center data | X̃ = X − µ | Shift to origin |
| Find covariance | Σ = X̃ᵀX̃/(n−1) | Measure spread in all directions |
| Eigen-decompose | Σ = QDQᵀ | Find axes of the variance ellipsoid |
| Rotate | Y = QᵀX̃ | Align coordinates with natural axes |
| Reduce | Keep top k PCs | Project onto most informative subspace |
