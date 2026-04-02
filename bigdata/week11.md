# 📘 Random Graphs — Detailed Explanations with Examples

---

## 🔷 CONCEPT 1: Network Data

**Explanation:** Real-world systems can be modeled as networks where entities are nodes and relationships are edges. This abstraction helps us analyze complex systems mathematically.

**Detailed Example: Airline Network**

Consider **Emirates Airlines**:
- **Nodes:** Airports (Dubai DXB, London LHR, New York JFK, Sydney SYD, etc.)
- **Edges:** Direct flight routes

**Hub-and-spoke structure:**

```text
    [DXB] - Hub (Dubai)
   /  |  \
 [LHR][JFK][SYD] - Destinations
  |    |    |
[MAN][LAX][MEL]
```



Emirates uses **1 hub** (Dubai) — almost all flights connect through it. In contrast, **British Airways** uses **2 hubs** (Heathrow and Gatwick), creating a different network topology.

**Analysis insights:**
- Average path length: How many stops for any trip?
- Betweenness centrality: Which airports are most critical?
- Resilience: What happens if DXB closes?

---

## 🔷 CONCEPT 2: Basic Definition of a Graph

**Explanation:** A graph is a mathematical structure with two components: vertices (points) and edges (connections between pairs of points). The formal definition ensures no self-loops and no multiple edges between the same pair.

**Detailed Example: Friendship Network**

**Visual representation:**
```text
Alice ------- Bob
  |             |
  |             |
David ------- Carol
```


This forms a **cycle C₄** (square). Each person is a node; friendship is mutual (undirected edge).

**Formal verification:**
- |V| = 4 ✓
- Each edge is an unordered pair ✓
- No {Alice, Alice} (no self-loops) ✓

---

## 🔷 CONCEPT 3: Vertex Set and Edge Set

**Explanation:** The vertex set is simply all nodes. The edge set contains all connections. We write V(G) and E(G) to emphasize these belong to graph G.

**Detailed Example: Computer Network**

**Router network with 5 nodes:**

**Network topology:**
```text
    R1
   /  \
 R2    R3
  \    / \
   R4 ---- R5
```

   
**Properties:**
- |V| = 5
- |E| = 6
- Is it connected? Yes, path exists between any pair
- Is it a tree? No (has cycles: R3-R4-R5-R3)

---

## 🔷 CONCEPT 4: Bipartite Graph

**Explanation:** A graph is bipartite if we can color all vertices with two colors such that no edge connects same-colored vertices. Equivalently, no odd-length cycles exist.

**Example: Dating App (Users and Profiles)**

**Two sets:**
- V₁ = Users = {U1, U2, U3, U4} (left side)
- V₂ = Profiles = {P1, P2, P3} (right side)

**Edges = "Viewed" relationships:**

```text
    U1 ----> P1
   / |       |
  /  |       |
U2   U3 ----> P2
  \  |     /
   \ |    /
    U4 --> P3
```

    
**Formal edges:** E = {{U1,P1}, {U1,P2}, {U2,P1}, {U3,P2}, {U3,P3}, {U4,P2}, {U4,P3}}

**Bipartite check:** Every edge connects U-* to P-* — no edges within users or within profiles ✓

**Complete bipartite K₂,₂ subset:** {U1,U3} connected to {P1,P2} forms K₂,₂

---

## 🔷 CONCEPT 5: Tree

**Explanation:** A tree is a minimally connected graph — removing any edge disconnects it, and adding any edge creates a cycle. Trees model hierarchical structures.

**Example: File System**

**Graph representation:**
```text
   /home
  /     \
/user1  /user2
 /  \     /  \
docs pics work music
```

**Verify tree properties:**
- n = 7 nodes (1 root, 2 users, 4 subfolders)
- edges = 6 parent-child relationships
- n − 1 = 6 ✓
- Unique path example: /home → /user1 → docs
- No cycles: there is exactly one simple path between any two nodes

---

## 🔷 CONCEPT 6: Complete Graph and Clique

**Explanation:** A complete graph has every possible edge. A clique is a complete subgraph — a tightly-knit community where everyone knows everyone.

**Example: Project Team — Complete Graph K₅**

