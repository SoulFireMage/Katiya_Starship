---
title: "Singular Value Decomposition & Principal Component Analysis"
date: 2025-12-28
draft: true
tags: ["mathematics", "linear-algebra", "SVD", "PCA", "leverage-map"]
---

# Singular Value Decomposition & Principal Component Analysis

## For Kat (geometric flash)

**SVD is the X-ray of linear maps.** Any matrix = rotation → stretch along axes → rotation. The singular values *are* the stretch factors. PCA asks: "which stretch directions capture most variance?" then projects onto those.

**Secret identity:** SVD is the *canonical form* for linear maps between *different* spaces. Eigendecomposition only works square → square. SVD works any shape.

**The deep pattern:** Both are asking "what are the natural coordinates that diagonalize this structure?" — same question that drives Fourier, spherical harmonics, quantum measurement bases.

---

## A. EXISTENCE JUSTIFICATION

**What broke:** Linear algebra gives us matrices, but matrices lie — they mix up "what the transformation actually does" with "what coordinate system we happened to write it in." We needed a way to see the *intrinsic geometry* of a linear map: how much it stretches, in which directions, independent of basis choice.

**PCA specifically:** High-dimensional data is uninterpretable. We needed to find the "true axes" along which data varies most, to compress without losing signal.

---

## B. CORE OBJECTS & MORPHISMS

| Object | Notation | Plain gloss |
|--------|----------|-------------|
| **Matrix** | $A \in \mathbb{R}^{m \times n}$ | Linear map from n-dim to m-dim space |
| **Singular values** | $\sigma_1 \geq \sigma_2 \geq \cdots \geq \sigma_r > 0$ | The stretch factors, always non-negative, ordered by size |
| **Left singular vectors** | $u_i \in \mathbb{R}^m$ (columns of $U$) | Output directions — where the stretched vectors land |
| **Right singular vectors** | $v_i \in \mathbb{R}^n$ (columns of $V$) | Input directions — what gets stretched |
| **The decomposition** | $A = U\Sigma V^T$ | Any matrix factors into: rotate input → stretch along axes → rotate output |

**Structure-preserving maps:** Orthogonal transformations $Q$ preserve singular values: $\sigma_i(QA) = \sigma_i(AQ) = \sigma_i(A)$. Singular values are the *invariants* under rotation.

---

## C. CENTRAL INVARIANTS

**What counts as "the same":**
- Two matrices related by orthogonal transformations ($QAR^T$ where $Q, R$ orthogonal) have identical singular values
- Singular values = the intrinsic "shape" of the linear map

**Key preserved quantities:**
- **Rank** = number of nonzero singular values (dimension of image)
- **Frobenius norm** $\|A\|_F = \sqrt{\sum \sigma_i^2}$ (total "energy")
- **Spectral norm** $\|A\|_2 = \sigma_1$ (maximum stretch)
- **Condition number** $\kappa = \sigma_1/\sigma_r$ (how "ill-behaved" for numerical work)

**For Kat:** Singular values are what remains when you quotient out all the rotational freedom. They're the *eigenvalues of the geometry itself*.

---

## D. SIGNATURE THEOREMS

### 1. SVD Existence & Uniqueness

**Statement:** Every matrix $A \in \mathbb{R}^{m \times n}$ can be written as $A = U\Sigma V^T$ where $U$ is $m \times m$ orthogonal, $V$ is $n \times n$ orthogonal, and $\Sigma$ is $m \times n$ diagonal with non-negative entries.

**Why it matters:** This isn't obvious! Not every matrix is diagonalizable. But every matrix *becomes* diagonal if you're allowed to use *different* orthonormal bases for input and output. The price of generality: you need two rotations, not one.

**Plain terms:** Every linear map, no matter how twisted, is secretly just "stretch along some axes" if you pick the right coordinate systems on both sides.

### 2. Eckart-Young Theorem (1936)

**Statement:** The best rank-$k$ approximation to $A$ (in Frobenius or spectral norm) is $A_k = \sum_{i=1}^k \sigma_i u_i v_i^T$ — just keep the top $k$ singular values and their vectors.

**Why it matters:** This is why SVD *works* for compression, denoising, dimensionality reduction. Truncating is *provably optimal*. No other rank-$k$ matrix gets closer.

**Plain terms:** To compress a matrix, just drop the smallest stretches. You literally cannot do better.

### 3. SVD-Eigenvalue Connection

