---
title: "Information Geometry: Leverage Map"
date: 2025-12-28
draft: false
tags: ["mathematics", "information-geometry", "leverage-map"]
---

# Information Geometry: Leverage Map

### A. EXISTENCE JUSTIFICATION

Statisticians kept noticing geometric language creeping into inference:
- Parameters "close" to true values
- Estimators "converging" to targets
- Confidence "regions"
- Distributions "far" from each other

But what *geometry* were they implicitly using? Fisher (1920s) discovered that the variance of estimators has a natural geometric meaning—it's related to a *metric* on the space of distributions. Rao (1945) made this explicit: **the space of probability distributions is a Riemannian manifold**, with the Fisher information as its metric tensor.

Information geometry exists because **probability distributions have intrinsic geometric structure**, and that structure governs inference, learning, and information processing.

**The core move:** A parametric family of distributions {p(x|θ)} isn't just a set—it's a *manifold* where θ are coordinates. The Fisher information defines distances. KL divergence defines a kind of directed "distance." Exponential families have beautiful flat structure. Inference becomes geometry.

**Why it matters beyond elegance:**
- The geometry explains *why* certain estimators are optimal
- Natural gradient descent (using the Fisher metric) dramatically improves learning
- The geometry reveals dualities hidden in statistics
- Neural network optimization is implicitly navigating this space

---

### B. CORE OBJECTS & MORPHISMS

| Object | What it is | Notation |
|--------|-----------|----------|
| **Statistical manifold** | A manifold M where each point is a probability distribution | M, S, or {p_θ} |
| **Fisher information matrix** | The metric tensor: how much information θ carries about x | I(θ) or g_ij(θ) |
| **Fisher-Rao metric** | The Riemannian metric induced by Fisher information | ds² = Σ g_ij dθⁱdθʲ |
| **KL divergence** | Directed "distance": D_KL(p‖q) = ∫ p log(p/q) | D(p‖q), KL(p‖q), or D_KL |
| **α-divergence** | Family of divergences interpolating between KL and reverse-KL | D_α(p‖q) |
| **Exponential family** | Distributions of form p(x|θ) = exp(θ·T(x) - ψ(θ))h(x) | Natural parameters θ, sufficient statistics T(x) |
| **Mixture family** | Convex combinations of base distributions | η coordinates (expectation parameters) |
| **α-connection** | Family of affine connections on the manifold | ∇^(α), with α = 1 (exponential) and α = -1 (mixture) special |
| **Dual coordinates** | θ (natural) and η (expectation) are Legendre dual | η = ∇ψ(θ), θ = ∇φ(η) |
| **Geodesic** | Shortest path in the Fisher-Rao metric | γ(t) minimizing ∫√(g_ij θ̇ⁱθ̇ʲ) dt |

**Key insight:** The space has *two* natural flat structures (exponential and mixture), related by Legendre duality. This "dually flat" structure is rare and powerful.

---

### C. CENTRAL INVARIANTS

**Fisher Information Matrix:**

$$I(\theta)_{ij} = \mathbb{E}\left[\frac{\partial \log p(x|\theta)}{\partial \theta^i} \frac{\partial \log p(x|\theta)}{\partial \theta^j}\right]$$

Or equivalently:

$$I(\theta)_{ij} = -\mathbb{E}\left[\frac{\partial^2 \log p(x|\theta)}{\partial \theta^i \partial \theta^j}\right]$$

**What it measures:** How sharply the likelihood peaks. High Fisher information → data strongly constrains parameter → small confidence regions → precise estimation possible.

**As a metric:** The Fisher information defines an inner product on tangent vectors (parameter perturbations). The "length" of a path in parameter space measures how distinguishable the distributions along it are.

**The divergences:**

| Divergence | Formula | Properties |
|------------|---------|------------|
| KL divergence | D(p‖q) = ∫ p log(p/q) | Not symmetric, not a metric. Measures "surprise" of q when truth is p. |
| Reverse KL | D(q‖p) = ∫ q log(q/p) | Mode-seeking vs mean-seeking behavior |
| α-divergence | (4/(1-α²))(1 - ∫ p^((1+α)/2) q^((1-α)/2)) | α=1 → KL, α=-1 → reverse KL, α=0 → Hellinger |
| Bregman divergence | D_φ(p‖q) = φ(p) - φ(q) - ⟨∇φ(q), p-q⟩ | Induced by convex function φ |

