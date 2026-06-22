# Soft Computing — Unit 2: Fuzzy Sets, Fuzzy Logic & Fuzzy Systems

> **Syllabus:** Classical sets and fuzzy sets, fuzzy relations, operations & properties, membership functions, fuzzification methods, λ-cuts & defuzzification, classical & fuzzy logic, approximate reasoning, fuzzy implication, fuzzy rule based systems (linguistic hedges, aggregation, Mamdani & Sugeno FIS), applications (home appliances, controllers, medical diagnosis, weather forecasting).

---

## Table of Contents

1. [Classical Sets — Operations & Properties](#1-classical-sets--operations--properties)
2. [Fuzzy Sets — Operations & Properties](#2-fuzzy-sets--operations--properties)
3. [Fuzzy Relations — Cardinality, Operations & Properties](#3-fuzzy-relations)
4. [Membership Functions & Fuzzification Methods](#4-membership-functions--fuzzification-methods)
5. [Fuzzy → Crisp Conversion (λ-Cuts & Defuzzification)](#5-fuzzy--crisp-conversion)
6. [Classical vs Fuzzy Logic](#6-classical-vs-fuzzy-logic)
7. [Approximate Reasoning & Fuzzy Implication](#7-approximate-reasoning--fuzzy-implication)
8. [Fuzzy Rule-Based Systems & Inference (Mamdani / Sugeno)](#8-fuzzy-rule-based-systems--inference)
9. [Applications of Fuzzy Logic](#9-applications-of-fuzzy-logic)
10. [Quick Revision Cheat-Sheet](#10-quick-revision-cheat-sheet)

---

# 1. Classical Sets — Operations & Properties

## 📘 1.1 Definition

A **classical (crisp) set** $A$ over a universe of discourse $X$ is a collection where every $x \in X$ either *fully belongs* or *does not belong*:

$$
\chi_A(x) = \begin{cases} 1 & x \in A \\ 0 & x \notin A \end{cases}
$$

$\chi_A$ is called the **characteristic function**.

### Representation
- **Roster form:** $A = \{1, 2, 3, 5, 7\}$
- **Set-builder:** $A = \{x \in \mathbb{N} : x \le 7,\; x\text{ is prime or }1\}$
- **Characteristic vector:** for $X=\{1,2,\dots,8\}$, $\chi_A = (1,1,1,0,1,0,1,0)$

---

## 🧮 1.2 Operations on Classical Sets

Let $A, B \subseteq X$.

| Operation | Definition | Characteristic Function |
|---|---|---|
| **Union** | $A \cup B = \{x : x \in A \text{ or } x \in B\}$ | $\chi_{A\cup B}(x) = \max(\chi_A,\chi_B)$ |
| **Intersection** | $A \cap B = \{x : x \in A \text{ and } x \in B\}$ | $\chi_{A\cap B}(x) = \min(\chi_A,\chi_B)$ |
| **Complement** | $\bar A = \{x \in X : x \notin A\}$ | $\chi_{\bar A}(x) = 1 - \chi_A(x)$ |
| **Difference** | $A - B = A \cap \bar B$ | $\chi_{A-B}(x) = \chi_A \cdot (1 - \chi_B)$ |
| **Sym. difference** | $A \triangle B = (A-B)\cup(B-A)$ | XOR |
| **Cartesian product** | $A \times B = \{(a,b) : a\in A, b\in B\}$ | — |

---

## 📐 1.3 Properties of Classical Sets

| Law | Statement |
|---|---|
| **Commutative** | $A\cup B = B\cup A,\; A\cap B = B\cap A$ |
| **Associative** | $(A\cup B)\cup C = A\cup(B\cup C)$ |
| **Distributive** | $A\cap(B\cup C)=(A\cap B)\cup(A\cap C)$ |
| **Idempotent** | $A\cup A = A,\; A\cap A = A$ |
| **Identity** | $A\cup\emptyset = A,\; A\cap X = A$ |
| **Domination** | $A\cup X = X,\; A\cap\emptyset = \emptyset$ |
| **Involution** | $\bar{\bar A} = A$ |
| **De Morgan's** | $\overline{A\cup B}=\bar A\cap \bar B$ |
| **Absorption** | $A\cup(A\cap B)=A,\; A\cap(A\cup B)=A$ |
| **Law of Excluded Middle** | $A\cup\bar A = X$ ✅ holds |
| **Law of Contradiction** | $A\cap\bar A = \emptyset$ ✅ holds |

> ⚠️ The last two laws hold for crisp sets but **fail** for fuzzy sets — this is *the* defining difference.

### Cardinality (crisp)

$$|A| = \sum_{x \in X} \chi_A(x)$$

For a power set: $|2^X| = 2^{|X|}$.

---

# 2. Fuzzy Sets — Operations & Properties

## 📘 2.1 Definition (Recap)

A **fuzzy set** $\tilde A$ over $X$ is defined by a membership function $\mu_{\tilde A} : X \to [0,1]$.

$$
\tilde A = \{(x, \mu_{\tilde A}(x)) : x \in X\}
$$

**Zadeh's notation:**

$$
\tilde A \;=\; \sum_{x_i \in X}\frac{\mu_{\tilde A}(x_i)}{x_i} \quad\text{(discrete)} \qquad \tilde A \;=\; \int_X \frac{\mu_{\tilde A}(x)}{x} \quad\text{(continuous)}
$$

> The "+" and "/" are **symbolic**, *not* arithmetic.

---

## 🧮 2.2 Operations on Fuzzy Sets (Zadeh's Standard)

Let $\tilde A, \tilde B$ be fuzzy sets on $X$.

| Operation | Membership Function |
|---|---|
| **Union** | $\mu_{\tilde A\cup\tilde B}(x)=\max(\mu_{\tilde A}(x),\mu_{\tilde B}(x))$ |
| **Intersection** | $\mu_{\tilde A\cap\tilde B}(x)=\min(\mu_{\tilde A}(x),\mu_{\tilde B}(x))$ |
| **Complement** | $\mu_{\bar{\tilde A}}(x)=1-\mu_{\tilde A}(x)$ |
| **Equality** | $\tilde A=\tilde B \iff \mu_{\tilde A}(x)=\mu_{\tilde B}(x)\;\forall x$ |
| **Containment** | $\tilde A\subseteq\tilde B \iff \mu_{\tilde A}(x)\le\mu_{\tilde B}(x)\;\forall x$ |
| **Algebraic product** | $\mu_{\tilde A\cdot\tilde B}(x)=\mu_{\tilde A}(x)\cdot\mu_{\tilde B}(x)$ |
| **Algebraic sum** | $\mu_{\tilde A+\tilde B}(x)=\mu_{\tilde A}(x)+\mu_{\tilde B}(x)-\mu_{\tilde A}(x)\mu_{\tilde B}(x)$ |
| **Bounded sum** | $\mu(x)=\min(1,\,\mu_{\tilde A}(x)+\mu_{\tilde B}(x))$ |
| **Bounded difference** | $\mu(x)=\max(0,\,\mu_{\tilde A}(x)-\mu_{\tilde B}(x))$ |
| **Power** | $\tilde A^p$ has $\mu(x)=[\mu_{\tilde A}(x)]^p$ |

### Generalized — *t*-norms & *s*-norms (*t*-conorms)

A **t-norm** $T:[0,1]^2\to[0,1]$ generalizes intersection; an **s-norm** $S$ generalizes union.

| Family | t-norm $T(a,b)$ | s-norm $S(a,b)$ |
|---|---|---|
| **Standard (Zadeh)** | $\min(a,b)$ | $\max(a,b)$ |
| **Algebraic** | $a\cdot b$ | $a+b-ab$ |
| **Łukasiewicz** | $\max(0, a+b-1)$ | $\min(1, a+b)$ |
| **Drastic** | $a$ if $b=1$, $b$ if $a=1$, else $0$ | dual |

Axioms (t-norm): commutativity, associativity, monotonicity, boundary $T(a,1)=a$.

---

## 📐 2.3 Properties of Fuzzy Sets

| Property | Status |
|---|---|
| Commutativity | ✅ |
| Associativity | ✅ |
| Distributivity | ✅ |
| Idempotency | ✅ ($\max,\min$ semantics) |
| Identity & Domination | ✅ |
| De Morgan's laws | ✅ |
| Involution | ✅ |
| **Law of Excluded Middle** $\tilde A \cup \bar{\tilde A}=X$ | ❌ FAILS |
| **Law of Contradiction** $\tilde A \cap \bar{\tilde A}=\emptyset$ | ❌ FAILS |

### 📐 Why excluded middle fails — example

If $\mu_{\tilde A}(x) = 0.4$ then $\mu_{\bar{\tilde A}}(x) = 0.6$, so
$\mu_{\tilde A \cup \bar{\tilde A}}(x) = \max(0.4,0.6) = 0.6 \ne 1$ and
$\mu_{\tilde A \cap \bar{\tilde A}}(x) = \min(0.4,0.6) = 0.4 \ne 0$.

---

## 🧮 2.4 Cardinality of a Fuzzy Set

### Scalar (sigma) cardinality
$$
|\tilde A| \;=\; \sum_{x \in X} \mu_{\tilde A}(x) \qquad\text{(discrete)}\qquad |\tilde A| \;=\; \int_X \mu_{\tilde A}(x)\,dx \qquad\text{(continuous)}
$$

### Relative cardinality
$$
\|\tilde A\| \;=\; \frac{|\tilde A|}{|X|}
$$

### Fuzzy cardinality
$|\tilde A|_f$ is itself a fuzzy set whose elements are $\alpha$-cut cardinalities at degree $\alpha$.

---

## ✏️ 2.5 Solved Problems

### ✏️ Problem 1 — Operations & Cardinality

$X=\{a,b,c,d,e\}$,
$\tilde A=\tfrac{0.1}{a}+\tfrac{0.4}{b}+\tfrac{0.7}{c}+\tfrac{1.0}{d}+\tfrac{0.3}{e}$,
$\tilde B=\tfrac{0.5}{a}+\tfrac{0.6}{b}+\tfrac{0.2}{c}+\tfrac{0.8}{d}+\tfrac{0.4}{e}$.

Find $\tilde A\cup\tilde B,\;\tilde A\cap\tilde B,\;\bar{\tilde A},\;|\tilde A|,\;\|\tilde A\|$, algebraic product and bounded sum.

| $x$ | $\mu_A$ | $\mu_B$ | $\cup$ | $\cap$ | $1-\mu_A$ | $\mu_A\mu_B$ | $\min(1,\mu_A+\mu_B)$ |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| a | 0.1 | 0.5 | 0.5 | 0.1 | 0.9 | 0.05 | 0.6 |
| b | 0.4 | 0.6 | 0.6 | 0.4 | 0.6 | 0.24 | 1.0 |
| c | 0.7 | 0.2 | 0.7 | 0.2 | 0.3 | 0.14 | 0.9 |
| d | 1.0 | 0.8 | 1.0 | 0.8 | 0.0 | 0.80 | 1.0 |
| e | 0.3 | 0.4 | 0.4 | 0.3 | 0.7 | 0.12 | 0.7 |

$|\tilde A| = 0.1+0.4+0.7+1.0+0.3 = \mathbf{2.5}$
$\|\tilde A\| = 2.5/5 = \mathbf{0.5}$

---

### ✏️ Problem 2 — Verify Excluded-Middle Failure

For $\mu_{\tilde A}(x) = 0.3$ on a singleton universe, show $\tilde A \cup \bar{\tilde A} \ne X$.

$\mu_{\tilde A \cup \bar{\tilde A}} = \max(0.3, 0.7) = 0.7 \ne 1$. ✅ Demonstrated.

---

# 3. Fuzzy Relations

## 📘 3.1 Crisp Relation Recap

A crisp relation $R$ from $X$ to $Y$ is a subset of $X\times Y$:
$$
\chi_R(x,y) = \begin{cases} 1 & (x,y)\in R\\ 0 & \text{else}\end{cases}
$$

A **fuzzy relation** $\tilde R$ generalizes this with $\mu_{\tilde R}:X\times Y \to [0,1]$.

$$
\tilde R = \{((x,y),\mu_{\tilde R}(x,y)) : x\in X, y\in Y\}
$$

Represented as a **fuzzy relation matrix** $M_{\tilde R}=[\mu_{\tilde R}(x_i,y_j)]$.

---

## 🧮 3.2 Operations on Fuzzy Relations

Let $\tilde R, \tilde S$ be fuzzy relations on $X\times Y$.

| Operation | Definition |
|---|---|
| **Union** | $\mu_{\tilde R\cup\tilde S}(x,y)=\max(\mu_{\tilde R},\mu_{\tilde S})$ |
| **Intersection** | $\mu_{\tilde R\cap\tilde S}(x,y)=\min(\mu_{\tilde R},\mu_{\tilde S})$ |
| **Complement** | $\mu_{\bar{\tilde R}}(x,y)=1-\mu_{\tilde R}(x,y)$ |
| **Containment** | $\tilde R\subseteq\tilde S \iff \mu_{\tilde R}\le\mu_{\tilde S}$ |
| **Inverse / Transpose** | $\mu_{\tilde R^{-1}}(y,x)=\mu_{\tilde R}(x,y)$ |
| **Projection on $X$** | $\mu_{\mathrm{proj}_X\tilde R}(x)=\max_y \mu_{\tilde R}(x,y)$ |
| **Cylindric extension** | from $X$ → $X\times Y$ by repeating $\mu$ over $Y$ |

---

## 🧮 3.3 Composition of Fuzzy Relations

Given $\tilde R$ on $X\times Y$ and $\tilde S$ on $Y\times Z$, the composition $\tilde R \circ \tilde S$ on $X \times Z$:

### Max–Min Composition
$$
\mu_{\tilde R \circ \tilde S}(x,z) \;=\; \max_{y \in Y}\,\min\!\bigl(\mu_{\tilde R}(x,y),\,\mu_{\tilde S}(y,z)\bigr)
$$

### Max–Product Composition
$$
\mu_{\tilde R \circ \tilde S}(x,z) \;=\; \max_{y \in Y}\,\bigl(\mu_{\tilde R}(x,y)\cdot\mu_{\tilde S}(y,z)\bigr)
$$

> Composition is analogous to matrix multiplication where $(+,\times)$ → $(\max,\min)$ or $(\max,\cdot)$.

---

## 📐 3.4 Properties of Fuzzy Relations on $X\times X$

A fuzzy relation $\tilde R$ on $X\times X$ may have:

| Property | Definition |
|---|---|
| **Reflexive** | $\mu_{\tilde R}(x,x)=1 \;\forall x$ |
| **Symmetric** | $\mu_{\tilde R}(x,y)=\mu_{\tilde R}(y,x)$ |
| **Anti-symmetric** | If $\mu_{\tilde R}(x,y)>0$ and $\mu_{\tilde R}(y,x)>0$ then $x=y$ |
| **Transitive** (max-min) | $\mu_{\tilde R}(x,z)\ge\max_y\min(\mu_{\tilde R}(x,y),\mu_{\tilde R}(y,z))$ |
| **Fuzzy equivalence** | Reflexive + Symmetric + Transitive |
| **Fuzzy tolerance** | Reflexive + Symmetric |

### Cardinality of a Fuzzy Relation

$$
|\tilde R| \;=\; \sum_{x,y} \mu_{\tilde R}(x,y)
$$

---

## ✏️ 3.5 Solved Problem — Max-Min Composition

$X=\{x_1,x_2\},\,Y=\{y_1,y_2,y_3\},\,Z=\{z_1,z_2\}$.

$$
\tilde R = \begin{bmatrix} 0.3 & 0.8 & 0.5 \\ 0.7 & 0.2 & 0.9 \end{bmatrix} \qquad
\tilde S = \begin{bmatrix} 0.6 & 0.4 \\ 0.3 & 0.7 \\ 0.5 & 0.8 \end{bmatrix}
$$

Compute $\tilde T = \tilde R \circ \tilde S$ via max-min.

**Compute** $\mu_{\tilde T}(x_1, z_1)$:
$$\max\{\min(0.3,0.6),\,\min(0.8,0.3),\,\min(0.5,0.5)\} = \max\{0.3,\,0.3,\,0.5\} = 0.5$$

**$\mu_{\tilde T}(x_1, z_2)$:** $\max\{\min(0.3,0.4),\min(0.8,0.7),\min(0.5,0.8)\}=\max\{0.3,0.7,0.5\}=0.7$

**$\mu_{\tilde T}(x_2, z_1)$:** $\max\{\min(0.7,0.6),\min(0.2,0.3),\min(0.9,0.5)\}=\max\{0.6,0.2,0.5\}=0.6$

**$\mu_{\tilde T}(x_2, z_2)$:** $\max\{\min(0.7,0.4),\min(0.2,0.7),\min(0.9,0.8)\}=\max\{0.4,0.2,0.8\}=0.8$

$$\tilde T = \begin{bmatrix} 0.5 & 0.7 \\ 0.6 & 0.8 \end{bmatrix}$$

---

# 4. Membership Functions & Fuzzification Methods

## 📘 4.1 Features of an MF

A membership function $\mu_{\tilde A}(x)$ is characterized by:

| Feature | Meaning |
|---|---|
| **Core** | $\{x : \mu_{\tilde A}(x)=1\}$ — full membership |
| **Support** | $\{x : \mu_{\tilde A}(x)>0\}$ — non-zero region |
| **Boundary** | $\{x : 0<\mu_{\tilde A}(x)<1\}$ — partial membership |
| **Height** | $\sup_x \mu_{\tilde A}(x)$ |
| **Normal** | Height = 1 |
| **Sub-normal** | Height < 1 |
| **Crossover point** | $\mu(x)=0.5$ |
| **Symmetry** | $\mu(c+t)=\mu(c-t)$ around center $c$ |
| **Convex** | $\mu(\lambda x_1+(1-\lambda)x_2)\ge \min(\mu(x_1),\mu(x_2))$ |

### 📐 Convexity Theorem
A fuzzy set $\tilde A$ is convex **iff** every α-cut $A_\alpha$ is a convex (interval) crisp set.

```
   1 ┤        ┌──────┐                    ← Core (μ=1)
     │       /│      │\                 
   μ │      / │      │ \                 
     │     /  │      │  \    Boundary    
   0 ┤────/───┴──────┴───\─────                 
            └─── Support ───┘             
                Symmetric, Normal, Convex MF
```

---

## 🧮 4.2 Standard MF Forms

### Triangular
$$
\mu(x;\,a,b,c) = \max\!\left(\min\!\left(\frac{x-a}{b-a},\,\frac{c-x}{c-b}\right),\,0\right)
$$

### Trapezoidal
$$
\mu(x;\,a,b,c,d) = \max\!\left(\min\!\left(\frac{x-a}{b-a},\,1,\,\frac{d-x}{d-c}\right),\,0\right)
$$

### Gaussian
$$
\mu(x;\,c,\sigma) = \exp\!\left(-\frac{(x-c)^2}{2\sigma^2}\right)
$$

### Generalized Bell
$$
\mu(x;\,a,b,c) = \frac{1}{1+\left|\dfrac{x-c}{a}\right|^{2b}}
$$

### Sigmoidal (S-shaped / Z-shaped pair)
$$
S(x;\,a,c) = \frac{1}{1+e^{-a(x-c)}},\qquad Z(x;\,a,c)=1-S(x;a,c)
$$

### Π (Pi) MF
Bell-like — combination of S and Z.

---

## 📘 4.3 Fuzzification Methods

**Fuzzification** = converting a crisp value $x_0$ (or measurement) into a fuzzy set / membership grade.

### A. Singleton fuzzification
$$
\mu_{\tilde A}(x) = \begin{cases} 1 & x=x_0\\ 0 & \text{else}\end{cases}
$$
Most common in real-time controllers — cheap, exact.

### B. Gaussian fuzzification
$$
\mu_{\tilde A}(x) = \exp\!\left(-\frac{(x-x_0)^2}{2\sigma^2}\right)
$$
Smooth; accounts for measurement noise of std-dev $\sigma$.

### C. Triangular fuzzification
Spread the crisp value as a narrow triangle around $x_0$.

### D. Intuition / Expert assignment
Domain experts directly draw the MF shape (Saaty's pairwise comparison, Delphi method).

### E. Rank ordering / Frequency-based
Use empirical histograms or rank tables to derive $\mu$.

### F. Neural Network–based
Train a NN to learn the MF parameters from data (ANFIS uses this).

### G. Genetic Algorithm tuning
Parameters of the MF are encoded as chromosomes and evolved.

### H. Inductive reasoning / Inference-based
Use entropy minimization (Klir-Yuan) to partition the universe.

---

## ✏️ 4.4 Solved Problem — Evaluate an MF

Triangular MF "**young**" $(15, 25, 35)$. Find $\mu(20)$ and $\mu(32)$.

- $\mu(20) = (20-15)/(25-15) = 5/10 = \mathbf{0.5}$
- $\mu(32) = (35-32)/(35-25) = 3/10 = \mathbf{0.3}$

Gaussian MF with $c=25, \sigma=5$: $\mu(20)=e^{-(5)^2/(2\cdot25)}=e^{-0.5}\approx 0.607$.

---

# 5. Fuzzy → Crisp Conversion

## 📘 5.1 λ-Cuts (Alpha-Cuts) for Fuzzy Sets

The **λ-cut** (also α-cut) of $\tilde A$ at level $\lambda \in [0,1]$:

$$
A_\lambda = \{x \in X : \mu_{\tilde A}(x) \ge \lambda\}
$$

**Strong λ-cut:** $A_\lambda^+ = \{x : \mu_{\tilde A}(x) > \lambda\}$.

### 📐 Key Properties of λ-Cuts
1. **Nested:** $\lambda_1 < \lambda_2 \Rightarrow A_{\lambda_2} \subseteq A_{\lambda_1}$.
2. **Union:** $(\tilde A \cup \tilde B)_\lambda = A_\lambda \cup B_\lambda$.
3. **Intersection:** $(\tilde A \cap \tilde B)_\lambda = A_\lambda \cap B_\lambda$.
4. **Complement (general):** $(\bar{\tilde A})_\lambda \ne \overline{A_\lambda}$ (warning!).
5. **Decomposition (Representation) Theorem:**
$$
\tilde A \;=\; \bigcup_{\lambda \in (0,1]} \lambda \cdot A_\lambda
$$
where $\lambda \cdot A_\lambda$ has MF equal to $\lambda$ on $A_\lambda$ and 0 elsewhere.

### ✏️ Example
$\tilde A = \tfrac{0.2}{a}+\tfrac{0.5}{b}+\tfrac{0.8}{c}+\tfrac{1.0}{d}+\tfrac{0.3}{e}$.

| λ | $A_\lambda$ |
|:-:|:--|
| 0.2 | $\{a,b,c,d,e\}$ |
| 0.3 | $\{b,c,d,e\}$ |
| 0.5 | $\{b,c,d\}$ |
| 0.8 | $\{c,d\}$ |
| 1.0 | $\{d\}$ |

---

## 📘 5.2 λ-Cuts for Fuzzy Relations

If $\tilde R$ is a fuzzy relation on $X\times Y$:
$$
R_\lambda = \{(x,y) : \mu_{\tilde R}(x,y) \ge \lambda\}
$$

Yields a crisp relation matrix with entries in $\{0,1\}$.

### ✏️ Example
$$
M_{\tilde R} = \begin{bmatrix} 0.2 & 0.7 \\ 0.9 & 0.4 \end{bmatrix}
\xrightarrow{\lambda=0.5}
M_{R_{0.5}} = \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}
$$

---

## 📘 5.3 Defuzzification Methods

**Goal:** Convert output fuzzy set $\tilde C$ to a crisp value $z^*$.

### A. Centroid / Center of Gravity (COG / COA)
$$
z^* \;=\; \frac{\displaystyle\int z\,\mu_{\tilde C}(z)\,dz}{\displaystyle\int \mu_{\tilde C}(z)\,dz}
\qquad\text{discrete: }\;
z^* = \frac{\sum_i z_i\,\mu_{\tilde C}(z_i)}{\sum_i \mu_{\tilde C}(z_i)}
$$
*Most popular*; balanced.

### B. Bisector (BOA)
$z^*$ such that the area is split equally:
$$
\int_{z_{\min}}^{z^*}\mu_{\tilde C}(z)\,dz \;=\; \int_{z^*}^{z_{\max}}\mu_{\tilde C}(z)\,dz
$$

### C. Mean of Maxima (MOM)
$$
z^* \;=\; \frac{\sum_{z\in G} z}{|G|},\qquad G=\{z : \mu_{\tilde C}(z)=\text{height}(\tilde C)\}
$$

### D. Smallest / Largest of Maxima (SOM / LOM)
$z^*=\min G$ or $\max G$ respectively.

### E. Weighted Average (used in Sugeno)
$$
z^* \;=\; \frac{\sum_i w_i\,\bar z_i}{\sum_i w_i}
$$
where $\bar z_i$ is the peak of the $i$-th output MF and $w_i$ its firing strength.

### F. Center of Sums (COS)
Faster than centroid; sums areas without union:
$$
z^* \;=\; \frac{\sum_z z\,\sum_i \mu_{\tilde C_i}(z)}{\sum_z \sum_i \mu_{\tilde C_i}(z)}
$$

### Comparison

| Method | Pros | Cons |
|---|---|---|
| **Centroid** | Smooth, intuitive | Computationally heavy |
| **Bisector** | Balances area | Same as centroid for symmetric |
| **MOM** | Simple, fast | Ignores shape |
| **SOM/LOM** | Conservative / aggressive choice | Discontinuous |
| **Weighted Avg** | Very fast | Only for Sugeno-style outputs |

---

## ✏️ 5.4 Solved Problem — Defuzzification

Output fuzzy set $\tilde C$ on $Z=\{0,1,2,3,4,5,6\}$ with MF $\mu = (0,\,0.3,\,0.6,\,1.0,\,1.0,\,0.5,\,0.2)$.

### (a) Centroid
$$
z^* = \frac{0(0)+1(0.3)+2(0.6)+3(1)+4(1)+5(0.5)+6(0.2)}{0+0.3+0.6+1+1+0.5+0.2}
= \frac{0+0.3+1.2+3+4+2.5+1.2}{3.6} = \frac{12.2}{3.6} \approx \mathbf{3.39}
$$

### (b) MOM
Maxima occur at $z=3,4$: $z^* = (3+4)/2 = \mathbf{3.5}$.

### (c) SOM / LOM
SOM = 3, LOM = 4.

### (d) Bisector
Total area = 3.6. Half = 1.8. Cumulative:
$0, 0.3, 0.9, 1.9, 2.9, 3.4, 3.6$ → crosses 1.8 between $z=2$ ($0.9$) and $z=3$ ($1.9$). Linearly: $z^* \approx 2 + (1.8-0.9)/(1.9-0.9) \approx 2.9$.

---

# 6. Classical vs Fuzzy Logic

## 📘 6.1 Classical Predicate Logic

**Propositions** are binary — *true* (1) or *false* (0).

| Connective | Symbol | Definition |
|---|---|---|
| Negation | $\neg p$ | $1-p$ |
| Conjunction | $p\land q$ | $\min$ / AND |
| Disjunction | $p\lor q$ | $\max$ / OR |
| Implication | $p\to q$ | $\neg p \lor q$ |
| Bi-conditional | $p\leftrightarrow q$ | $(p\to q)\land(q\to p)$ |

### Predicate logic adds **quantifiers** $\forall$ (universal) and $\exists$ (existential).

### Classical Inference Rules

1. **Modus Ponens (MP):** $\dfrac{p,\;p\to q}{q}$
2. **Modus Tollens (MT):** $\dfrac{\neg q,\;p\to q}{\neg p}$
3. **Hypothetical syllogism:** $\dfrac{p\to q,\;q\to r}{p\to r}$

---

## 📘 6.2 Fuzzy Logic

**Fuzzy logic** generalizes Boolean logic to truth values in $[0,1]$. Connectives are realized via t-norms (AND), s-norms (OR), and negation operators.

| Operator | Standard form | Probabilistic | Łukasiewicz |
|---|---|---|---|
| NOT $p$ | $1-p$ | $1-p$ | $1-p$ |
| $p\land q$ | $\min$ | $p\cdot q$ | $\max(0,p+q-1)$ |
| $p\lor q$ | $\max$ | $p+q-pq$ | $\min(1,p+q)$ |

**Linguistic variables** (e.g., "temperature") take **linguistic values** ("low", "medium", "high"), each represented by a fuzzy set.

---

# 7. Approximate Reasoning & Fuzzy Implication

## 📘 7.1 Approximate Reasoning

Reasoning where premises, rules, and conclusions involve fuzzy concepts.

**Generalized Modus Ponens (GMP):**
- **Premise 1 (rule):** IF $x$ is $\tilde A$ THEN $y$ is $\tilde B$
- **Premise 2 (fact):** $x$ is $\tilde A'$
- **Conclusion:** $y$ is $\tilde B'$

Computed via the **compositional rule of inference (CRI)** by Zadeh:

$$
\tilde B' \;=\; \tilde A' \circ \tilde R(\tilde A,\tilde B)
$$

where $\tilde R$ is the fuzzy implication relation.

---

## 🧮 7.2 Fuzzy Implication Operators

Different definitions for $\mu_{\tilde R}(x,y) = \mathrm{Imp}(\mu_{\tilde A}(x),\mu_{\tilde B}(y))$:

| Name | Formula |
|---|---|
| **Mamdani (Minimum)** | $\min(\mu_{\tilde A}(x),\,\mu_{\tilde B}(y))$ |
| **Larsen (Product)** | $\mu_{\tilde A}(x)\cdot\mu_{\tilde B}(y)$ |
| **Zadeh** | $\max(\min(\mu_{\tilde A},\mu_{\tilde B}),\,1-\mu_{\tilde A})$ |
| **Łukasiewicz** | $\min(1,\,1-\mu_{\tilde A}+\mu_{\tilde B})$ |
| **Gödel** | $1$ if $\mu_{\tilde A}\le\mu_{\tilde B}$ else $\mu_{\tilde B}$ |
| **Kleene-Dienes** | $\max(1-\mu_{\tilde A},\,\mu_{\tilde B})$ |
| **Goguen** | $1$ if $\mu_{\tilde A}\le\mu_{\tilde B}$ else $\mu_{\tilde B}/\mu_{\tilde A}$ |

> **Mamdani** and **Larsen** are popular in **engineering** controllers (not classical logic implications, but work well in practice).

---

## ✏️ 7.3 Solved Problem — GMP with Mamdani Implication

Universes $X=\{x_1,x_2\}$, $Y=\{y_1,y_2,y_3\}$.

Rule: IF $x$ is $\tilde A$ THEN $y$ is $\tilde B$, with $\tilde A=\tfrac{0.6}{x_1}+\tfrac{0.9}{x_2}$, $\tilde B=\tfrac{0.4}{y_1}+\tfrac{0.7}{y_2}+\tfrac{1.0}{y_3}$.

**Step 1 — Build relation $\tilde R$** (Mamdani = min):

$$
\tilde R = \begin{bmatrix} \min(0.6,0.4) & \min(0.6,0.7) & \min(0.6,1.0)\\ \min(0.9,0.4) & \min(0.9,0.7) & \min(0.9,1.0)\end{bmatrix} = \begin{bmatrix} 0.4 & 0.6 & 0.6\\ 0.4 & 0.7 & 0.9\end{bmatrix}
$$

**Step 2 — Fact:** $\tilde A' = \tfrac{0.5}{x_1}+\tfrac{0.8}{x_2}$.

**Step 3 — Inference (max-min):**
$$\mu_{\tilde B'}(y_1) = \max(\min(0.5,0.4),\,\min(0.8,0.4)) = \max(0.4,0.4) = 0.4$$
$$\mu_{\tilde B'}(y_2) = \max(\min(0.5,0.6),\,\min(0.8,0.7)) = \max(0.5,0.7) = 0.7$$
$$\mu_{\tilde B'}(y_3) = \max(\min(0.5,0.6),\,\min(0.8,0.9)) = \max(0.5,0.8) = 0.8$$

**Conclusion:** $\tilde B' = \tfrac{0.4}{y_1}+\tfrac{0.7}{y_2}+\tfrac{0.8}{y_3}$.

---

# 8. Fuzzy Rule-Based Systems & Inference

## 📘 8.1 Linguistic Variables & Hedges

A **linguistic variable** $\langle$ name, $T(\text{name})$, $U$, $G$, $M\rangle$:
- name e.g. *Age*
- term set $T$ = {young, old, very-young, somewhat-old…}
- universe $U=[0,120]$
- syntactic rule $G$ for generating terms
- semantic rule $M$ assigning MFs

### Linguistic Hedges (Modifiers)

Given fuzzy set $\tilde A$ with MF $\mu_{\tilde A}$, hedges produce new fuzzy sets:

| Hedge | Operation | Effect |
|---|---|---|
| **Very $A$** | $[\mu_{\tilde A}(x)]^2$ | Concentration — sharper |
| **More-or-less $A$** | $[\mu_{\tilde A}(x)]^{0.5}$ | Dilation — softer |
| **Extremely $A$** | $[\mu_{\tilde A}(x)]^3$ | Strong concentration |
| **Slightly $A$** | $[\mu_{\tilde A}(x)]^{0.33}$ | Strong dilation |
| **Indeed $A$** | $\begin{cases} 2\mu^2 & \mu\le 0.5 \\ 1-2(1-\mu)^2 & \mu>0.5 \end{cases}$ | Contrast intensification |
| **Not $A$** | $1-\mu_{\tilde A}(x)$ | Negation |
| **About $A$** | bell around peak | Approximation |

### ✏️ Example
"Tall" $= \tfrac{0.0}{150}+\tfrac{0.5}{170}+\tfrac{1.0}{180}$
"Very Tall" $= \tfrac{0.0}{150}+\tfrac{0.25}{170}+\tfrac{1.0}{180}$
"More-or-less Tall" $= \tfrac{0.0}{150}+\tfrac{0.707}{170}+\tfrac{1.0}{180}$

---

## 📘 8.2 Fuzzy Rule Base

A **fuzzy rule** has the form:
$$\text{IF } x_1 \text{ is } \tilde A_1 \text{ AND } x_2 \text{ is } \tilde A_2 \text{ THEN } y \text{ is } \tilde B$$

Multiple rules form a **rule base** $\{R_i\}_{i=1}^{N}$.

### Connectives within antecedent
- `AND` → t-norm (often min or product)
- `OR` → s-norm (often max)

### Aggregation of Rules
Once each rule fires to produce $\tilde B_i'$, all rule outputs are **combined**:
$$
\tilde B' \;=\; \bigcup_{i=1}^N \tilde B_i'
$$
Typical aggregation operators:

| Method | Definition |
|---|---|
| **Max** | $\mu_{\tilde B'}(y)=\max_i \mu_{\tilde B_i'}(y)$ — most common |
| **Sum** | $\sum_i \mu_{\tilde B_i'}(y)$ |
| **Probabilistic OR** | iteratively $a+b-ab$ |

---

## 📘 8.3 Fuzzy Inference System (FIS)

```
   Crisp input  ──►  Fuzzification  ──►  Rule Evaluation (Implication)
                                                 │
                                                 ▼
                                          Aggregation
                                                 │
                                                 ▼
                                       Defuzzification  ──►  Crisp output
```

---

## 📘 8.4 Mamdani Fuzzy Model (1975)

- **Antecedent:** fuzzy MFs
- **Consequent:** fuzzy MFs
- **Implication:** min (clipping) or product (scaling)
- **Aggregation:** max
- **Defuzzification:** Centroid / MOM / etc.

### Steps
1. Fuzzify each crisp input $x_0$ → $\mu_{\tilde A_i}(x_0)$.
2. Compute rule firing strength $w_i = T(\mu_{\tilde A_{i1}}(x_1^0),\dots)$.
3. **Implication**: clip/scale consequent MF by $w_i$ → $\tilde B_i'$.
4. **Aggregate** all $\tilde B_i'$ → $\tilde B'$.
5. **Defuzzify** $\tilde B'$ → crisp output $y^*$.

### Pros & Cons
✅ Intuitive, expressive consequents — easy to interpret.
❌ Computationally expensive (defuzzification on full fuzzy set).

---

## 📘 8.5 Sugeno (TSK) Fuzzy Model (Takagi-Sugeno-Kang, 1985)

- **Antecedent:** fuzzy
- **Consequent:** crisp **function** of inputs:
$$\text{IF } x_1 \text{ is } \tilde A_1 \text{ AND } x_2 \text{ is } \tilde A_2 \text{ THEN } y_i = f_i(x_1,x_2)$$

- **Zero-order Sugeno:** $f_i = c_i$ (constant)
- **First-order Sugeno:** $f_i = a_{i0}+a_{i1}x_1+a_{i2}x_2$

### Crisp output (weighted average)
$$
y^* \;=\; \frac{\sum_{i=1}^N w_i \cdot f_i(\mathbf{x})}{\sum_{i=1}^N w_i}
$$

### Pros & Cons
✅ Computationally efficient, no defuzzification step.
✅ Works seamlessly with adaptive techniques (ANFIS).
❌ Consequents less interpretable than Mamdani.

### Mamdani vs Sugeno

| Aspect | Mamdani | Sugeno |
|---|---|---|
| Consequent | Fuzzy MF | Linear / constant function |
| Defuzzification | Centroid etc. | Weighted average |
| Interpretability | High | Medium |
| Speed | Slow | Fast |
| Use case | Decision support, controllers requiring intuitive rules | Adaptive control, optimization |

---

## ✏️ 8.6 Solved Problem — Complete Mamdani FIS

**Problem:** Tip calculator. Inputs: *service* $(0–10)$, *food* $(0–10)$. Output: *tip* $(0–25\%)$.

**MFs**
- service: poor `(0,0,5)`, good `(0,5,10)`, excellent `(5,10,10)` (triangular)
- food: bad `(0,0,5)`, good `(5,10,10)`
- tip: low `(0,5,10)`, average `(10,15,20)`, high `(20,25,25)`

**Rules**
- R1: IF service is poor OR food is bad THEN tip is low
- R2: IF service is good THEN tip is average
- R3: IF service is excellent OR food is good THEN tip is high

**Input:** service = 3, food = 8.

**Step 1 — Fuzzification**

| Variable | poor | good | excellent | bad | good |
|---|---|---|---|---|---|
| service=3 | $(5-3)/5=0.4$ | $3/5=0.6$ | 0 | — | — |
| food=8 | — | — | — | 0 | $(8-5)/5=0.6$ |

**Step 2 — Rule firing** (OR=max, AND=min)
- $w_1 = \max(0.4, 0) = 0.4$ → tip = low
- $w_2 = 0.6$ → tip = average
- $w_3 = \max(0, 0.6) = 0.6$ → tip = high

**Step 3 — Implication (clip consequent)**
- low_clip = min(0.4, low)
- average_clip = min(0.6, average)
- high_clip = min(0.6, high)

**Step 4 — Aggregation:** max of the three clipped MFs ⇒ output fuzzy set $\tilde B'$.

**Step 5 — Defuzzification (centroid).** Approximate by sampling tip ∈ {0,5,10,15,20,25} and computing $z^*$. For symmetric triangles the centroid ≈ weighted average of peaks:

$$
y^* \approx \frac{0.4(5)+0.6(15)+0.6(25)}{0.4+0.6+0.6} = \frac{2+9+15}{1.6} = \frac{26}{1.6} \approx \mathbf{16.25\%}
$$

---

## ✏️ 8.7 Solved Problem — Zero-Order Sugeno

Same inputs, rules:
- R1: tip = 5
- R2: tip = 15
- R3: tip = 25

$$
y^* = \frac{0.4(5)+0.6(15)+0.6(25)}{0.4+0.6+0.6} = \frac{26}{1.6} = \mathbf{16.25\%}
$$

(In this case Mamdani-with-symmetric-peaks ≈ Sugeno result.)

---

# 9. Applications of Fuzzy Logic

## 📘 9.1 Home Appliances

### Washing Machine
- **Inputs:** dirt level (turbidity sensor), fabric type, load weight.
- **Outputs:** wash time, water level, agitation cycle, detergent quantity.
- **Sample rule:** IF dirt is HIGH AND fabric is HARD THEN wash-time is LONG.

### Air Conditioner
- **Inputs:** room temperature, humidity, occupancy.
- **Outputs:** compressor speed, fan speed.
- **Sample rule:** IF temp is HOT AND humidity is HIGH THEN cooling is STRONG.

### Rice Cooker, Refrigerator, Microwave, Vacuum cleaner
- Similar fuzzy controllers; Japan ("Sendai Subway", 1987) is the **classic large-scale industrial example**.

---

## 📘 9.2 General Fuzzy Logic Controller (FLC)

```
                    ┌────────────────────┐
                    │     Plant /        │
   r(t) ─┐         │     Process        │
         │         └──────┬─────────────┘
         ▼                │ y(t)
       ┌───┐  e(t)  ┌─────┴────┐   crisp
       │ + │──────► │  Fuzzy   │ ◄────────┐
       └───┘        │ Logic    │   sensors│
         ▲          │ Control. │           │
         │          └─────┬────┘           │
         │ y(t)           │ u(t)           │
         └────────────────┴────────────────┘
```

- **Inputs:** error $e=r-y$, rate $\dot e$.
- **MFs:** NB, NM, NS, ZE, PS, PM, PB (negative big, … positive big).
- **Rule table (FAM — Fuzzy Associative Memory):**

|  $\dot e\backslash e$ | NB | NM | NS | ZE | PS | PM | PB |
|---|---|---|---|---|---|---|---|
| **NB** | NB | NB | NB | NM | NS | ZE | PS |
| **NM** | NB | NB | NM | NS | ZE | PS | PM |
| **NS** | NB | NM | NS | ZE | PS | PM | PB |
| **ZE** | NM | NS | ZE | ZE | ZE | PS | PM |
| **PS** | NM | NS | ZE | PS | PS | PM | PB |
| **PM** | NM | NS | ZE | PS | PM | PB | PB |
| **PB** | NS | ZE | PS | PM | PB | PB | PB |

Output $u$ = controller signal (e.g., motor voltage).

---

## 📘 9.3 Medical Diagnosis (Fuzzy Inference)

### Approach
- Symptoms $S=\{s_1,\dots,s_m\}$, diseases $D=\{d_1,\dots,d_n\}$.
- Fuzzy relation $\tilde R$ on $S\times D$: $\mu_{\tilde R}(s,d)=$ how strongly $s$ indicates $d$.
- Patient profile $\tilde P$ on $S$.
- Diagnosis: $\tilde D = \tilde P \circ \tilde R$ (max-min).

### ✏️ Example
$S=\{\text{fever, cough, fatigue}\}$, $D=\{\text{flu, cold}\}$.

$$
\tilde R = \begin{bmatrix} 0.9 & 0.4 \\ 0.6 & 0.8 \\ 0.7 & 0.3\end{bmatrix},\quad
\tilde P = (0.8,\,0.5,\,0.6)
$$

$\mu_{\tilde D}(\text{flu}) = \max(\min(0.8,0.9),\,\min(0.5,0.6),\,\min(0.6,0.7)) = \max(0.8,0.5,0.6) = \mathbf{0.8}$
$\mu_{\tilde D}(\text{cold}) = \max(\min(0.8,0.4),\,\min(0.5,0.8),\,\min(0.6,0.3)) = \max(0.4,0.5,0.3) = \mathbf{0.5}$

⇒ Flu is the more likely diagnosis.

---

## 📘 9.4 Weather Forecasting

- **Inputs:** temperature, humidity, pressure trend, wind speed, cloud cover.
- **Linguistic terms:** low / medium / high.
- **Sample rules:**
  - IF pressure is FALLING AND humidity is HIGH THEN rain-chance is HIGH.
  - IF temp is HIGH AND humidity is LOW AND wind is LOW THEN weather is SUNNY.
- **Output:** probability of rain, expected temperature range — defuzzified into crisp forecast.

Advantages over Bayesian-only forecasting: copes with linguistic expert knowledge, handles missing/noisy data.

---

# 10. Quick Revision Cheat-Sheet

## 📝 Classical vs Fuzzy
- Crisp: $\chi_A \in \{0,1\}$. Fuzzy: $\mu_{\tilde A}\in[0,1]$.
- All classical laws hold for fuzzy EXCEPT **Excluded Middle** & **Contradiction**.

## 📝 Operations
- $\cup=\max$, $\cap=\min$, $\bar{}=1-\mu$ (Zadeh standard).
- Generalized: t-norm (AND), s-norm (OR).
- Algebraic: product $a\cdot b$; algebraic sum $a+b-ab$.

## 📝 Fuzzy Relations
- $\mu_{\tilde R}:X\times Y\to [0,1]$ — matrix form.
- **Max-min composition**: $\max_y\min(\mu_R,\mu_S)$.
- Properties: reflexive, symmetric, transitive ⇒ fuzzy equivalence.

## 📝 MF & Fuzzification
- Features: core, support, boundary, height, crossover.
- Convex iff every α-cut is convex (theorem).
- Standard: triangular, trapezoidal, Gaussian, bell, sigmoid.
- Methods: singleton, Gaussian, expert, NN, GA, inductive.

## 📝 λ-Cut & Defuzzification
- $A_\lambda=\{x:\mu(x)\ge\lambda\}$ — nested.
- Decomposition: $\tilde A=\bigcup_\lambda \lambda\cdot A_\lambda$.
- Centroid $z^*=\dfrac{\sum z\mu}{\sum\mu}$ — most common.
- MOM, SOM, LOM, Bisector, Weighted-Avg (Sugeno).

## 📝 Implication & GMP
- Mamdani = min, Larsen = product.
- GMP: $\tilde B'=\tilde A' \circ \tilde R$.

## 📝 Linguistic Hedges
- very = $\mu^2$, more-or-less = $\mu^{0.5}$, extremely = $\mu^3$.

## 📝 Mamdani vs Sugeno
| | Mamdani | Sugeno |
|---|---|---|
| Output | Fuzzy MF | Crisp function |
| Defuzz | Centroid | Weighted avg |
| Speed | Slow | Fast |
| Use | Interpretable rules | Adaptive control / ANFIS |

## 📝 Applications
- Washing machine, AC, rice cooker, vacuum, ABS brakes.
- Medical diagnosis via max-min composition $\tilde D=\tilde P\circ \tilde R$.
- Weather forecasting (rules from meteorologists).
- General FLC with FAM table over $(e,\dot e)$.

---

> **End of Unit 2 — Fuzzy Sets, Logic & Systems.**
> *Next: Unit 3 (share when ready — likely Neural Networks in depth or Genetic Algorithms in depth).*
