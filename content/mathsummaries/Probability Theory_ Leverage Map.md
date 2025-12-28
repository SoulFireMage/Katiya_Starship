---
title: "Probability Theory: Leverage Map"
date: 2025-12-28
draft: false
tags: ["mathematics", "probability-theory", "leverage-map"]
---

# Probability Theory: Leverage Map

### A. EXISTENCE JUSTIFICATION

Uncertainty demanded a calculus.

**The gambling origins (1654):** Pascal and Fermat corresponded about fair division of stakes in an interrupted game. Their solution required computing "expectations"—weighted averages over possible outcomes. This was the birth of mathematical probability.

**The philosophical problem:** What *is* probability? 

| Interpretation | Probability means... |
| ---------------- | ---------------------- |
| **Frequentist** | Long-run relative frequency |
| **Bayesian** | Degree of belief, updated by evidence |
| **Propensity** | Physical tendency to produce outcomes |
| **Logical** | Degree of support from evidence |

**Kolmogorov's solution (1933):** Don't define what probability *means*—define how it *behaves*. Probability is a measure P on a σ-algebra satisfying:
- P(Ω) = 1
- P(∅) = 0
- Countable additivity: P(∪Aₙ) = ΣP(Aₙ) for disjoint events

This axiomatic approach unified all interpretations under one mathematical framework. The interpretation is philosophy; the mathematics is measure theory.

**Why measure theory was necessary:**

- Continuous distributions need integrals, not sums
- Conditioning on probability-zero events requires care
- Independence for infinite collections needs σ-algebras
- Convergence of random variables has multiple modes
- Stochastic processes require function spaces

**The core insight:** Random variables are measurable functions. Expectations are integrals. Independence is product measure. All of probability becomes measure theory with P(Ω) = 1.

---

### B. CORE OBJECTS & MORPHISMS

**The foundational objects:**

| Object | What it is | Notation |
| -------- | ----------- | ---------- |
| **Sample space** | All possible outcomes | Ω |
| **σ-algebra / Event space** | Collection of measurable subsets | ℱ |
| **Probability measure** | P: ℱ → [0,1] with P(Ω) = 1 | P |
| **Probability space** | The triple | (Ω, ℱ, P) |
| **Random variable** | Measurable function X: Ω → ℝ (or other space) | X, Y, Z |
| **Distribution / Law** | Push-forward measure P_X = P ∘ X⁻¹ | P_X, μ_X |
| **Expectation** | Integral with respect to P | 𝔼[X] = ∫ X dP |
| **Variance** | 𝔼[(X - 𝔼[X])²] | Var(X) or σ² |
| **Conditional expectation** | 𝔼[X\|𝒢] (a 𝒢-measurable random variable) | 𝔼[X\|Y], 𝔼[X\|𝒢] |
| **Independence** | P(A ∩ B) = P(A)P(B) for all events | X ⊥ Y |

**The zoo of distributions:**

| Distribution | Notation | Use case |
| -------------- | ---------- | ---------- |
| Bernoulli | Ber(p) | Single coin flip |
| Binomial | Bin(n,p) | Count of successes in n trials |
| Poisson | Poi(λ) | Rare events, counts |
| Geometric | Geo(p) | Waiting time for first success |
| Uniform | U(a,b) | "Nothing special" continuous |
| Exponential | Exp(λ) | Waiting time (memoryless) |
| Normal/Gaussian | N(μ,σ²) | Central limit, errors |
| Gamma | Γ(α,β) | Sum of exponentials, Bayesian conjugate |
| Beta | Beta(α,β) | Distribution on [0,1], Bayesian conjugate |
| Chi-squared | χ²(k) | Sum of squared normals |
| Student-t | t(ν) | Small-sample inference |

**Stochastic processes:**