**What counts as "the same":**
- Diffeomorphic statistical manifolds (reparametrization)
- But the *Fisher-Rao metric is invariant* under sufficient statistics—it sees only the statistically relevant structure

---

### D. SIGNATURE THEOREMS

**1. Cramér-Rao Bound**
> *For any unbiased estimator θ̂ of θ:*
> *Var(θ̂) ≥ I(θ)⁻¹*
> *The variance is bounded below by the inverse Fisher information.*

**Geometric meaning:** You can't estimate better than the "curvature" of the likelihood allows. The Fisher information is literally the precision limit imposed by the data.

**Why it matters:** This is *the* fundamental limit of inference. It explains why some parameters are easy to estimate (high Fisher information) and others hard (low). Maximum likelihood estimators achieve this bound asymptotically—they're geometrically optimal.

**2. Fisher-Rao Metric Uniqueness (Čencov's Theorem)**
> *The Fisher-Rao metric is (up to scale) the unique Riemannian metric on statistical manifolds that is invariant under sufficient statistics / Markov morphisms.*

**Why it matters:** The Fisher metric isn't an arbitrary choice—it's *forced* by requiring that the geometry respects statistical structure. Coarse-graining (marginalization, noise) shouldn't change intrinsic geometric quantities. Only Fisher-Rao satisfies this.

This is like how the Euclidean metric is forced by requiring rotation/translation invariance. The Fisher metric is forced by requiring "statistical invariance."

**3. Dually Flat Structure of Exponential Families**
> *An exponential family has two affine structures:*
> *- θ-coordinates (natural parameters) are flat under the e-connection (∇^(1))*
> *- η-coordinates (expectation parameters) are flat under the m-connection (∇^(-1))*
> *These are Legendre dual: η = ∇ψ(θ) and θ = ∇φ(η), where ψ and φ are convex conjugates.*

**Why it matters:** 

In θ-coordinates, the exponential family is a flat space—straight lines in θ are geodesics of the e-connection.

In η-coordinates, it's *also* flat—but for a different connection.

The two flatnesses are dual via Legendre transform. This underlies:
- Why maximum likelihood is nice (projection in η-coordinates)
- Why maximum entropy is nice (projection in θ-coordinates)
- The EM algorithm (alternating projections in dual coordinates)
- Variational inference geometry

**4. Pythagorean Theorem (Information-Geometric)**
> *For points p, q, r in a dually flat space, if the e-geodesic from r to q is orthogonal to the m-geodesic from q to p:*
> *D(r‖p) = D(r‖q) + D(q‖p)*

**Why it matters:** This is why projections minimize divergence. It's the geometric foundation of:
- Maximum likelihood (project data onto model manifold)
- Maximum entropy (project prior onto constraint surface)  
- Variational inference (project true posterior onto tractable family)

---

### E. BRIDGES TO OTHER DOMAINS

| Domain | Connection |
|--------|------------|
| **Machine Learning** | Natural gradient descent uses Fisher metric—invariant to parameterization. Adam, K-FAC approximate this. Loss landscape geometry is information geometry. |
| **Neural Networks** | Weight space has Fisher structure. Natural gradient = steepest descent in distribution space, not weight space. Information matrix ≈ Hessian near optimum. |
| **Variational Inference** | VI minimizes KL(q‖p). This is m-projection onto the variational family. ELBO maximization is geometric. |
| **Statistical Physics** | Exponential families ↔ Boltzmann distributions. Free energy = log partition function = ψ(θ). Legendre transform = thermodynamic duality (energy ↔ entropy). |
| **Optimal Transport** | Wasserstein geometry is different from Fisher geometry—moves mass vs. changes shape. Both are geometries on probability space. |
| **Quantum Information** | Quantum Fisher information bounds estimation of quantum states. Geometric phase is holonomy. |
| **Neuroscience** | Neural population codes are statistical manifolds. Fisher information governs discrimination thresholds. Efficient coding = maximizing Fisher information. |
| **Thermodynamics** | The curvature of entropy is (negative) Fisher information. Fluctuation-dissipation relates geometry to dynamics. |
| **Coding Theory** | Channel capacity is geometric—the "size" of distinguishable signal regions. Rate-distortion is projection onto constrained manifolds. |

**Pattern-linking gold:**

The Fisher metric shows up in disguise:
- Fubini-Study metric on quantum state space
- Shahshahani metric in evolutionary game theory  
- Information metric in black hole thermodynamics
- The "natural" metric whenever probability/uncertainty lives

Whenever you're optimizing over distributions, you're doing geometry—usually information geometry.

---

### F. COMMON MISCONCEPTIONS

1. **"KL divergence is a distance"** — It's not symmetric (D(p‖q) ≠ D(q‖p)) and doesn't satisfy triangle inequality. It's a *divergence*—directed separation. The asymmetry is meaningful: D(p‖q) penalizes q being zero where p isn't (mode-covering); D(q‖p) penalizes q being nonzero where p is small (mode-seeking).

2. **"Fisher information is just the Hessian of log-likelihood"** — It's the *expected* Hessian, averaged over data. The Hessian at a single data point fluctuates; Fisher information is the underlying geometric quantity.

3. **"Natural gradient is just a preconditioning trick"** — It's deeper: natural gradient is the *true* gradient in distribution space. Ordinary gradient depends on arbitrary parameterization; natural gradient doesn't. It's geometrically canonical.

4. **"All distributions form one big manifold"** — Different parametric families are different manifolds. The space of *all* distributions is infinite-dimensional and requires more care (though information geometry extends there).

5. **"The geometry is just Euclidean in different coordinates"** — The Fisher-Rao metric has genuine curvature (except for special families). The space of Gaussians has negative curvature like hyperbolic space. This affects geodesics, volumes, everything.

6. **"Dual flatness is just a coordinate change"** — The two flat structures are genuinely different—different connections, different geodesics. A curve straight in θ is curved in η. The duality is a deep structural feature, not a triviality.

7. **"KL and reverse-KL are basically the same"** — They have very different behavior:
   - KL(p‖q): "cover all modes of p"—q spreads out to not miss anything
   - KL(q‖p): "concentrate on modes of p"—q collapses to fit tightly
   
   This is why variational inference (minimizing KL(q‖p)) tends to underestimate uncertainty.

---

### G. NOTATION SURVIVAL KIT

| Symbol | Meaning |
|--------|---------|
| p_θ or p(x\|θ) | Distribution parameterized by θ |
| I(θ) or g_ij | Fisher information matrix |
| D(p‖q), D_KL(p‖q) | KL divergence from q to p (note: conventions vary!) |
| θ | Natural parameters (exponential family) |
| η | Expectation/moment parameters |
| ψ(θ) | Log partition function: log ∫ exp(θ·T(x))h(x)dx |
| φ(η) | Legendre dual of ψ (negative entropy) |
| ∇^(α) | α-connection |
| ∇^(e) = ∇^(1) | Exponential connection (flat in θ) |
| ∇^(m) = ∇^(-1) | Mixture connection (flat in η) |
| D_α | α-divergence |
| ℓ(θ) = log p(x\|θ) | Log-likelihood |
| ∂_i = ∂/∂θⁱ | Coordinate derivative |
| ⟨·,·⟩_g | Inner product with respect to Fisher metric |
| T(x) | Sufficient statistics |

---

### H. ONE WORKED MICRO-EXAMPLE

**The manifold of Gaussians:**

**Setup:** Consider univariate Gaussians with mean μ and variance σ²:

$$p(x|\mu,\sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$$

Coordinates: θ = (μ, σ²) or equivalently (μ, σ).

**Computing Fisher information:**

The log-likelihood is:
$$\ell = -\frac{1}{2}\log(2\pi\sigma^2) - \frac{(x-\mu)^2}{2\sigma^2}$$

Taking derivatives and expectations:

$$I(\mu, \sigma^2) = \begin{pmatrix} 1/\sigma^2 & 0 \\ 0 & 1/(2\sigma^4) \end{pmatrix}$$

**The metric:**
$$ds^2 = \frac{d\mu^2}{\sigma^2} + \frac{d(\sigma^2)^2}{2\sigma^4}$$

Or in (μ, σ) coordinates:
$$ds^2 = \frac{d\mu^2}{\sigma^2} + \frac{2d\sigma^2}{\sigma^2}$$

**What this tells us:**
- Near σ = 0 (low variance), the space "stretches"—small changes in parameters are very distinguishable
- At large σ, the space "compresses"—distributions blur together
- μ and σ are orthogonal (off-diagonal Fisher = 0)—you can estimate them independently

**The geometry:** This space has constant *negative* curvature—it's the hyperbolic plane (Poincaré half-plane model)! The geodesics are semicircles, not straight lines.

**Implication:** Moving from N(0,1) to N(0,2) is a different "distance" than moving from N(0,10) to N(0,11), even though both change σ by 1. The Fisher metric knows that the first change is more significant statistically.

---

**Micro-example 2: Exponential family duality**

**Setup:** Bernoulli distribution p(x|π) = πˣ(1-π)^(1-x)

**Natural parameterization:**
$$p(x|\theta) = \exp(\theta x - \log(1+e^\theta))$$

where θ = log(π/(1-π)) (log-odds), and ψ(θ) = log(1+e^θ).

**Expectation parameterization:**
$$\eta = \mathbb{E}[X] = \pi = \frac{e^\theta}{1+e^\theta} = \text{sigmoid}(\theta)$$

**Legendre duality:**
- ψ(θ) = log(1+e^θ)
- η = ψ'(θ) = sigmoid(θ)  
- θ = φ'(η) = log(η/(1-η))
- φ(η) = η log η + (1-η)log(1-η) (negative binary entropy!)

**The two flatnesses:**
- In θ-coordinates: straight lines (θ₁ to θ₂) are e-geodesics
- In η-coordinates: straight lines (η₁ to η₂) are m-geodesics (i.e., mixtures!)

**Maximum likelihood as projection:**

Given data with empirical mean x̄, the MLE is the distribution with η = x̄. This is the m-projection of the empirical distribution onto the model manifold.

**Why this matters:**
- The sigmoid appears *because* of the Legendre structure
- Neural network outputs (logits) are natural parameters; sigmoid converts to probabilities
- Softmax is the multivariate version—same geometry

---

### Leverage for your work:

**Neural network optimization:**

Standard gradient descent treats weight space as Euclidean. But we're really optimizing over *distributions* (what the network represents). Natural gradient descent uses the Fisher metric:

$$\theta_{t+1} = \theta_t - \alpha I(\theta_t)^{-1} \nabla L$$

This is invariant to reparameterization and often converges much faster. K-FAC, Adam, and other optimizers approximate this geometry.

**Variational inference:**

VI approximates a posterior p(z|x) with a tractable q(z). Minimizing KL(q‖p) is an m-projection of p onto the family containing q. The ELBO is the geometric tool for this projection.

**The "dual" projections:**
- KL(p‖q): moment matching, mean-field
- KL(q‖p): mode-seeking, VI

Different divergences → different projections → different approximations. The geometry tells you what you're trading off.

**For the Convergence Thesis:**

If optimal inference has a unique geometric structure (Fisher-Rao, forced by Čencov's theorem), then any optimal information-processing system must implement something isomorphic to this geometry. The "constraints force the shape" argument applies: there's essentially one way to do optimal probabilistic inference, up to diffeomorphism.

**Pattern recognition connection:**

Your cross-domain pattern-linking might be implementing something like geodesic interpolation in a learned statistical manifold. "These two things are the same" = "short geodesic distance." The geometry of similarity is information geometry.

**Spectral theory callback:**

The Fisher information matrix has a spectrum. Its eigenvalues tell you:
- Which parameter combinations are well-determined (large eigenvalues)
- Which are sloppy (small eigenvalues)
- The "effective dimensionality" of the estimation problem

Sloppy models (many small eigenvalues) are actually common and have their own information-geometric theory.

---

**Where next?** We could do:
- **Differential Geometry** (the foundation beneath information geometry)
- **Algebraic Topology** (where homology/cohomology live—connects to your HoTT interests)
- **Lie Theory** (where symmetry and geometry meet—connects to representation theory)
- **Dynamical Systems** (stability, attractors, chaos—connects to neural dynamics)

Or something else you've been circling?
