---
title: "Information Theory: Leverage Map"
date: 2025-12-28
draft: true
tags: ["mathematics", "information-theory", "leverage-map"]
---

# Information Theory: Leverage Map

### A. EXISTENCE JUSTIFICATION

Communication kept failing in predictable ways.

**The problem (1940s):** Engineers at Bell Labs needed to send messages through noisy channels—telephone wires, radio waves. Sometimes bits got flipped. How much redundancy do you need to correct errors? Is there a fundamental limit to reliable communication?

**Shannon's revolution (1948):** Claude Shannon proved that every channel has a *capacity* C—a maximum rate at which information can be transmitted reliably. Below capacity, you can communicate with arbitrarily small error. Above capacity, errors are unavoidable. The capacity is computable from the channel's statistics.

**The deeper insight:** Information is *physical*. It can be measured, quantified, transmitted, stored, compressed, encrypted. Shannon gave information a unit (the bit) and a calculus (entropy, mutual information, channel capacity).

**Why this was shocking:**

Before Shannon, engineers thought:
- More noise → need more redundancy → lower rate
- Approaching zero error requires infinite redundancy

Shannon showed:
- There's a sharp threshold (capacity)
- Below it, you can achieve *arbitrarily small* error with *finite* redundancy
- The capacity depends only on signal-to-noise ratio

**The core move:** Separate the *source* (what you want to say) from the *channel* (how you transmit it). Compress the source to remove redundancy. Add redundancy back strategically for error correction. These are independent problems with independent solutions.

**Why this matters:**
- **Communication:** Every modern communication system (internet, cell phones, WiFi, satellites) is designed using Shannon's theory
- **Compression:** ZIP, MP3, JPEG, video codecs—all information theory
- **Cryptography:** Perfect secrecy, key rates, secure communication
- **Statistics:** Minimum description length, model selection
- **Physics:** Thermodynamic entropy, black hole information, Landauer's principle
- **Neuroscience:** Neural coding, efficient representation, metabolic costs
- **Machine learning:** Variational inference, rate-distortion, information bottleneck

---

### B. CORE OBJECTS & MORPHISMS

**The fundamental quantities:**

| Object | What it is | Formula |
|--------|-----------|---------|
| **Entropy** | Uncertainty / information content of a random variable | H(X) = -Σ p(x) log p(x) |
| **Joint entropy** | Uncertainty of two variables together | H(X,Y) = -Σ p(x,y) log p(x,y) |
| **Conditional entropy** | Remaining uncertainty given knowledge of another | H(X\|Y) = H(X,Y) - H(Y) |
| **Mutual information** | Information shared between two variables | I(X;Y) = H(X) + H(Y) - H(X,Y) |
| **Relative entropy / KL divergence** | "Distance" from Q to P | D(P‖Q) = Σ p(x) log(p(x)/q(x)) |
| **Cross entropy** | Expected surprise using wrong distribution | H(P,Q) = -Σ p(x) log q(x) = H(P) + D(P‖Q) |
| **Differential entropy** | Continuous version of entropy | h(X) = -∫ p(x) log p(x) dx |

**Key relationships (the Venn diagram):**

```
    H(X)                    H(Y)
   ┌─────────────────────────────┐
   │         ┌───────┐           │
   │         │ I(X;Y)│           │
   │ H(X|Y)  │       │  H(Y|X)   │
   │         └───────┘           │
   └─────────────────────────────┘
            H(X,Y)
```

- H(X,Y) = H(X) + H(Y|X) = H(Y) + H(X|Y)
- I(X;Y) = H(X) - H(X|Y) = H(Y) - H(Y|X)
- I(X;Y) = H(X) + H(Y) - H(X,Y)
- I(X;Y) = D(P_{XY} ‖ P_X ⊗ P_Y)

**The fundamental problems:**