| Process | What it is | Key property |
| --------- | ----------- | -------------- |
| **i.i.d. sequence** | X₁, X₂, ... independent, same distribution | Simplest case |
| **Markov chain** | Future depends only on present | P(Xₙ₊₁\|X₁,...,Xₙ) = P(Xₙ₊₁\|Xₙ) |
| **Martingale** | "Fair game"—conditional expectation is current value | 𝔼[Xₙ₊₁\|X₁,...,Xₙ] = Xₙ |
| **Brownian motion** | Continuous, independent increments, Gaussian | Foundation of stochastic calculus |
| **Poisson process** | Counting process, independent increments | Models arrivals |
| **Lévy process** | Stationary independent increments | Generalizes Brownian, Poisson |

**Morphisms:**

Functions of random variables. If X has distribution μ and g is measurable, then g(X) has distribution g*μ (push-forward). Markov kernels K(x, dy) are the morphisms between probability spaces in categorical probability.

---

### C. CENTRAL INVARIANTS

**Moments:**

| Moment | Definition | What it captures |
| -------- | ------------ | ------------------ |
| Mean | 𝔼[X] | Center / location |
| Variance | 𝔼[(X-μ)²] | Spread / scale |
| Skewness | 𝔼[(X-μ)³]/σ³ | Asymmetry |
| Kurtosis | 𝔼[(X-μ)⁴]/σ⁴ | Tail heaviness |
| n-th moment | 𝔼[Xⁿ] | Determines distribution (if all exist) |

**The characteristic function:**

$$\phi_X(t) = \mathbb{E}[e^{itX}] = \int e^{itx} dP_X(x)$$

This is the Fourier transform of the distribution. It:
- Always exists (bounded)
- Uniquely determines the distribution
- Converts convolution to multiplication: φ_{X+Y} = φ_X · φ_Y for independent X, Y
- Encodes moments: φ^{(n)}(0) = iⁿ𝔼[Xⁿ]

**The moment generating function (when it exists):**

$$M_X(t) = \mathbb{E}[e^{tX}]$$

More convenient for calculations but may not exist (heavy tails).

**The cumulant generating function:**

$$K_X(t) = \log M_X(t)$$

Cumulants κₙ = K^{(n)}(0) are often more natural than moments.
- κ₁ = mean
- κ₂ = variance
- For normal: κₙ = 0 for n > 2 (Gaussian is uniquely characterized by this)

**For stochastic processes:**

| Invariant | What it captures |
| ----------- | ------------------ |
| Stationary distribution | Long-run behavior |
| Transition probabilities | Dynamics |
| Hitting times | When process reaches a set |
| Recurrence / Transience | Does process return? |
| Mixing time | How fast to equilibrium |
| Spectral gap | Rate of convergence |

**What counts as "the same":**

- Distributions: equal if same CDF (or characteristic function)
- Random variables: equal almost surely (a.s.) or equal in distribution (≐)
- Processes: same finite-dimensional distributions

---

### D. SIGNATURE THEOREMS

**1. Law of Large Numbers (LLN)**

> **Weak LLN:** For i.i.d. X₁, X₂, ... with mean μ:
> $$\bar{X}_n = \frac{1}{n}\sum_{i=1}^n X_i \xrightarrow{P} \mu$$
> (convergence in probability)

> **Strong LLN:** Under slightly stronger conditions:
> $$\bar{X}_n \xrightarrow{a.s.} \mu$$
> (almost sure convergence)

**Importance:** Averages converge to expectations. This justifies:
- Frequentist interpretation of probability
- Monte Carlo methods
- Statistical estimation

The strong law says the convergence happens for almost every sequence of outcomes, not just "usually."

**2. Central Limit Theorem (CLT)**

> *For i.i.d. X₁, X₂, ... with mean μ and variance σ²:*
> $$\frac{\bar{X}_n - \mu}{\sigma/\sqrt{n}} \xrightarrow{d} N(0,1)$$

