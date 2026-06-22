# Soft Computing — Unit 1: Introduction

> **Syllabus (8 Hrs):** Introduction to soft computing; introduction to fuzzy sets and fuzzy logic systems; introduction to biological and artificial neural networks; introduction to Genetic Algorithm.

---

## Table of Contents

1. [Introduction to Soft Computing](#1-introduction-to-soft-computing)
2. [Fuzzy Sets and Fuzzy Logic Systems](#2-fuzzy-sets-and-fuzzy-logic-systems)
3. [Biological and Artificial Neural Networks](#3-biological-and-artificial-neural-networks)
4. [Genetic Algorithms](#4-genetic-algorithms)
5. [Quick Revision Cheat-Sheet](#5-quick-revision-cheat-sheet)

---

# 1. Introduction to Soft Computing

## 📘 1.1 Theory

**Soft Computing (SC)** is a collection of computational techniques in computer science that — *unlike conventional (hard) computing* — is **tolerant of imprecision, uncertainty, partial truth, and approximation**. The guiding principle, given by **Prof. Lotfi A. Zadeh (1994)**, is:

> *"The role model for soft computing is the human mind."*

The aim is to **exploit tolerance for imprecision** to achieve tractability, robustness, low solution-cost, and a better rapport with reality.

### Characteristics of Soft Computing

| Property | Meaning |
|---|---|
| **Approximation** | Solutions are *good-enough*, not necessarily exact. |
| **Uncertainty handling** | Works with vague/noisy/partial data. |
| **Learning ability** | Improves from examples (data-driven). |
| **Bio-inspired** | Mimics biological & evolutionary processes. |
| **Parallelism** | Naturally parallel architectures (e.g., neural nets). |
| **Robustness** | Performs gracefully under noise & faults. |

### Components (Pillars) of Soft Computing

```
              ┌──────────────────────────┐
              │     SOFT COMPUTING       │
              └──────────────────────────┘
                          │
   ┌──────────────┬───────┴───────┬───────────────────┐
   ▼              ▼               ▼                   ▼
Fuzzy Logic   Neural Nets   Evolutionary Comp.   Probabilistic
 (Reasoning)  (Learning)    (Optimization: GA)    Reasoning
                                                  (BBN, Bayesian)
```

1. **Fuzzy Logic (FL)** — Approximate reasoning with linguistic variables.
2. **Artificial Neural Networks (ANN)** — Learning from data; pattern recognition.
3. **Evolutionary Computation (EC)** — Population-based optimization (GA, GP, ES).
4. **Probabilistic Reasoning (PR)** — Bayesian nets, belief networks, chaos theory.

These methods are **complementary** rather than competing — they are often combined into **Hybrid Soft Computing Systems** (e.g., Neuro-Fuzzy, Genetic-Fuzzy, Neuro-Genetic).

---

## 📘 1.2 Hard Computing vs Soft Computing

| Feature | Hard Computing | Soft Computing |
|---|---|---|
| Basis | Binary / Boolean logic | Multi-valued / Fuzzy logic |
| Precision | Exact answers required | Approximate answers acceptable |
| Computation | Sequential | Parallel |
| Data | Precise data | Imprecise / noisy data |
| Model | Mathematical (deterministic) | Empirical / bio-inspired |
| Cost | High | Low |
| Examples | Numerical methods, sorting, search | ANN, Fuzzy, GA |

---

## 🧮 1.3 Mathematical Foundation

A **soft-computing system** can be viewed as a mapping:

$$
f : X \subseteq \mathbb{R}^n \;\longrightarrow\; Y \subseteq \mathbb{R}^m
$$

approximated by a parameterized family $\hat{f}(\mathbf{x};\boldsymbol{\theta})$ where the parameter vector $\boldsymbol{\theta}$ is **learned** or **evolved** to minimize an error functional:

$$
\boldsymbol{\theta}^{*} \;=\; \arg\min_{\boldsymbol{\theta}} \; E(\boldsymbol{\theta})
\;=\; \arg\min_{\boldsymbol{\theta}} \; \frac{1}{N}\sum_{i=1}^{N} L\bigl(y_i,\hat{f}(\mathbf{x}_i;\boldsymbol{\theta})\bigr)
$$

where $L(\cdot,\cdot)$ is a loss function.

---

## 💡 1.4 Applications

- Handwriting / speech / face recognition
- Medical diagnosis (e.g., fuzzy cancer-risk classifier)
- Weather forecasting
- Autonomous driving & robotics
- Stock-market prediction
- Smart appliances (washing machines, ACs, rice cookers)
- Image compression & enhancement
- Power-system load forecasting

---

# 2. Fuzzy Sets and Fuzzy Logic Systems

## 📘 2.1 Need for Fuzzy Logic

Real-world concepts (*"tall man"*, *"warm water"*, *"fast car"*) cannot be modelled with **crisp** (yes/no) sets. **Lotfi Zadeh (1965)** proposed **Fuzzy Sets** to capture *degrees of membership*.

### Crisp Set vs Fuzzy Set

| | Crisp Set $A$ | Fuzzy Set $\tilde{A}$ |
|---|---|---|
| Membership $\mu_A(x)$ | $\{0,1\}$ | $[0,1]$ |
| Boundary | Sharp | Gradual |
| Notation | $A = \{x : P(x)\}$ | $\tilde{A} = \{(x, \mu_{\tilde A}(x)) : x \in X\}$ |

---

## 🧮 2.2 Formal Definitions

### Fuzzy Set

A fuzzy set $\tilde{A}$ over a universe of discourse $X$ is defined by its **membership function**:

$$
\mu_{\tilde A} : X \;\longrightarrow\; [0,1]
$$

**Discrete representation:**

$$
\tilde{A} \;=\; \sum_{x_i \in X} \frac{\mu_{\tilde A}(x_i)}{x_i}
\quad\text{(Zadeh's notation; '+' and '/' are NOT arithmetic)}
$$

**Continuous representation:**

$$
\tilde{A} \;=\; \int_X \frac{\mu_{\tilde A}(x)}{x}
$$

### Support, Core, Height, $\alpha$-Cut

| Term | Definition |
|---|---|
| **Support** | $\operatorname{supp}(\tilde A) = \{x \in X : \mu_{\tilde A}(x) > 0\}$ |
| **Core** | $\operatorname{core}(\tilde A) = \{x \in X : \mu_{\tilde A}(x) = 1\}$ |
| **Height** | $h(\tilde A) = \sup_{x \in X}\mu_{\tilde A}(x)$ |
| **Normal set** | $h(\tilde A)=1$ |
| **$\alpha$-cut** | $A_\alpha = \{x : \mu_{\tilde A}(x) \ge \alpha\}$ |
| **Crossover point** | $x$ such that $\mu_{\tilde A}(x) = 0.5$ |

---

## 🧮 2.3 Common Membership Functions

### Triangular

$$
\mu(x;\,a,b,c) \;=\; \max\!\left(\min\!\left(\frac{x-a}{b-a},\,\frac{c-x}{c-b}\right),\,0\right)
$$

### Trapezoidal

$$
\mu(x;\,a,b,c,d) \;=\; \max\!\left(\min\!\left(\frac{x-a}{b-a},\,1,\,\frac{d-x}{d-c}\right),\,0\right)
$$

### Gaussian

$$
\mu(x;\,c,\sigma) \;=\; \exp\!\left(-\frac{(x-c)^2}{2\sigma^2}\right)
$$

### Sigmoidal

$$
\mu(x;\,a,c) \;=\; \frac{1}{1+e^{-a(x-c)}}
$$

### Bell-shaped (Generalized)

$$
\mu(x;\,a,b,c) \;=\; \frac{1}{1+\left|\dfrac{x-c}{a}\right|^{2b}}
$$

---

## 🧮 2.4 Operations on Fuzzy Sets

Let $\tilde A, \tilde B$ be fuzzy sets over $X$.

| Operation | Definition (Zadeh's standard) |
|---|---|
| **Union** | $\mu_{\tilde A \cup \tilde B}(x) = \max(\mu_{\tilde A}(x),\,\mu_{\tilde B}(x))$ |
| **Intersection** | $\mu_{\tilde A \cap \tilde B}(x) = \min(\mu_{\tilde A}(x),\,\mu_{\tilde B}(x))$ |
| **Complement** | $\mu_{\bar{\tilde A}}(x) = 1 - \mu_{\tilde A}(x)$ |
| **Equality** | $\mu_{\tilde A}(x) = \mu_{\tilde B}(x) \;\forall x$ |
| **Containment** | $\tilde A \subseteq \tilde B \iff \mu_{\tilde A}(x) \le \mu_{\tilde B}(x) \;\forall x$ |
| **Product** | $\mu_{\tilde A \cdot \tilde B}(x) = \mu_{\tilde A}(x)\cdot\mu_{\tilde B}(x)$ |
| **Algebraic sum** | $\mu_{\tilde A + \tilde B}(x) = \mu_{\tilde A}(x)+\mu_{\tilde B}(x)-\mu_{\tilde A}(x)\mu_{\tilde B}(x)$ |
| **Bounded sum** | $\mu(x)=\min(1,\mu_{\tilde A}(x)+\mu_{\tilde B}(x))$ |
| **Bounded difference** | $\mu(x)=\max(0,\mu_{\tilde A}(x)-\mu_{\tilde B}(x))$ |

**t-norms (generalized intersection):** $\min$, product, Łukasiewicz $\max(0,a+b-1)$.
**t-conorms / s-norms (generalized union):** $\max$, algebraic sum, $\min(1,a+b)$.

---

## 📐 2.5 Important Properties / Theorems

For fuzzy sets, **most** of the classical set-theoretic laws hold (with $\max/\min$ semantics):

| Law | Statement |
|---|---|
| Commutativity | $\tilde A \cup \tilde B = \tilde B \cup \tilde A$ |
| Associativity | $(\tilde A \cup \tilde B)\cup \tilde C = \tilde A \cup(\tilde B \cup \tilde C)$ |
| Distributivity | $\tilde A \cap (\tilde B \cup \tilde C) = (\tilde A \cap \tilde B)\cup(\tilde A \cap \tilde C)$ |
| Idempotency | $\tilde A \cup \tilde A = \tilde A$ |
| Identity | $\tilde A \cup \varnothing = \tilde A,\;\tilde A \cap X = \tilde A$ |
| De Morgan's | $\overline{\tilde A \cup \tilde B} = \bar{\tilde A}\cap \bar{\tilde B}$ |
| Involution | $\overline{\overline{\tilde A}} = \tilde A$ |

> ⚠️ **Important exception:** The **Law of Excluded Middle** and **Law of Contradiction** **DO NOT** hold for fuzzy sets:
>
> $$\tilde A \cup \bar{\tilde A} \;\ne\; X, \qquad \tilde A \cap \bar{\tilde A} \;\ne\; \varnothing$$

### 📐 Decomposition (Representation) Theorem

Any fuzzy set $\tilde A$ can be represented as the union of its $\alpha$-cuts:

$$
\tilde A \;=\; \bigcup_{\alpha \in (0,1]} \alpha \cdot A_\alpha
\quad\text{where}\quad
\mu_{\alpha A_\alpha}(x) =
\begin{cases} \alpha & x \in A_\alpha \\ 0 & \text{otherwise}\end{cases}
$$

### 📐 Extension Principle (Zadeh)

If $f:X \to Y$ and $\tilde A$ is a fuzzy set on $X$, then the fuzzy set $\tilde B = f(\tilde A)$ on $Y$ is:

$$
\mu_{\tilde B}(y) \;=\; \sup_{x:\,y = f(x)} \mu_{\tilde A}(x)
$$

---

## ✏️ 2.6 Solved Problems

### ✏️ Problem 1 — Basic Operations

Given $X=\{1,2,3,4,5\}$ and

$$
\tilde A = \frac{0.2}{1}+\frac{0.5}{2}+\frac{0.8}{3}+\frac{1.0}{4}+\frac{0.3}{5}
$$

$$
\tilde B = \frac{0.6}{1}+\frac{0.4}{2}+\frac{0.7}{3}+\frac{0.5}{4}+\frac{0.9}{5}
$$

Find $\tilde A \cup \tilde B,\; \tilde A \cap \tilde B,\; \bar{\tilde A}$.

**Solution:**

| $x$ | $\mu_{\tilde A}$ | $\mu_{\tilde B}$ | $\max$ (Union) | $\min$ (Intersection) | $1-\mu_{\tilde A}$ |
|:-:|:-:|:-:|:-:|:-:|:-:|
| 1 | 0.2 | 0.6 | **0.6** | **0.2** | 0.8 |
| 2 | 0.5 | 0.4 | **0.5** | **0.4** | 0.5 |
| 3 | 0.8 | 0.7 | **0.8** | **0.7** | 0.2 |
| 4 | 1.0 | 0.5 | **1.0** | **0.5** | 0.0 |
| 5 | 0.3 | 0.9 | **0.9** | **0.3** | 0.7 |

$$
\tilde A \cup \tilde B = \tfrac{0.6}{1}+\tfrac{0.5}{2}+\tfrac{0.8}{3}+\tfrac{1.0}{4}+\tfrac{0.9}{5}
$$

$$
\tilde A \cap \tilde B = \tfrac{0.2}{1}+\tfrac{0.4}{2}+\tfrac{0.7}{3}+\tfrac{0.5}{4}+\tfrac{0.3}{5}
$$

$$
\bar{\tilde A} = \tfrac{0.8}{1}+\tfrac{0.5}{2}+\tfrac{0.2}{3}+\tfrac{0.0}{4}+\tfrac{0.7}{5}
$$

---

### ✏️ Problem 2 — α-Cut

Using $\tilde A$ above, find $A_{0.5}$ and $A_{0.8}$.

**Solution:** Pick elements with $\mu \ge \alpha$.

- $A_{0.5} = \{2,3,4\}$ (since $\mu = 0.5,0.8,1.0$).
- $A_{0.8} = \{3,4\}$.

---

### ✏️ Problem 3 — Triangular Membership

Define **"warm"** temperature with triangular MF $(20,25,30)$. Find $\mu(22)$ and $\mu(27)$.

$$
\mu(22) = \frac{22-20}{25-20} = \frac{2}{5} = 0.4
$$

$$
\mu(27) = \frac{30-27}{30-25} = \frac{3}{5} = 0.6
$$

---

## 📘 2.7 Fuzzy Logic Systems (FLS)

A **Fuzzy Inference System (FIS)** maps crisp inputs to crisp outputs via fuzzy rules.

```
   Crisp                                                Crisp
  inputs                                              outputs
    │                                                    ▲
    ▼                                                    │
┌──────────────┐    ┌─────────────┐    ┌──────────────┐  │
│ Fuzzifier    │──► │ Inference   │──► │ Defuzzifier  │──┘
└──────────────┘    │  Engine     │    └──────────────┘
                    └─────────────┘
                          ▲
                          │
                    ┌─────────────┐
                    │ Rule Base   │
                    │ (IF-THEN)   │
                    └─────────────┘
                    ┌─────────────┐
                    │ Database    │
                    │ (MFs)       │
                    └─────────────┘
```

### Stages

1. **Fuzzification** — Crisp $x$ → fuzzy membership values.
2. **Rule Base** — IF–THEN rules from expert knowledge.
   *Example:* IF temperature is HIGH AND humidity is HIGH THEN fan-speed is FAST.
3. **Inference Engine** — Combines rules using **Mamdani** or **Sugeno** methods.
4. **Defuzzification** — Fuzzy output → crisp value.

### Defuzzification Methods

| Method | Formula |
|---|---|
| **Centroid (COG)** | $x^* = \dfrac{\int x\,\mu(x)\,dx}{\int \mu(x)\,dx}$ |
| **Bisector** | $x^*$ such that $\int_{a}^{x^*}\mu(x)dx = \int_{x^*}^{b}\mu(x)dx$ |
| **Mean of Maxima (MOM)** | Average $x$ where $\mu(x)$ peaks |
| **Smallest of Max (SOM)** | Smallest $x$ where $\mu$ is max |
| **Largest of Max (LOM)** | Largest $x$ where $\mu$ is max |
| **Weighted Average** | $x^* = \dfrac{\sum w_i x_i}{\sum w_i}$ |

---

### ✏️ Problem 4 — Centroid Defuzzification

Fuzzy output:

| $x$ | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| $\mu(x)$ | 0.2 | 0.5 | 0.8 | 0.6 | 0.3 |

$$
x^* = \frac{\sum x_i\mu(x_i)}{\sum \mu(x_i)}
= \frac{1(0.2)+2(0.5)+3(0.8)+4(0.6)+5(0.3)}{0.2+0.5+0.8+0.6+0.3}
$$

$$
= \frac{0.2+1.0+2.4+2.4+1.5}{2.4}
= \frac{7.5}{2.4} \approx \mathbf{3.125}
$$

---

# 3. Biological and Artificial Neural Networks

## 📘 3.1 Biological Neuron

The human brain contains ≈ **$10^{11}$ neurons** with ≈ **$10^{14}$ synaptic connections**.

```
         Dendrites (inputs)
              │
              ▼
        ┌───────────┐
        │  Soma     │  ← Cell body (integrates signals)
        │ (Nucleus) │
        └─────┬─────┘
              │ Axon (output cable)
              ▼
          Axon terminals
              │
              ▼
          Synapse  ──► next neuron's dendrite
```

| Component | Function |
|---|---|
| **Dendrites** | Receive signals from other neurons |
| **Soma (cell body)** | Sums incoming signals; if threshold crossed → fires |
| **Axon** | Carries output signal away |
| **Synapse** | Junction; modulates signal strength (weight) |
| **Myelin sheath** | Insulator, speeds up signal propagation |

**Signal:** electrochemical impulse (**action potential**) — *"all-or-none"* law.

---

## 📘 3.2 Biological vs Artificial Neuron

| Biological Neuron | Artificial Neuron |
|---|---|
| Dendrite | Input $x_i$ |
| Synapse | Weight $w_i$ |
| Soma | Summation $\Sigma$ + activation $f$ |
| Axon | Output $y$ |
| ~ms response | ns – $\mu$s response |
| Highly parallel | Mostly simulated parallelism |
| ~$10^{11}$ neurons | $10^2$ – $10^9$ (in DNNs) |
| Adapts (plasticity) | Adapts via learning algorithm |

---

## 🧮 3.3 McCulloch–Pitts Neuron (1943)

The earliest mathematical neuron model:

```
   x1 ──w1──►┐
   x2 ──w2──►│  Σ ─► f(net) ─► y
   ...       │
   xn ──wn──►┘
```

**Net input:**

$$
\text{net} \;=\; \sum_{i=1}^{n} w_i x_i \;-\; \theta
$$

**Output (binary step):**

$$
y \;=\; f(\text{net}) \;=\;
\begin{cases}
1, & \text{net} \ge 0 \\
0, & \text{net} < 0
\end{cases}
$$

where $\theta$ is the **threshold** (bias).

---

## 🧮 3.4 Activation Functions

| Name | Formula | Range |
|---|---|---|
| **Step / Heaviside** | $f(x) = \begin{cases}1 & x \ge 0\\0 & x<0\end{cases}$ | $\{0,1\}$ |
| **Signum** | $f(x) = \operatorname{sgn}(x)$ | $\{-1,0,1\}$ |
| **Linear** | $f(x) = x$ | $\mathbb{R}$ |
| **Sigmoid (logistic)** | $f(x) = \dfrac{1}{1+e^{-x}}$ | $(0,1)$ |
| **Tanh** | $f(x) = \dfrac{e^x - e^{-x}}{e^x + e^{-x}}$ | $(-1,1)$ |
| **ReLU** | $f(x) = \max(0,x)$ | $[0,\infty)$ |
| **Leaky ReLU** | $f(x) = \max(0.01x,\,x)$ | $\mathbb{R}$ |
| **Softmax** | $f_i(\mathbf{x}) = \dfrac{e^{x_i}}{\sum_j e^{x_j}}$ | $(0,1)$, sums to 1 |

**Sigmoid derivative (useful for BP):** $f'(x) = f(x)\,(1-f(x))$.

---

## 📘 3.5 Architectures of ANN

1. **Single-Layer Feed-Forward** — Perceptron.
2. **Multi-Layer Feed-Forward (MLP)** — Input, hidden, output layers; trained by back-propagation.
3. **Recurrent (RNN)** — Contains feedback loops; handles sequential data (Hopfield, LSTM).
4. **Self-Organizing Map (SOM, Kohonen)** — Unsupervised; topology-preserving.
5. **Radial Basis Function (RBF) Network** — Local activation, fast learning.
6. **Convolutional NN (CNN)** — For images.

---

## 📘 3.6 Learning Paradigms

| Type | Description | Examples |
|---|---|---|
| **Supervised** | Input + target given | Perceptron, BP, RBF |
| **Unsupervised** | Only input, find structure | SOM, Hebbian, ART |
| **Reinforcement** | Reward / penalty feedback | Q-learning, TD |

### Learning Rules

| Rule | Update equation |
|---|---|
| **Hebbian** | $\Delta w_{ij} = \eta\,x_i\,y_j$ |
| **Perceptron** | $\Delta w_i = \eta\,(t-y)\,x_i$ |
| **Delta (Widrow–Hoff)** | $\Delta w_i = \eta\,(t-y)\,f'(\text{net})\,x_i$ |
| **Competitive** | $\Delta w_{ij} = \eta\,(x_i - w_{ij})$ if neuron $j$ wins |
| **Correlation** | $\Delta w_{ij} = \eta\,x_i\,t_j$ |
| **Outstar (Grossberg)** | $\Delta w_{ij} = \eta\,(t_j - w_{ij})$ |

Here $\eta$ is the **learning rate**, $t$ is target, $y$ is actual output.

---

## ✏️ 3.7 Solved Problems

### ✏️ Problem 5 — McCulloch–Pitts AND Gate

Design an M-P neuron that computes the logical AND of two binary inputs $x_1, x_2$.

**Solution:** Take $w_1=w_2=1$, $\theta = 2$.

| $x_1$ | $x_2$ | net $=x_1+x_2-2$ | $y$ |
|:-:|:-:|:-:|:-:|
| 0 | 0 | −2 | 0 |
| 0 | 1 | −1 | 0 |
| 1 | 0 | −1 | 0 |
| 1 | 1 | 0 | **1** |

Output matches AND truth-table.

---

### ✏️ Problem 6 — Perceptron Learning (1 step)

Initial weights $w_1=0.2, w_2=-0.1, b=0.0$. Input $(x_1,x_2)=(1,1)$, target $t=1$, learning rate $\eta=0.5$, activation = step.

**Step 1: net input**

$$\text{net} = (1)(0.2)+(1)(-0.1)+0 = 0.1 \ge 0 \Rightarrow y = 1$$

Since $y = t$, weights unchanged.

Now feed $(1,0)$, target $t=0$:

$$\text{net} = 0.2 + 0 + 0 = 0.2 \ge 0 \Rightarrow y = 1$$

Error $e = t - y = -1$. Update:

$$w_1 \leftarrow 0.2 + (0.5)(-1)(1) = -0.3$$
$$w_2 \leftarrow -0.1 + (0.5)(-1)(0) = -0.1$$
$$b   \leftarrow 0   + (0.5)(-1)     = -0.5$$

New weights: $(w_1,w_2,b) = (-0.3,-0.1,-0.5)$.

---

## 📐 3.8 Important Theorems

### 📐 Perceptron Convergence Theorem (Rosenblatt, 1962)
If the training set is **linearly separable**, the perceptron learning algorithm converges in a **finite** number of steps to a weight vector that classifies all examples correctly.

### 📐 Universal Approximation Theorem (Cybenko 1989; Hornik 1991)
A feed-forward network with **a single hidden layer** containing a *finite* number of neurons and a **non-constant, bounded, continuous** activation function (e.g., sigmoid) can approximate any continuous function $f:\mathbb{R}^n \to \mathbb{R}^m$ on a compact set to **arbitrary precision**.

### 📐 XOR Limitation (Minsky & Papert, 1969)
A **single-layer perceptron cannot** solve the XOR problem because XOR is **not linearly separable**. At least one hidden layer is required.

---

# 4. Genetic Algorithms

## 📘 4.1 Inspiration

Proposed by **John Holland (1975)** — a **population-based metaheuristic** inspired by **Darwinian natural selection** and **Mendelian genetics**.

**Key idea:** Encode candidate solutions as *chromosomes*. Evolve them through *selection*, *crossover*, and *mutation* across generations; better solutions (higher *fitness*) survive and reproduce.

---

## 📘 4.2 Terminology

| GA Term | Biology | Meaning |
|---|---|---|
| **Chromosome** | DNA strand | Encoded candidate solution (string of genes) |
| **Gene** | DNA segment | One variable / bit |
| **Allele** | Variant of gene | Possible value of a gene |
| **Locus** | Position on chromosome | Index in string |
| **Genotype** | Encoded form | Bit string `10110` |
| **Phenotype** | Decoded form | Real-world value (e.g., $x=22$) |
| **Population** | Group | Set of chromosomes |
| **Fitness** | Survival ability | Objective-function value |
| **Generation** | Lifecycle | One iteration |

---

## 📘 4.3 GA Workflow

```
        ┌─────────────────────────────┐
        │  Initialize Population (P0) │
        └─────────────┬───────────────┘
                      ▼
        ┌─────────────────────────────┐
        │  Evaluate Fitness           │
        └─────────────┬───────────────┘
                      ▼
                ┌─────────────┐  No
       ┌───────►│ Terminate?  ├───────┐
       │        └──────┬──────┘       │
       │               │ Yes          ▼
       │               ▼      ┌────────────────┐
       │            Return    │   Selection    │
       │            best      └───────┬────────┘
       │                              ▼
       │                      ┌────────────────┐
       │                      │   Crossover    │
       │                      └───────┬────────┘
       │                              ▼
       │                      ┌────────────────┐
       │                      │   Mutation     │
       │                      └───────┬────────┘
       │                              ▼
       │                       New Generation
       └──────────────────────────────┘
```

### Algorithm (Pseudo-code)

```text
Initialize population P(0) randomly
Evaluate fitness of each individual in P(0)
t ← 0
while (termination condition not met) do
    Select parents from P(t) using a selection scheme
    Apply crossover with probability p_c → offspring
    Apply mutation with probability p_m → mutated offspring
    Evaluate fitness of offspring
    Form P(t+1) by replacement (elitism / generational)
    t ← t + 1
return best individual in P(t)
```

---

## 🧮 4.4 GA Operators

### Selection

| Scheme | Idea |
|---|---|
| **Roulette Wheel** | $p_i = \dfrac{f_i}{\sum_j f_j}$ |
| **Tournament** | Pick $k$ random; choose fittest |
| **Rank-based** | Sort by fitness; assign probabilities by rank |
| **Stochastic Universal Sampling** | $N$ equally-spaced pointers on wheel |
| **Elitism** | Carry best $e$ individuals unchanged |

### Crossover (Recombination)

| Type | Description |
|---|---|
| **Single-point** | Pick locus $k$; swap suffixes after $k$ |
| **Two-point** | Pick two loci; swap middle segment |
| **Uniform** | For each gene, swap with probability 0.5 |
| **Arithmetic** | $c = \alpha\,p_1 + (1-\alpha)\,p_2$ for real-valued |

### Mutation

| Type | Description |
|---|---|
| **Bit-flip** | Flip a bit with probability $p_m$ |
| **Swap** | Swap two genes |
| **Inversion** | Reverse a sub-string |
| **Gaussian** | Add $\mathcal{N}(0,\sigma^2)$ noise (real-valued) |

### Probabilities — typical values

- Crossover: $p_c \in [0.6,\,0.95]$
- Mutation: $p_m \in [0.001,\,0.05]$

---

## 📐 4.5 Schema Theorem (Holland, 1975)

A **schema** $H$ is a template (e.g., `1*0*1`) representing a similarity subset of chromosomes.

Define:
- $m(H,t)$ = number of strings matching $H$ at generation $t$
- $f(H)$ = average fitness of strings matching $H$
- $\bar f$ = average fitness of population
- $o(H)$ = **order** = # of fixed (non-`*`) positions
- $\delta(H)$ = **defining length** = distance between first and last fixed position
- $L$ = chromosome length, $p_c$ = crossover prob, $p_m$ = mutation prob

$$
\boxed{\;
m(H, t+1) \;\ge\; m(H, t)\cdot\frac{f(H)}{\bar f}
\cdot\left[1 - p_c\,\frac{\delta(H)}{L-1}\right]
\cdot\left[1 - p_m\right]^{o(H)}
\;}
$$

**Building Block Hypothesis (corollary):** GAs work by combining **short, low-order, high-fitness** schemata (*building blocks*) into better solutions.

---

## ✏️ 4.6 Solved Problem — Maximize $f(x)=x^2$ on $\{0,\dots,31\}$

**Encoding:** 5-bit binary string ⇒ chromosome length $L=5$.

**Initial population (random):**

| Chromosome | Decoded $x$ | $f(x)=x^2$ |
|:--:|:--:|:--:|
| `01101` | 13 | 169 |
| `11000` | 24 | 576 |
| `01000` |  8 |  64 |
| `10011` | 19 | 361 |
| **Total** | | **1170** |
| **Avg** | | **292.5** |

**Roulette-wheel selection probabilities:**

| String | $f_i$ | $p_i = f_i/\sum f_j$ | Expected count $f_i/\bar f$ |
|:--:|:--:|:--:|:--:|
| `01101` | 169 | 0.144 | 0.58 |
| `11000` | 576 | 0.492 | 1.97 |
| `01000` |  64 | 0.055 | 0.22 |
| `10011` | 361 | 0.309 | 1.23 |

Assume mating pool after selection: `{01101, 11000, 11000, 10011}`.

**Single-point crossover** at point 4 between `01101` and `11000`:

```
Parent 1: 0110 | 1     Child 1: 0110 | 0  → 01100 = 12
Parent 2: 1100 | 0     Child 2: 1100 | 1  → 11001 = 25
```

**Crossover** at point 2 between `11000` and `10011`:

```
Parent 1: 11 | 000     Child 1: 11 | 011 → 11011 = 27
Parent 2: 10 | 011     Child 2: 10 | 000 → 10000 = 16
```

**Mutation:** flip bit 3 of `11011` → `11111` = 31, $f = 961$. 🎉

**New population:**

| Chromosome | $x$ | $f(x)$ |
|:--:|:--:|:--:|
| `01100` | 12 | 144 |
| `11001` | 25 | 625 |
| `11111` | 31 | **961** |
| `10000` | 16 | 256 |
| **Total** | | **1986** |
| **Avg** | | **496.5** |

Average fitness rose from **292.5 → 496.5**; best individual reached the **optimum** $x=31$. ✅

---

## 📘 4.7 Advantages & Limitations of GA

**✅ Advantages**
- Works with any objective (no derivatives needed).
- Excellent for **multi-modal**, discontinuous, non-differentiable spaces.
- Naturally **parallel**.
- Provides multiple alternative solutions.

**⚠️ Limitations**
- No guarantee of global optimum.
- Many hyper-parameters ($p_c, p_m, \text{pop. size}$).
- Slow convergence on simple problems.
- Premature convergence (loss of diversity).

---

# 5. Quick Revision Cheat-Sheet

## 📝 Soft Computing
- **Father:** Lotfi Zadeh.
- **4 pillars:** Fuzzy Logic, ANN, Evolutionary Computation, Probabilistic Reasoning.
- **Tolerant** of imprecision; **hard** computing is exact.

## 📝 Fuzzy Sets
- Membership $\mu \in [0,1]$.
- $\cup = \max,\;\cap = \min,\;\bar{} = 1-\mu$.
- $\alpha$-cut $= \{x : \mu(x) \ge \alpha\}$.
- **Excluded middle FAILS** in fuzzy logic.
- FIS: Fuzzify → Inference → Defuzzify (Mamdani / Sugeno).
- Centroid: $x^* = \dfrac{\sum x\mu(x)}{\sum \mu(x)}$.

## 📝 Neural Networks
- Biological: dendrite-soma-axon-synapse.
- Artificial: $\text{net}=\sum w_i x_i - \theta$, $y=f(\text{net})$.
- **Activation:** step, sigmoid, tanh, ReLU.
- **Learning:** Hebbian, Perceptron, Delta.
- **Perceptron convergence** — linearly separable data only.
- **Universal approximation** — one hidden layer suffices.
- **XOR** ⇒ need ≥ 1 hidden layer.

## 📝 Genetic Algorithm
- Father: John Holland (1975).
- Cycle: **Init → Eval → Select → Crossover → Mutate → Repeat**.
- Operators: roulette/tournament selection, 1-pt/uniform crossover, bit-flip mutation.
- $p_c \approx 0.7,\;p_m \approx 0.01$.
- **Schema theorem:** short, low-order, above-average schemata survive exponentially.

---

> **End of Unit 1 — Introduction (Soft Computing).**
> *Next: Unit 2 will cover Fuzzy Set Theory & Fuzzy Logic in depth (share when ready).*