| Problem | Question | Answer |
|---------|----------|--------|
| **Source coding** | How much can you compress? | H(X) bits per symbol |
| **Channel coding** | How fast can you communicate reliably? | C = max_{P_X} I(X;Y) bits per use |
| **Rate-distortion** | How much compression at given fidelity? | R(D) = min_{P_{X̂\|X}: 𝔼[d(X,X̂)]≤D} I(X;X̂) |
| **Cryptography** | How much key for perfect secrecy? | H(Message) bits |

**Morphisms:**

Channels are the morphisms. A channel P_{Y|X} transforms input X to output Y. Composition: cascade channels. The "good" channels are those with high capacity.

---

### C. CENTRAL INVARIANTS

**Entropy as the fundamental measure:**

| Property | Statement |
|----------|-----------|
| **Non-negativity** | H(X) ≥ 0 (= 0 iff X is deterministic) |
| **Maximum** | H(X) ≤ log|𝒳| (achieved by uniform distribution) |
| **Additivity** | H(X,Y) = H(X) + H(Y) if X ⊥ Y |
| **Chain rule** | H(X₁,...,Xₙ) = Σᵢ H(Xᵢ|X₁,...,Xᵢ₋₁) |
| **Conditioning reduces entropy** | H(X|Y) ≤ H(X) (equality iff X ⊥ Y) |

**Mutual information properties:**

| Property | Statement |
|----------|-----------|
| **Non-negativity** | I(X;Y) ≥ 0 (= 0 iff X ⊥ Y) |
| **Symmetry** | I(X;Y) = I(Y;X) |
| **Chain rule** | I(X;Y,Z) = I(X;Y) + I(X;Z|Y) |
| **Data processing inequality** | If X → Y → Z (Markov chain), then I(X;Z) ≤ I(X;Y) |

**The data processing inequality is fundamental:** You can't create information by processing. Any operation on Y can only lose information about X, never gain it.

**KL divergence properties:**