**5-person team where everyone works directly with everyone:**
```text
  1
   /|\
  / | \
 2--3--4
  \ | /
   \|/
  5
```

    
**All edges:** {1,2}, {1,3}, {1,4}, {1,5}, {2,3}, {2,4}, {2,5}, {3,4}, {3,5}, {4,5}

**Count:** C(5,2) = 10 edges ✓

**Clique in larger graph:** Consider a company of 100 people. The "Executive Committee" {CEO, CFO, CTO, COO} forms a K₄ clique if all four have direct working relationships, even if the whole company graph isn't complete.

---

## 🔷 CONCEPT 7: Graph Isomorphism

**Explanation:** Two graphs are isomorphic if they have identical structure — same connectivity pattern, just with different labels. Finding isomorphism is computationally hard (GI problem).

**Example: Two "Different" Looking Graphs**

**Graph G:**
```text
a - b
|   |
d - c
```

**Graph H:**
```text
1 - 2
|   |
4 - 3
```


**Are they isomorphic?**

Try mapping: φ(a)=1, φ(b)=2, φ(c)=3, φ(d)=4

Check edges:
- {a,b} → {1,2} ✓ exists
- {b,c} → {2,3} ✓ exists  
- {c,d} → {3,4} ✓ exists
- {d,a} → {4,1} ✓ exists

**Both are C₄ (4-cycle)!** Isomorphic ✓

---

## 🔷 CONCEPT 8: Cycles

**Explanation:** A cycle is a closed walk with no repeated vertices (except start=end). Cycles create redundancy in networks — multiple paths between nodes.

**Example: City Road Network — One-Way Ring**

**Cycle C₅ — downtown one-way ring road:**
```text
    A (City Hall)
   /             \
B (Train Station)   E (Airport)
  |               |
  |               |
  C -----------> D (Mall)
  (Residential)
```

      
**Edges (undirected version):** {{A,B}, {B,C}, {C,D}, {D,E}, {E,A}}

**Properties:**
- n = 5 vertices, n = 5 edges
- Connected, each vertex has degree 2
- Diameter = 2 (furthest apart: B and E, via A or C-D)

---

## 🔷 CONCEPT 9: Degree of a Vertex