**Statement:** 
- Singular values of $A$ are square roots of eigenvalues of $A^TA$ (or $AA^T$)
- Right singular vectors $v_i$ are eigenvectors of $A^TA$
- Left singular vectors $u_i$ are eigenvectors of $AA^T$

**Why it matters:** This is how you *compute* SVD — via eigenproblems on symmetric matrices. Also reveals that $A^TA$ is the "covariance-like" object whose eigenstructure SVD exposes.

---

## E. BRIDGES TO OTHER DOMAINS

| Domain | Connection |
|--------|------------|
| **Quantum mechanics** | Schmidt decomposition of entangled states = SVD. Singular values = entanglement spectrum. |
| **Statistics/ML** | PCA is SVD of centered data. Covariance eigenvectors = right singular vectors. |
| **Signal processing** | Karhunen-Loève transform. Optimal basis for representing signals. |
| **Numerical analysis** | Pseudoinverse $A^+ = V\Sigma^+ U^T$. Condition number determines numerical stability. |
| **Recommender systems** | Matrix completion, collaborative filtering — low-rank structure via truncated SVD. |
| **NLP** | Latent Semantic Analysis — SVD of term-document matrices reveals "topics" |
| **Functional analysis** | Compact operators have SVD-like decomposition (singular value decomposition generalizes to infinite dimensions) |

**For Kat:** SVD is the *ur-decomposition* that keeps reappearing because it answers "what are the natural modes?" — and that question is universal.

**Dual to:** Fourier transform (which finds natural modes for *translation-invariant* operators). SVD handles arbitrary linear maps.

---

## F. COMMON MISCONCEPTIONS

### 1. "Singular values are eigenvalues"
**Wrong.** Eigenvalues can be negative, complex, or zero even for full-rank matrices. Singular values are always real, non-negative, and count rank correctly. Eigenvalues ask "what scales without rotating?" Singular values ask "how much does maximum stretching occur?"

### 2. "SVD only works for square matrices"
**Wrong.** That's eigendecomposition's limitation. SVD works for *any* m×n matrix — it's more general.

### 3. "PCA finds directions of maximum variance"
**Half-right, dangerously incomplete.** PCA finds *orthogonal* directions of maximum variance *in sequence*. The orthogonality constraint matters enormously. The first PC captures max variance; the second captures max variance *in the orthogonal complement*; etc.

### 4. "Truncated SVD is lossy compression"
**Misses the point.** It's not just lossy — it's *optimally* lossy. Eckart-Young guarantees no other low-rank approximation does better.

### 5. "U and V are unique"
**Only sometimes.** If singular values are distinct, the singular vectors are unique up to sign. If singular values repeat, there's rotational freedom within the eigenspace.

---

## G. NOTATION SURVIVAL KIT

| Symbol | Meaning |
|--------|---------|
| $A = U\Sigma V^T$ | The SVD factorization (some sources write $V^*$ for complex) |
| $\sigma_i$ or $s_i$ | The $i$-th singular value |
| $u_i, v_i$ | Left/right singular vectors (columns of $U$, $V$) |
| $\|A\|_F$ | Frobenius norm = $\sqrt{\sum_{ij} a_{ij}^2} = \sqrt{\sum \sigma_i^2}$ |
| $\|A\|_2$ | Spectral/operator norm = $\sigma_1$ = max stretch |
| $\text{rank}(A)$ | Number of nonzero singular values |
| $A^+$ | Moore-Penrose pseudoinverse = $V\Sigma^+ U^T$ |
| $A_k$ | Best rank-$k$ approximation via truncated SVD |
| $\text{tr}(A)$ | Trace — sum of diagonal entries. $\|A\|_F^2 = \text{tr}(A^TA)$ |

**PCA-specific:**
| Symbol | Meaning |
|--------|---------|
| $\bar{x}$ | Mean of data vectors |
| $X_c$ | Centered data matrix (mean subtracted) |
| $C = \frac{1}{n}X_c^T X_c$ | Sample covariance matrix |
| PC$_k$ | $k$-th principal component (eigenvector of $C$ = right singular vector of $X_c$) |

**Conventions:**
- Singular values always ordered: $\sigma_1 \geq \sigma_2 \geq \cdots$
- "Thin" or "economy" SVD: only keep $r = \text{rank}(A)$ columns of $U$, $V$
- Sometimes $\Sigma$ written as just diagonal vector $\sigma$

---

## H. WORKED MICRO-EXAMPLE