| Property | Statement |
|----------|-----------|
| **Non-negativity** | D(P‖Q) ≥ 0 (Gibbs' inequality) |
| **Zero iff equal** | D(P‖Q) = 0 ⟺ P = Q |
| **Not symmetric** | D(P‖Q) ≠ D(Q‖P) in general |
| **Convexity** | D(P‖Q) is convex in the pair (P,Q) |

**What counts as "the same":**

- Distributions with same entropy have same "information content"
- Channels with same capacity have same "communication power"
- But: different distributions/channels can have same entropy/capacity while being very different in structure

---

### D. SIGNATURE THEOREMS

**1. Shannon's Source Coding Theorem (Noiseless Coding)**
> *A source with entropy H can be compressed to H bits per symbol on average, but not fewer.*

**Precise statement:** For n i.i.d. samples from X, there exist codes achieving rate R > H(X) with vanishing error probability, and no code can achieve rate R < H(X) with vanishing error.

**Why it matters:** Entropy IS the compressibility. H(X) bits is both achievable and necessary. This defines entropy operationally—it's not just a formula, it's what compression achieves.

**Typical sequences:** The key insight is *typicality*. Among 2^{nH} possible sequences, almost all probability mass concentrates on ~2^{nH(X)} "typical" sequences. Encode only these.

**2. Shannon's Channel Coding Theorem (Noisy Coding)**
> *A channel with capacity C can reliably transmit at any rate R < C, but not at R > C.*

**Precise statement:** For any R < C and any ε > 0, there exist codes of rate R with error probability < ε. Conversely, for R > C, error probability is bounded away from 0.

**Why it matters:** This is the most important theorem in information theory. It says:
- There's a sharp threshold (capacity)
- Reliable communication is possible right up to that threshold
- The threshold is computable

**The converse is crucial:** It's not just that we don't know how to exceed capacity—it's *impossible*. This is proven via Fano's inequality.

**3. Rate-Distortion Theorem**
> *To represent source X with average distortion ≤ D, you need at least R(D) bits per symbol, where R(D) = min I(X;X̂) over distributions achieving distortion D.*

**Why it matters:** Source coding with a fidelity criterion. You can't compress below H(X) losslessly, but you can compress further if you accept distortion. R(D) is the rate-distortion function—it tells you exactly how bits trade off against fidelity.

**4. Data Processing Inequality**
> *If X → Y → Z forms a Markov chain, then I(X;Z) ≤ I(X;Y).*

**Why it matters:** Processing can only destroy information, never create it. This is why:
- Sufficient statistics capture all relevant information
- Cascaded channels can only lose capacity
- You can't recover information that's been lost

**Equality condition:** I(X;Z) = I(X;Y) iff X → Z → Y also holds (Z is sufficient for Y about X).

**5. Entropy Power Inequality**
> *For independent continuous random variables X, Y:*
> $$e^{2h(X+Y)} \geq e^{2h(X)} + e^{2h(Y)}$$

**Why it matters:** This is the information-theoretic analog of the Brunn-Minkowski inequality in geometry. It implies:
- Gaussian has maximum entropy for given variance
- Central limit theorem has information-theoretic proof
- Bounds on capacity of Gaussian channels

**6. Asymptotic Equipartition Property (AEP)**
> *For i.i.d. X₁,...,Xₙ:*
> $$-\frac{1}{n} \log P(X_1,...,X_n) \to H(X) \text{ in probability}$$

**Why it matters:** The probability of a typical sequence is approximately 2^{-nH}. There are approximately 2^{nH} typical sequences. This is *why* compression to H bits works—typical sequences are all roughly equally likely, and there are just the right number of them.

---

### E. BRIDGES TO OTHER DOMAINS

| Domain | Connection |
|--------|------------|
| **Probability / Statistics** | Entropy is expected log-likelihood. KL divergence is log-likelihood ratio. Mutual information measures dependence. Maximum entropy = principle for inference. |
| **Measure Theory** | Entropy is an integral. Differential entropy needs measure theory. Radon-Nikodym for KL divergence. |
| **Coding Theory** | Source coding, channel coding, error correction. Algebraic codes, LDPC codes, polar codes. |
| **Cryptography** | Perfect secrecy requires key entropy ≥ message entropy. Information-theoretic security vs computational security. |
| **Thermodynamics** | Boltzmann entropy S = k_B ln W. Gibbs entropy S = -k_B Σ p ln p. Landauer's principle: erasing 1 bit costs k_B T ln 2 energy. |
| **Statistical Mechanics** | Maximum entropy distributions are Boltzmann. Free energy = energy - temperature × entropy. Partition function. |
| **Machine Learning** | Cross-entropy loss. KL divergence in VAEs. Information bottleneck. Mutual information neural estimation. |
| **Neuroscience** | Efficient coding hypothesis. Neural information transmission. Rate coding vs temporal coding. |
| **Quantum Information** | Von Neumann entropy S(ρ) = -Tr(ρ log ρ). Quantum channels. Entanglement entropy. Holevo bound. |
| **Information Geometry** | Fisher information as metric. KL divergence induces geometry. Statistical manifolds. |
| **Algorithmic Information** | Kolmogorov complexity K(x). Minimum description length. Algorithmic randomness. |
| **Linguistics** | Zipf's law. Entropy rate of language. Compression as language model evaluation. |

**Pattern-linking gold:**

**Entropy is universal:**

The formula H = -Σ p log p appears everywhere:
- Information theory: uncertainty
- Thermodynamics: disorder
- Statistical mechanics: Gibbs entropy
- Ecology: species diversity (Shannon index)
- Economics: market concentration (Theil index)

Why? Because it's the *unique* measure satisfying natural axioms (continuity, maximality for uniform, additivity for independent). Entropy isn't chosen—it's forced.

**The duality: compression ↔ prediction**

Good compression requires good prediction. If you can predict the next symbol well, you don't need many bits to encode it. This is why:
- Language models are evaluated by perplexity (= 2^H)
- Compression benchmarks test intelligence (Hutter Prize)
- MDL principle: best hypothesis = best compression

**The geometry of distributions:**

KL divergence induces geometry on probability space (information geometry). Mutual information is KL divergence from product to joint. The Fisher information is the metric tensor. All the information-theoretic quantities have geometric interpretations.

---

### F. COMMON MISCONCEPTIONS

1. **"Entropy measures disorder/randomness"** — Entropy measures *uncertainty given your model*. A deterministic chaotic system has zero entropy (deterministic), but might look random. Entropy depends on the distribution you assign, not the "true" randomness.

2. **"More entropy = less information"** — Confusing senses of "information." High entropy means high *potential* information (many bits needed to specify the outcome). Low entropy means high *prior* information (you already know roughly what will happen).

3. **"KL divergence is a distance"** — It's not symmetric and doesn't satisfy the triangle inequality. It's a *divergence*, measuring the penalty for using Q when P is true. The asymmetry is meaningful: D(P‖Q) ≠ D(Q‖P).

4. **"Mutual information measures correlation"** — It measures *all* statistical dependence, including nonlinear. Zero correlation doesn't imply zero mutual information. I(X;Y) = 0 iff X and Y are independent.

5. **"Capacity is a property of the physical channel"** — Capacity depends on what you're allowed to put in. The same physical wire has different capacity depending on power constraints, bandwidth, etc. Capacity = max over input distributions.

6. **"Compression to entropy is easy"** — Achieving the entropy limit requires codes that grow with block length, and optimal codes (arithmetic coding, ANS) are non-trivial. Simple codes like Huffman approach but don't always achieve the limit.

7. **"Differential entropy is just continuous entropy"** — Differential entropy can be negative! It's not the limit of discrete entropy. It's coordinate-dependent. The "right" continuous quantity is often KL divergence relative to a reference measure.

8. **"Shannon entropy captures all notions of information"** — There are other measures: Rényi entropies, min-entropy (for cryptography), Kolmogorov complexity (algorithmic), Fisher information (for estimation). Shannon entropy is central but not unique.

---

### G. NOTATION SURVIVAL KIT

| Symbol | Meaning |
|--------|---------|
| H(X) | Entropy of X |
| H(X,Y) | Joint entropy |
| H(X\|Y) | Conditional entropy |
| I(X;Y) | Mutual information |
| I(X;Y\|Z) | Conditional mutual information |
| D(P‖Q) or D_{KL}(P‖Q) | KL divergence from Q to P |
| h(X) | Differential entropy (continuous) |
| C | Channel capacity |
| R | Rate (bits per symbol or per channel use) |
| R(D) | Rate-distortion function |
| P_X or p(x) | Distribution of X |
| P_{Y\|X} or p(y\|x) | Conditional distribution / channel |
| 𝒳 | Alphabet (set of possible values) |
| log | Usually log base 2 (bits); sometimes natural log (nats) |
| X^n | n i.i.d. copies: (X₁,...,Xₙ) |
| T_ε^{(n)} | Typical set (sequences within ε of entropy rate) |
| P_e | Probability of error |

**Key formulas:**

| Quantity | Formula |
|----------|---------|
| Entropy | H(X) = -Σ_x p(x) log p(x) = 𝔼[-log p(X)] |
| Mutual information | I(X;Y) = Σ_{x,y} p(x,y) log(p(x,y)/(p(x)p(y))) |
| KL divergence | D(P‖Q) = Σ_x p(x) log(p(x)/q(x)) |
| Capacity (DMC) | C = max_{P_X} I(X;Y) |
| Binary entropy | H_b(p) = -p log p - (1-p) log(1-p) |
| Gaussian entropy | h(X) = ½ log(2πeσ²) for X ~ N(μ,σ²) |
| AWGN capacity | C = ½ log(1 + SNR) bits per channel use |

**Common channels:**

| Channel | Description | Capacity |
|---------|-------------|----------|
| **Binary symmetric** | Flips each bit with prob p | C = 1 - H_b(p) |
| **Binary erasure** | Erases each bit with prob ε | C = 1 - ε |
| **AWGN** | Y = X + N, N ~ N(0,σ²) | C = ½ log(1 + P/σ²) |
| **Z-channel** | 0→0, 1→0 with prob p | Asymmetric; C < 1-H_b(p) |

---

### H. ONE WORKED MICRO-EXAMPLE

**Computing entropy: the biased coin**

**Setup:** X ~ Bernoulli(p), taking values {0, 1} with P(X=1) = p.

**Entropy:**

$$H(X) = -p \log_2 p - (1-p) \log_2(1-p) = H_b(p)$$

This is the *binary entropy function*.

**Key values:**

| p | H_b(p) |
|---|--------|
| 0 | 0 (certain: always 0) |
| 0.5 | 1 (maximum uncertainty) |
| 1 | 0 (certain: always 1) |
| 0.1 | 0.469 bits |
| 0.01 | 0.081 bits |

**The shape:** H_b(p) is concave, symmetric around p = 0.5, maximum at p = 0.5.

```
H_b(p)
  1 |      ___
    |    /     \
    |   /       \
    |  /         \
  0 |_/___________\___
    0    0.5      1    p
```

**Operational meaning:** 

To encode n i.i.d. biased coin flips:
- Naive: n bits (one per flip)
- Optimal: nH_b(p) bits

For p = 0.1: only need 0.469n bits instead of n. You can compress by more than half!

**Why:** Most sequences have about 0.1n ones. There are only C(n, 0.1n) ≈ 2^{nH_b(0.1)} such sequences. Encode only those.

---

**Micro-example 2: Binary symmetric channel capacity**

**Setup:** Input X ∈ {0,1}, output Y ∈ {0,1}. Each bit flips independently with probability p (crossover probability).

$$P(Y=0|X=0) = P(Y=1|X=1) = 1-p$$
$$P(Y=1|X=0) = P(Y=0|X=1) = p$$

**Computing capacity:**

$$C = \max_{P_X} I(X;Y)$$

By symmetry, optimal input is uniform: P(X=0) = P(X=1) = ½.

Then Y is also uniform: P(Y=0) = P(Y=1) = ½.

$$H(Y) = 1 \text{ bit}$$

$$H(Y|X) = H_b(p)$$

(Given X, Y is a biased coin flip with parameter p.)

$$I(X;Y) = H(Y) - H(Y|X) = 1 - H_b(p)$$

**Therefore:**

$$C_{BSC} = 1 - H_b(p)$$

**Key values:**

| p | C |
|---|---|
| 0 | 1 bit (perfect channel) |
| 0.1 | 0.531 bits |
| 0.5 | 0 bits (pure noise, output independent of input) |

**Interpretation:** The noise "uses up" H_b(p) bits of capacity. What remains, 1 - H_b(p), is what you can reliably communicate.

**Shannon's promise:** For any rate R < 1 - H_b(p), there exist codes with error probability → 0 as block length → ∞.

---

**Micro-example 3: Data processing inequality in action**

**Setup:** Markov chain X → Y → Z.

**Claim:** I(X;Z) ≤ I(X;Y).

**Proof:**

$$I(X;Y,Z) = I(X;Y) + I(X;Z|Y)$$

by chain rule for mutual information.

But also:

$$I(X;Y,Z) = I(X;Z) + I(X;Y|Z)$$

So:

$$I(X;Y) + I(X;Z|Y) = I(X;Z) + I(X;Y|Z)$$

Since X → Y → Z, we have X ⊥ Z | Y (X and Z are conditionally independent given Y).

Therefore I(X;Z|Y) = 0.

$$I(X;Y) = I(X;Z) + I(X;Y|Z) \geq I(X;Z)$$

since I(X;Y|Z) ≥ 0. ∎

**Example:** 

X = original image
Y = compressed version
Z = re-compressed version

I(X;Z) ≤ I(X;Y): The twice-compressed version has less information about the original than the once-compressed version. You can't recover lost information.

**Why this matters:**

This is why:
- Lossy compression is irreversible
- Sufficient statistics capture all information (equality case)
- Neural network layers can only lose information about the input
- Every stage of processing is an information bottleneck

---

### Information and Physics

**Thermodynamic connection:**

Shannon entropy and Boltzmann-Gibbs entropy are the same formula:

$$S_{Boltzmann} = -k_B \sum_i p_i \ln p_i$$

Just different units (k_B converts nats to energy/temperature).

**Landauer's principle:** Erasing 1 bit of information requires at least k_B T ln 2 of energy dissipation. Information is physical—you can't erase it for free.

**Maxwell's demon:** A demon who knows molecule positions could violate the second law by sorting fast/slow molecules. Resolution: The demon must *store* information, and erasing that memory costs entropy.

**Black hole entropy:** Bekenstein-Hawking entropy S = A/(4ℓ_P²) counts information hidden behind the horizon. The holographic principle: information content of a region scales with surface area, not volume.

**Quantum information:**

Von Neumann entropy: S(ρ) = -Tr(ρ log ρ) for density matrix ρ.

Entanglement entropy: S(ρ_A) where ρ_A is the reduced state of subsystem A.

Key difference: Quantum information can be entangled. Two bits can carry more than 2 bits of correlation (Bell inequality violations). But you can't transmit classical information faster than light (no-signaling).

---

### Leverage for your work:

**The information bottleneck:**

For a Markov chain X → Y → Z, the bottleneck principle says: Z should retain information about X that's relevant for some task T, while discarding irrelevant information.

$$\mathcal{L} = I(X;Z) - \beta I(Z;T)$$

This is a variational principle for representation learning. Your Convergence Thesis might say: optimal cognitive representations are those that solve the information bottleneck for the organism's task distribution.

**Efficient coding hypothesis:**

Barlow (1961): Neural codes should maximize information transmission given metabolic constraints. This predicts:
- Sparse coding in visual cortex
- Center-surround receptive fields (decorrelation)
- Adaptation to stimulus statistics

If brains optimize information transmission, information theory tells you what the code should look like. The "constraints force the structure" theme applies.

**Compression and prediction:**

Good compression requires good prediction (entropy = average surprise). Language models are evaluated by cross-entropy (compression). If cognition does prediction (predictive coding theory), then cognition does compression.

The minimum description length (MDL) principle: the best hypothesis is the one that most compresses the data. Learning = compression.

**Mutual information and neural networks:**

The information plane: track I(X;T) vs I(T;Y) where T is a hidden layer representation, X is input, Y is label. Training dynamics trace a path in this plane.

Deep networks might work by progressive refinement: early layers maximize I(X;T), later layers maximize I(T;Y) while compressing I(X;T). This is speculative but suggests information-theoretic constraints on architectures.

**Channel capacity as cognitive limit:**

If neural pathways are channels, they have capacity. The capacity limits how much information can flow. Attention might be capacity allocation—routing limited capacity to task-relevant channels.

**Rate-distortion for representations:**

You can't represent everything perfectly (R(0) = H). Optimal lossy representation trades off rate (how many bits) against distortion (how much error). Different tasks have different distortion measures, so optimal representations depend on task.

This connects to your pattern: constraints (task, distortion measure, rate budget) force structure (optimal representation).

**Zipf's law and optimal coding:**

Zipf's law (word frequency ∝ 1/rank) is close to optimal for communication efficiency. If the goal is to minimize communication cost, Zipf-like distributions emerge. Language structure might be shaped by information-theoretic pressure.

**The zeta connection (via physics):**

In statistical mechanics, the partition function Z = Σ e^{-βE} generates all thermodynamic quantities. Free energy F = -T log Z. Entropy S = -∂F/∂T.

The partition function is like a zeta function: a sum over states weighted by energy. Your "spectral echoes" intuition connects: the spectrum of the Hamiltonian determines the partition function, which determines the entropy, which determines the information-theoretic properties.

---

**Now we have 16 domains:**

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