**Explanation:** Degree counts direct connections. The Handshaking Lemma states that summing all degrees equals twice the edge count (each edge contributes to two vertices' degrees).

**Example: Academic Collaboration Network**

**Co-authorship network:**

```text
   Alice (deg=3) - Bob (deg=2)
    |   \           |
    |    \          |
  Carol --- Dave (deg=5) - Frank (deg=1)
    \      /
     \    /
      Eve (deg=2)
```


  
**Edges:** {Alice,Bob}, {Alice,Carol}, {Alice,Dave}, {Bob,Dave}, {Carol,Dave}, {Carol,Eve}, {Dave,Eve}, {Dave,Frank}

**Degree table:**
| Person | Co-authors | Degree |
|--------|-----------|--------|
| Alice | Bob, Carol, Dave | 3 |
| Bob | Alice, Dave | 2 |
| Carol | Alice, Dave, Eve | 3 |
| Dave | Alice, Bob, Carol, Eve, Frank | **5** |
| Eve | Carol, Dave | 2 |
| Frank | Dave | 1 |

**Verify Handshaking Lemma:**
Σ deg(v) = 3+2+3+5+2+1 = 16 = 2 × 8 edges ✓

---

## 🔷 CONCEPT 10: Adjacency Matrix

**Explanation:** The adjacency matrix encodes all edges in a 0-1 matrix. Entry (i,j) = 1 means vertices i and j are connected. For undirected graphs, A = Aᵀ (symmetric).

**Example: Small Social Network (4 friends)**

**Network:** Edges show who messages whom regularly

```text
[1]--[2]
 | X |
[3]--[4]
```


Edges: {1,2}, {1,3}, {2,3}, {2,4}, {3,4}

**Adjacency matrix A (4×4):**

|   | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| **1** | 0 | 1 | 1 | 0 |
| **2** | 1 | 0 | 1 | 1 |
| **3** | 1 | 1 | 0 | 1 |
| **4** | 0 | 1 | 1 | 0 |

**Properties verified:**
- A = Aᵀ (symmetric) ✓
- Diagonal = 0 (no self-loops) ✓
- Row sums = degrees: deg(1)=2, deg(2)=3, deg(3)=3, deg(4)=2 ✓

---

## 🔷 CONCEPT 11: Random Graph

**Explanation:** Instead of a fixed graph, we consider a probability space of all possible graphs. This allows probabilistic analysis: "What properties does a typical graph have?"

**Example: Random Friendship Formation (5 students)**

**Scenario:** 5 new students. Each pair becomes friends with probability p.

**Sample space:** All 2^(C(5,2)) = 2^10 = 1024 possible friendship graphs

**Three possible outcomes:**

**G₁ (sparse, p=0.1):** Only 2 friendships - disconnected

```text
1 - 2     3 - 4     5
```


**G₂ (moderate, p=0.4):** ~8 friendships — connected

```text
1--2--3
|\ |  |
| \|  |
4--5--(more edges)
```


**G₃ (dense, p=0.8):** ~20 friendships - nearly complete

```text
1 - 2
| X |
3 - 4 - 5
 \___/
```

Here, most pairs are connected, so the graph is close to complete and has many triangles.


---

## 🔷 CONCEPT 12: Erdős–Rényi Model G(n, p)

**Explanation:** The foundational random graph model. n vertices; each of C(n,2) possible edges included independently with probability p.

**Example: G(6, 0.3) — Research Collaborations**

6 researchers, each potential collaboration forms with probability 0.3.

**Possible edges:** C(6,2) = 15

**One realization:** Edges {1,2}, {1,4}, {2,3}, {2,5}, {3,6}, {4,5} appear (6 edges)

**Visual:**
```text
1 -- 2 -- 3
|    \    \
4 ---- 5   6
```


**G(n,M) alternative:** Exactly 4 edges chosen uniformly from 15 possible. Different distribution!

---

## 🔷 CONCEPT 13: Properties of G(n, p)

**Explanation:** Key probabilistic properties: probability of specific graphs, expected edges, adjacency matrix structure.

**Example: G(100, 0.05) — Online Social Network**

n=100 people, p=0.05 chance any two are friends.

**Expected edges:**
E[|E|] = p × C(100,2) = 0.05 × 4950 = **247.5 edges**

**Probability of specific graph with m=250 edges:**
P(G) = (0.05)^250 × (0.95)^4700 — tiny, but graphs near 247 edges dominate.

**Adjacency matrix:** 100×100 symmetric, 4950 independent Bernoulli(0.05) entries above diagonal.

---

## 🔷 CONCEPT 14: Sparse vs Dense Regimes

**Explanation:** The scaling of p with n determines global structure. p = c/n is the critical threshold where a giant component emerges.

**Example: Epidemic Spread Model (n=10,000)**

**Regime 1: c = 0.5 (p = 0.00005)**
- Average degree: 0.5
- **Structure:** Tiny isolated components
- **Epidemic:** Dies out immediately

**Regime 2: c = 2 (p = 0.0002)** — **ABOVE THRESHOLD**
- Average degree: 2
- **Structure:** Giant component with ~75% of nodes!
- **Epidemic:** Spreads widely

**Phase transition at c=1:** At p=1/n, largest component jumps from O(log n) to Θ(n).

---

## 🔷 CONCEPT 15: Connectivity Threshold

**Explanation:** Being connected requires p ≥ (ln n)/n. Isolated vertices are the main obstruction.

**Example: Sensor Network (n=1000 sensors)**

**Critical question:** What p ensures full connectivity?

**Calculation:** ln(1000) ≈ 6.9, so threshold p* ≈ 6.9/1000 = 0.0069

**p = 0.005 (below):** ~6-7 isolated sensors expected → disconnected

**p = 0.01 (above):** ~0.05 expected isolates → essentially 0 → connected!

**Sharp threshold:** Connectivity probability jumps from near 0 to near 1 at p ≈ (ln n)/n.

---

## 🔷 CONCEPT 16: Cliques in G(n, p)

**Explanation:** Cliques represent tightly-knit groups. Expected k-clique count: C(n,k) · p^C(k,2)

**Example: G(200, 0.5) — Brain Region Connectivity**

200 brain regions, edge = functional correlation > threshold.

| Clique size | Expected count | Interpretation |
|-------------|---------------|----------------|
| 4 | ~1,010,000 | Very common |
| 8 | ~2,000 | Moderate |
| 10 | ~0.64 | Rare |
| 15 | Tiny | Extremely rare |

**Maximum clique size:** Concentrated around 2 log₂(n) ≈ 15-16, but actual max is ~9-11 due to precise formula.

---

## 🔷 CONCEPT 17: Diameter and Distances

**Explanation:** Diameter measures worst-case communication efficiency. Random graphs have remarkably small diameters.

**Example: G(1000, 0.01) — Academic Citation Network**

p = 0.01 > (1+ε)ln(n)/n ≈ 0.007, so diameter is **2 or 3**.

**Why diameter ≈ 2?**

For any two vertices u, v:
- P(no direct edge) = 0.99
- P(no common neighbor) ≈ (0.995)^998 ≈ 0.006

P(distance > 2) ≈ 0.99 × 0.006 ≈ very small!

**Result:** Any two researchers connect in ≤ 3 citation hops with high probability.

---

## 🔷 CONCEPT 18: Triangles in G(n, p)

**Explanation:** E[T] = C(n,3) · p³. Random graphs have fewer triangles than real social networks (no transitivity).

**Example: G(50, 0.2) — Startup Team Interactions**

50 employees, edge = "had meeting together."

**Expected triangles:** E[T] = C(50,3) × 0.008 = 19,600 × 0.008 = **156.8**

**Actual observation:** 340 triangles found!

**Comparison:** 340 vs 157 — **2.17× more than random!**

This excess indicates natural team clustering around projects.

---

## 🔷 CONCEPT 19: Bernoulli View of Edges

**Explanation:** G(n,p) is completely described by C(n,2) independent Bernoulli(p) variables.

**Example: G(4, 0.5) — Complete Analysis**

**6 independent Bernoulli(0.5) variables:**

X12, X13, X14, X23, X24, X34 where Xij = 1 if edge (i,j) is present.


**Sample outcome:** (1, 0, 1, 1, 0, 1) → edges {1,2}, {1,4}, {2,3}, {3,4}

**Probability:** (0.5)^6 = 1/64

**When p=0.5:** All 2^6 = 64 graphs are equally likely!

---

## 🔷 CONCEPT 20: Degree Distribution

**Explanation:** Degrees are Binomial(n-1, p). For p=c/n, converges to Poisson(c).

**Example: G(1000, 0.003) — Sparse Network**

p = 3/1000 = c/n with c=3.

**Poisson(3) approximation:**

| Degree k | P(deg = k) |
|----------|-----------|
| 0 | 0.050 |
| 1 | 0.149 |
| 2 | 0.224 |
| 3 | 0.224 |
| 4 | 0.168 |

**Real networks differ:** Twitter degrees are power-law, not Poisson.

---

## 🔷 CONCEPT 21: Maximum Likelihood Estimation

**Explanation:** Given observed network with m edges, p̂_MLE = m / C(n,2) = observed edge density.

**Example 1: Protein Network**

n=500 proteins, m=1250 interactions.

p̂ = 1250 / C(500,2) = 1250 / 124750 ≈ **0.01 (1%)**

**Example 2: Multiple Networks**

Three tissue networks (all n=4):
- Liver: K₄ (6 edges)
- Brain: K₁,₃ (3 edges)  
- Muscle: P₄ (3 edges)

**Likelihood:** L(p) = p^6 · p³(1-p)³ · p³(1-p)³ = p^12 (1-p)^6

**MLE:** p̂ = 12 / (12+6) = **12/18 = 2/3 ≈ 0.667**

---

## 🔷 CONCEPT 22: Markov's Inequality

**Explanation:** For non-negative X: P(X ≥ k) ≤ E[X]/k

**Example: Server Load**

X = job completion time, E[X] = 10 minutes.

**Bound:** P(X > 30) ≤ 10/30 = **33.3%**

P(X > 60) ≤ 16.7%, P(X > 120) ≤ 8.3%

**Network application:** P(edges > 50000 in G(1000,0.1)) ≤ 49995/50000 ≈ 90% (weak — use Chernoff for tighter bounds).

---

## 🔷 CONCEPT 23: Chebyshev's Inequality

**Explanation:** P(|X−µ| ≥ ε) ≤ σ²/ε²

**Example: Manufacturing Quality**

Part diameter: µ = 10mm, σ = 0.5mm.

**Bound:** P(|X−10| ≥ 2) ≤ 0.25/4 = **6.25%**

Compare to normal: actual P ≈ 0.003% — Chebyshev is conservative but assumption-free.

---

## 🔷 CONCEPT 24: Indicator Function

**Explanation:** ₁ₐ(x) = 1 if x ∈ A, else 0. Converts counting to summation.

**Example: Election Polling**

Iᵢ = 1 if voter i supports Candidate A.

**Total support:** S = Σ Iᵢ, E[S] = Σ E[Iᵢ] = n × p

**Network application:** Δᵢⱼₖ = 1{triangle on i,j,k}, T = Σ Δᵢⱼₖ, E[T] = C(n,3)p³

---

## 🔷 CONCEPT 25: Weak Law of Large Numbers

**Explanation:** Sample averages converge to expectations: X̄ₙ →ᵖ µ

**Example: Monte Carlo π Estimation**

Xᵢ = 1 if random point in [0,1]² falls in quarter-circle.

E[Xᵢ] = π/4 ≈ 0.785

**WLLN:** (points in circle)/n →ᵖ π/4

| n | Typical estimate |
|---|---------------|
| 100 | 0.76–0.81 |
| 10,000 | 0.782–0.788 |
| 1,000,000 | 0.784–0.786 |

---

## 🔷 CONCEPT 26: WLLN for Random Graphs (Triangle Count)

**Explanation:** Triangle count concentrates: P(|Δ/E[Δ] − 1| > ε) → 0

**Detailed Example: G(50, 0.2)**

**Step 1 — Setup:**
- n = 50, p = 0.2
- C(50,3) = 19,600 triples
- E[Δ] = 19,600 × 0.008 = **156.8**

**Step 2 — Variance:**

*Individual variances:* 19,600 × (0.008 − 0.000064) ≈ 155.55

*Covariances (pairs sharing 1 edge):*
- C(50,2) × C(48,2) = 1,381,800 pairs
- Each: Cov = p⁵ − p⁶ = 0.00032 − 0.000064 = 0.000256
- Total: 1,381,800 × 0.000256 ≈ **353.74**

*Total variance:* Var(Δ) ≈ 155.55 + 353.74 = **509.3**

**Step 3 — Chebyshev application:**

P(|Δ/E[Δ] − 1| > 0.3) ≤ Var(Δ)/(0.3² × E[Δ]²) = 509.3/(0.09 × 24579) ≈ 0.23

For large n: ratio → 0, giving strong concentration. Δ/E[Δ] →ᵖ 1 ✓

---

## 📌 Master Summary Table

| Concept | Key Formula/Fact |
|---------|-----------------|
| Graph | G = (V, E) |
| Complete Graph Kₙ | \|E\| = C(n,2) = n(n−1)/2 |
| Tree | n vertices, n−1 edges, no cycles |
| Bipartite | V = V₁ ∪ V₂, edges only cross partitions |
| Random Graph | Probability distribution over graphs |
| G(n,p) — Expected edges | E[\|E\|] = p·C(n,2) |
| Degree distribution | Binomial(n−1, p) → Poisson(c) when p=c/n |
| Connectivity threshold | p = (ln n)/n |
| Giant component threshold | p = 1/n (c=1) |
| Expected triangles | C(n,3)·p³ |
| Expected k-cliques | C(n,k)·p^C(k,2) |
| Diameter (dense, p constant) | ≈ 2 with high probability |
| MLE of p | p̂ = 2m/n(n−1) = observed edge density |
| Markov's Inequality | P(X≥k) ≤ E[X]/k |
| Chebyshev's Inequality | P(\|X−µ\|≥ε) ≤ σ²/ε² |
| WLLN | X̄ₙ →ᵖ µ as n→∞ |
| LLN for triangles | Δ/E[Δ] →ᵖ 1 as n→∞ |