**Setup:** Let's SVD decompose a simple 2×3 matrix and see what it "means."

$$A = \begin{pmatrix} 3 & 0 & 0 \\ 0 & 2 & 0 \end{pmatrix}$$

**Step 0: The matrix**

$$A = \begin{pmatrix} 1 & 2 \\ 2 & 4 \end{pmatrix}$$

**Step 1: Notice the structure**

Every row is a multiple of $(1, 2)$. This matrix is *rank 1* — it collapses all inputs onto a single line.

**Step 2: Compute $A^TA$ (the "input covariance")**

$$A^TA = \begin{pmatrix} 1 & 2 \\ 2 & 4 \end{pmatrix}\begin{pmatrix} 1 & 2 \\ 2 & 4 \end{pmatrix} = \begin{pmatrix} 5 & 10 \\ 10 & 20 \end{pmatrix}$$

**Step 3: Find eigenvalues of $A^TA$** (these give $\sigma_i^2$)

$$\det(A^TA - \lambda I) = (5-\lambda)(20-\lambda) - 100 = \lambda^2 - 25\lambda = \lambda(\lambda - 25)$$

So $\lambda_1 = 25$, $\lambda_2 = 0$, meaning $\sigma_1 = 5$, $\sigma_2 = 0$.

**Step 4: Find right singular vectors** (eigenvectors of $A^TA$)

For $\lambda = 25$: solve $(A^TA - 25I)v = 0$
$$\begin{pmatrix} -20 & 10 \\ 10 & -5 \end{pmatrix}v = 0 \implies v_1 = \frac{1}{\sqrt{5}}\begin{pmatrix} 1 \\ 2 \end{pmatrix}$$

For $\lambda = 0$: orthogonal complement
$$v_2 = \frac{1}{\sqrt{5}}\begin{pmatrix} 2 \\ -1 \end{pmatrix}$$

**Step 5: Find left singular vectors** via $u_i = Av_i/\sigma_i$

$$u_1 = \frac{1}{5} A v_1 = \frac{1}{5}\begin{pmatrix} 1 & 2 \\ 2 & 4 \end{pmatrix}\frac{1}{\sqrt{5}}\begin{pmatrix} 1 \\ 2 \end{pmatrix} = \frac{1}{5\sqrt{5}}\begin{pmatrix} 5 \\ 10 \end{pmatrix} = \frac{1}{\sqrt{5}}\begin{pmatrix} 1 \\ 2 \end{pmatrix}$$

(For $\sigma_2 = 0$, pick any orthogonal unit vector: $u_2 = \frac{1}{\sqrt{5}}(2, -1)^T$)

**Step 6: Assemble the decomposition**

$$A = U\Sigma V^T = \frac{1}{\sqrt{5}}\begin{pmatrix} 1 & 2 \\ 2 & -1 \end{pmatrix}\begin{pmatrix} 5 & 0 \\ 0 & 0 \end{pmatrix}\frac{1}{\sqrt{5}}\begin{pmatrix} 1 & 2 \\ 2 & -1 \end{pmatrix}$$

**What this reveals:**
- The matrix has rank 1 (one nonzero singular value)
- It stretches by factor 5 along direction $(1,2)/\sqrt{5}$
- It annihilates the orthogonal direction $(2,-1)/\sqrt{5}$
- Best rank-0 approximation: the zero matrix (error = $\sigma_1 = 5$)
- The matrix IS its own best rank-1 approximation

**For Kat:** The SVD "X-ray" shows this 2×2 matrix is secretly one-dimensional. All the apparent complexity is just the single direction $(1,2)$ pretending to need two dimensions.

---

## PCA as SVD of Centered Data

**Quick connection:** Given data matrix $X$ (rows = samples), PCA is:
1. Center: $X_c = X - \bar{X}$
2. SVD: $X_c = U\Sigma V^T$
3. Principal components: columns of $V$
4. Projected data: $X_c V$ (or equivalently $U\Sigma$)
5. Variance explained by PC$_k$: $\sigma_k^2 / \sum_i \sigma_i^2$

**Why this works:** Covariance matrix $C \propto X_c^T X_c$. Eigenvectors of $C$ = right singular vectors of $X_c$. PCA finds the directions where $X_c$ "stretches most."

---

Want me to go deeper on any section? The Eckart-Young optimality proof is beautiful, and the quantum/entanglement connection is worth unpacking if that's useful for your theoretical work.