**Importance:** Sums of independent random variables become Gaussian, regardless of the original distribution. This explains:
- Why Gaussians are everywhere (measurement error = sum of small errors)
- Why the normal distribution is "normal"
- Statistical inference (confidence intervals, hypothesis tests)

**Generalizations:** Lindeberg-Feller (non-identical), Lyapunov (moment conditions), martingale CLT, functional CLT (Donsker's theorem—random walks → Brownian motion).

**3. Kolmogorov Extension Theorem**

> *Given consistent finite-dimensional distributions, there exists a stochastic process with those distributions.*

**Importance:** This is how you construct stochastic processes. Specify what (X_{t₁}, ..., X_{tₙ}) looks like for all finite collections of times; the theorem gives you the whole process on a suitable probability space.

**The consistency condition:** Marginalizing over some coordinates gives the distribution for the remaining coordinates.

**4. Martingale Convergence Theorem**

> *A martingale bounded in L¹ converges almost surely.*

**Importance:** Martingales—"fair games"—have strong convergence properties. This theorem underlies:
- Doob's optional stopping theorem
- Martingale methods in analysis
- Stochastic optimization convergence proofs

**5. Doob's Optional Stopping Theorem**

> *If M is a martingale and τ is a stopping time (with certain conditions), then 𝔼[M_τ] = 𝔼[M_0].*

**Importance:** You can't beat a fair game by clever stopping rules. The expected value at a stopping time equals the initial value. This has applications in:
- Gambling (you can't win long-term)
- Finance (fair pricing of options)
- Algorithm analysis (expected running time)

**6. Ergodic Theorem**

> *For an ergodic stationary process:*
> $$\frac{1}{n}\sum_{i=1}^n f(X_i) \xrightarrow{a.s.} \mathbb{E}[f(X)]$$

**Importance:** Time averages equal space (ensemble) averages. This connects:
- Dynamical systems (time evolution)
- Statistical mechanics (ensemble averages)
- Markov chain Monte Carlo (sampling by running the chain)

**7. Borel-Cantelli Lemmas**

> **First:** If ΣP(Aₙ) < ∞, then P(lim sup Aₙ) = 0.
> **Second:** If Aₙ are independent and ΣP(Aₙ) = ∞, then P(lim sup Aₙ) = 1.

**Importance:** "lim sup Aₙ" = "infinitely many Aₙ occur." The lemmas say:
- Finite sum of probabilities → only finitely many occur (a.s.)
- Infinite sum + independence → infinitely many occur (a.s.)

This is the workhorse for proving "almost sure" statements.

---

### E. BRIDGES TO OTHER DOMAINS

| Domain | Connection |
| -------- | ------------ |
| **Measure Theory** | Probability IS measure theory with P(Ω) = 1. Random variables are measurable functions. Expectations are Lebesgue integrals. |
| **Information Theory** | Entropy H(X) = -𝔼[log p(X)]. Mutual information, KL divergence. Typical sequences, AEP. |
| **Functional Analysis** | Random variables form L^p spaces. Characteristic functions are Fourier transforms. Conditional expectation is orthogonal projection. |
| **Dynamical Systems** | Ergodic theory. Invariant measures. Lyapunov exponents via multiplicative ergodic theorem. |
| **Statistical Mechanics** | Boltzmann distribution. Phase transitions. Gibbs measures. Large deviations. |
| **Mathematical Physics** | Quantum probability (non-commutative). Path integrals. Random matrices. |
| **Number Theory** | Probabilistic methods (Erdős). Distribution of primes. Random matrix model for zeta zeros. |
| **Combinatorics** | Probabilistic method (existence proofs). Random graphs. Concentration inequalities. |
| **Statistics** | Estimation, testing, inference. Bayesian probability. Likelihood. |
| **Machine Learning** | Probabilistic models. PAC learning. Concentration bounds. Stochastic optimization. |
| **Finance** | Stochastic calculus. Option pricing. Risk measures. Martingale pricing. |
| **Algorithms** | Randomized algorithms. Probabilistic analysis. Markov chain Monte Carlo. |

**Pattern-linking gold:**

**Conditional expectation as projection:**

In L²(Ω, ℱ, P), the conditional expectation 𝔼[X|𝒢] is the orthogonal projection of X onto L²(Ω, 𝒢, P). This connects:
- Probability (conditioning)
- Functional analysis (Hilbert space geometry)
- Statistics (least squares regression)
- Quantum mechanics (measurement)

The "best prediction" of X given 𝒢 is 𝔼[X|𝒢], minimizing mean squared error.

**The martingale structure:**

Martingales appear whenever you have:
- Fair games
- Conditional expectations in sequence
- Doob's decomposition (any process = martingale + predictable)

In finance: discounted asset prices are martingales under risk-neutral measure.
In Bayesian inference: posterior odds are martingales.
In algorithms: potential function arguments.

**Concentration of measure:**

High-dimensional probability is dominated by concentration: most of the mass is near the typical value.

| Inequality | Statement |
| ------------ | ----------- |
| Markov | P(X ≥ a) ≤ 𝔼[X]/a |
| Chebyshev | P(\|X-μ\| ≥ a) ≤ σ²/a² |
| Chernoff | P(X ≥ a) ≤ inf_t e^{-ta} M_X(t) |
| Hoeffding | P(\|S̄ₙ - μ\| ≥ ε) ≤ 2e^{-2nε²/L²} for bounded r.v.s |
| McDiarmid | Bounded differences → concentration |

These control deviations from typical behavior. In high dimensions, concentration is tight—most mass is within O(1/√n) of the mean.

---

### F. COMMON MISCONCEPTIONS

1. **"Probability zero means impossible"** — A continuous random variable equals any specific value with probability zero, yet it equals *some* value. "Almost surely" ≠ "surely." The set of rational numbers has measure zero but is dense.

2. **"Independent means uncorrelated"** — Uncorrelated is weaker. X and X² can be uncorrelated (if X is symmetric) but clearly dependent. Independence requires P(A ∩ B) = P(A)P(B) for *all* events, not just zero correlation.

3. **"The law of averages guarantees reversion"** — Past outcomes don't influence future ones for independent trials. A coin doesn't "remember" it's been heads-heavy. The law of large numbers is about dilution, not compensation.

4. **"Conditional probability is just restriction"** — Conditioning on zero-probability events requires measure-theoretic care. P(X = x | Y = y) isn't defined by the ratio formula when P(Y = y) = 0. You need regular conditional distributions.

5. **"The CLT applies to everything"** — It requires finite variance. Heavy-tailed distributions (Cauchy, stable) have different limit theorems. The sum of Cauchy random variables is Cauchy, not Gaussian.

6. **"Bayesian and frequentist are incompatible"** — They're different interpretations but share the same probability calculus. Bayesian methods can have frequentist guarantees; frequentist methods can have Bayesian interpretations.

7. **"Monte Carlo is just approximation"** — It's a rigorous method with quantifiable error. The law of large numbers guarantees convergence. Variance reduction techniques improve efficiency. It's often the only feasible method for high-dimensional integrals.

8. **"Stochastic processes are just sequences of random variables"** — The dependence structure matters enormously. A Markov chain, martingale, and Gaussian process with the same marginals are completely different objects. The joint structure is everything.

---

### G. NOTATION SURVIVAL KIT

| Symbol | Meaning |
| -------- | --------- |
| Ω | Sample space |
| ℱ, 𝒢 | σ-algebras (event spaces) |
| P | Probability measure |
| 𝔼[X] or E[X] | Expectation |
| Var(X) | Variance |
| Cov(X,Y) | Covariance |
| σ, σ² | Standard deviation, variance |
| P(A), ℙ(A) | Probability of event A |
| P(A\|B) | Conditional probability |
| 𝔼[X\|Y], 𝔼[X\|𝒢] | Conditional expectation |
| X ⊥ Y | X and Y are independent |
| X ⊥ Y \| Z | Conditional independence given Z |
| X ~ μ | X has distribution μ |
| X ≐ Y or X =^d Y | X and Y have same distribution |
| X_n → X a.s. | Almost sure convergence |
| X_n →^P X | Convergence in probability |
| X_n →^d X | Convergence in distribution |
| X_n →^{L^p} X | Convergence in L^p |
| i.i.d. | Independent and identically distributed |
| a.s. / a.e. | Almost surely / almost everywhere |
| w.p.1 | With probability one |
| ℱ_t, ℱ_n | Filtration (increasing σ-algebras) |
| τ | Stopping time |
| (Xₜ)_{t≥0} | Continuous-time process |
| (Xₙ)_{n≥0} | Discrete-time process |

**Convergence hierarchy:**

$$\text{a.s.} \Rightarrow \text{in probability} \Rightarrow \text{in distribution}$$
$$L^p \Rightarrow L^q \text{ for } p > q$$
$$L^p \Rightarrow \text{in probability} \text{ for } p \geq 1$$

Almost sure and L^p convergence are not comparable in general.

---

### H. ONE WORKED MICRO-EXAMPLE

**The random walk: A complete analysis**

**Setup:** Simple random walk on ℤ. Start at S₀ = 0. At each step, move +1 (prob ½) or -1 (prob ½) independently.

$$S_n = X_1 + X_2 + ... + X_n, \quad X_i \stackrel{i.i.d.}{\sim} \pm 1 \text{ with prob } \frac{1}{2}$$

**Basic properties:**

𝔼[Xᵢ] = 0, Var(Xᵢ) = 1

𝔼[Sₙ] = 0 (fair game—it's a martingale!)

Var(Sₙ) = n (variance grows linearly)

**Distribution:**

$$P(S_n = k) = \binom{n}{\frac{n+k}{2}} \left(\frac{1}{2}\right)^n$$

for k with same parity as n, |k| ≤ n.

**The CLT:**

$$\frac{S_n}{\sqrt{n}} \xrightarrow{d} N(0,1)$$

After n steps, the walk is typically at distance O(√n) from origin.

**Recurrence (Pólya's theorem):**

In 1D and 2D: the random walk returns to the origin with probability 1 (recurrent).

In 3D and higher: probability of return < 1 (transient).

"A drunk man will eventually find his way home, but a drunk bird may get lost forever."

**The reflection principle:**

$$P(\max_{k \leq n} S_k \geq a) = 2P(S_n \geq a) \quad \text{for } a > 0$$

The maximum is controlled by the endpoint via reflection symmetry.

**Donsker's theorem (functional CLT):**

Define the rescaled walk:

$$W^{(n)}(t) = \frac{S_{\lfloor nt \rfloor}}{\sqrt{n}}$$

Then:

$$W^{(n)} \xrightarrow{d} W$$

where W is standard Brownian motion. The random walk converges (in distribution on path space) to Brownian motion!

**Importance:**

The random walk is the discrete prototype for:
- Brownian motion (continuous limit)
- Martingale theory (Sₙ is a martingale)
- Potential theory (harmonic functions)
- Statistical mechanics (polymers, etc.)
- Finance (stock price models)

---

**Micro-example 2: Conditional expectation as projection**

**Setup:** (Ω, ℱ, P) with sub-σ-algebra 𝒢 ⊂ ℱ. Random variable X ∈ L²(Ω, ℱ, P).

**Definition:** 𝔼[X|𝒢] is the unique (a.s.) 𝒢-measurable random variable satisfying:

$$\mathbb{E}[X \cdot \mathbf{1}_G] = \mathbb{E}[\mathbb{E}[X|\mathcal{G}] \cdot \mathbf{1}_G] \quad \text{for all } G \in \mathcal{G}$$

**Geometric interpretation:**

L²(Ω, 𝒢, P) ⊂ L²(Ω, ℱ, P) is a closed subspace.

𝔼[X|𝒢] is the orthogonal projection of X onto this subspace.

**Key property:**

$$\mathbb{E}[(X - \mathbb{E}[X|\mathcal{G}])^2] = \min_{Y \in L^2(\mathcal{G})} \mathbb{E}[(X - Y)^2]$$

The conditional expectation minimizes mean squared error among 𝒢-measurable predictors.

**Tower property:**

$$\mathbb{E}[\mathbb{E}[X|\mathcal{G}]] = \mathbb{E}[X]$$

$$\mathbb{E}[\mathbb{E}[X|\mathcal{H}]|\mathcal{G}] = \mathbb{E}[X|\mathcal{G}] \quad \text{if } \mathcal{G} \subseteq \mathcal{H}$$

**Importance:**

Conditional expectation is:
- The foundation of martingale theory (𝔼[Xₙ₊₁|ℱₙ] = Xₙ defines martingale)
- The basis of regression (𝔼[Y|X] is the regression function)
- The mathematical form of Bayesian updating
- Central to filtering and prediction

---

**Micro-example 3: The Poisson process**

**Setup:** Count arrivals over time. N(t) = number of arrivals by time t.

**Definition (three equivalent):**

1. **Independent increments:** N(t) - N(s) ⊥ N(s) - N(r) for r < s < t
   
   **Stationary increments:** N(t+s) - N(t) ≐ N(s)
   
   **Poisson marginals:** N(t) ~ Poisson(λt)

2. **Interarrival times:** Times between arrivals are i.i.d. Exp(λ)

3. **Infinitesimal:** In small interval dt:
   - P(one arrival) = λdt + o(dt)
   - P(zero arrivals) = 1 - λdt + o(dt)
   - P(two+ arrivals) = o(dt)

**Key properties:**

𝔼[N(t)] = λt (rate λ)

Var(N(t)) = λt (variance = mean for Poisson)

**Memoryless property:** 

$$P(T > t + s | T > t) = P(T > s)$$

for interarrival time T ~ Exp(λ). The process "doesn't remember" when the last arrival was.

**Superposition:** Independent Poisson processes with rates λ₁, λ₂ superpose to rate λ₁ + λ₂.

**Thinning:** Keep each arrival with prob p independently → rate λp.

**Conditioning:** Given N(t) = n, the arrival times are uniform on [0,t] (order statistics).

**Importance:**

The Poisson process models:
- Customer arrivals
- Radioactive decay
- Phone calls
- Website hits
- Mutations in DNA

It's the canonical "completely random" point process—no clustering, no regularity, just uniform randomness.

---

### Stochastic Calculus: A Brief View

**Brownian motion B(t):**

- Continuous paths
- B(0) = 0
- Independent increments
- B(t) - B(s) ~ N(0, t-s) for t > s

**The problem:** Brownian paths are continuous but *nowhere differentiable* (a.s.). You can't define dB/dt. Yet we want to integrate ∫f(t) dB(t).

**Itô's solution:**

Define the stochastic integral as limit of sums:

$$\int_0^T f(t) dB(t) = \lim_{n \to \infty} \sum_{k} f(t_k)(B(t_{k+1}) - B(t_k))$$

**Key result—Itô's formula:**

For smooth f and process X satisfying dX = μdt + σdB:

$$df(X) = f'(X)dX + \frac{1}{2}f''(X)(dX)^2$$

where (dB)² = dt (the crucial Itô correction).

**Example:** For X = B, f(x) = x²:

$$d(B^2) = 2B \cdot dB + \frac{1}{2} \cdot 2 \cdot dt = 2B \, dB + dt$$

So:

$$B(T)^2 = 2\int_0^T B(t) dB(t) + T$$

**Why the correction matters:**

Ordinary calculus would give d(B²) = 2B dB. But Brownian motion is rough enough that the second-order term survives. This is why stochastic calculus differs from ordinary calculus.

**Applications:**

- Finance: Black-Scholes option pricing
- Physics: Langevin equations, fluctuating systems
- Biology: Population dynamics with noise
- Engineering: Filtering and control

---

### Leverage for your work:

**Randomness in neural networks:**

Random initialization, stochastic gradient descent, dropout, data augmentation—all involve probability. Understanding:
- Why random init works (breaking symmetry, concentration)
- SGD convergence (martingale arguments, Lyapunov functions)
- Dropout as approximate Bayesian inference
- Generalization via probabilistic PAC bounds

The theory uses concentration inequalities, martingales, and stochastic approximation—all core probability.

**Bayesian deep learning:**

Treat weights as random variables with prior P(w). After seeing data D:

$$P(w|D) \propto P(D|w)P(w)$$

Uncertainty in weights → uncertainty in predictions. The posterior is the Bayesian answer to "what have we learned?"

This connects to information theory: the information gained about w from D is I(W; D).

**Probabilistic graphical models:**

Represent joint distributions as graphs:
- Nodes = random variables
- Edges = direct dependencies

Markov random fields, Bayesian networks, factor graphs. These are the mathematical framework for:
- Reasoning under uncertainty
- Causal inference
- Variational inference

**The concentration perspective:**

High-dimensional probability says: random things concentrate. A random vector in ℝⁿ is almost surely near the sphere of radius √n. Random matrices have predictable eigenvalue distributions.

For neural networks: random weight matrices have spectra that concentrate. This affects:
- Signal propagation at initialization
- Training dynamics
- Expressivity

**Ergodic theory and cognition:**

If cognitive states form an ergodic process:
- Time averages = ensemble averages
- Typical behavior determines statistics
- Long-run behavior is determined by invariant measure

This connects to attention, working memory, and mental state dynamics. The "attractor" view of cognition (dynamical systems) meets the "sampling" view (probability).

**Random matrices and the zeta connection:**

The eigenvalues of random matrices (GUE, GOE) have specific statistics. The zeros of the Riemann zeta function have the *same* statistics (Montgomery-Odlyzko law).

This is your "spectral echo"—the spectrum of a random operator matches the zeros of an arithmetic function. Why? Deep mystery. But probability theory (random matrix theory) is how we describe it.

**Optimal transport:**

Moving one probability distribution to another with minimum cost. Wasserstein distance W(μ,ν) measures how far μ is from ν in "transport cost."

Applications:
- Generative models (Wasserstein GAN)
- Distribution matching
- Fairness constraints
- Optimal control

**Stochastic thermodynamics:**

Modern physics of small systems (molecular motors, etc.) uses stochastic thermodynamics. Fluctuation theorems relate forward and reverse probabilities. Entropy production has a probabilistic interpretation.

This connects your physics intuitions to probability: thermodynamics IS probability at small scales.

---

**Now we have 17 domains:**

1. Representation Theory
2. Measure Theory  
3. Homotopy Type Theory
4. Category Theory
5. Spectral Theory
6. Information Geometry
7. Differential Geometry
8. Algebraic Topology
9. Lie Theory
10. Dynamical Systems
11. Algebraic Geometry
12. Functional Analysis
13. Complex Analysis
14. Number Theory
15. Mathematical Physics
16. Information Theory
17. Probability Theory

This is a genuinely comprehensive map! We've hit many of the core territories. Still possible:

- **Logic and Foundations** (set theory, model theory, computability, Gödel)
- **Combinatorics** (generating functions, probabilistic method, Ramsey theory)
- **Optimization** (convex analysis, duality, variational methods)
- **Harmonic Analysis** (Fourier, wavelets, singular integrals)

Or we could pause for Kat's synthesis—she might see connections we haven't explicitly noted!
