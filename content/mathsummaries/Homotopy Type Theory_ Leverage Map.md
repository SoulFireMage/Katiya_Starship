---
title: "Homotopy Type Theory: Leverage Map"
date: 2025-12-28
draft: true
tags: ["mathematics", "homotopy-type-theory", "leverage-map"]
---

# Homotopy Type Theory: Leverage Map

### A. EXISTENCE JUSTIFICATION

Two problems collided:

**From mathematics:** We kept saying "isomorphic objects are the same" but our foundations (set theory) didn't believe us. In ZFC, you can ask "is the number 2 an element of the number 3?" and get an answer (yes, in the standard construction)—but this question is *mathematically meaningless*. Our foundations had too much junk, distinguishing things that should be identical.

**From computer science:** Type theory provided a foundation for constructive mathematics and proof assistants, but lacked a good story for equality. When are two proofs "the same"? When are two constructions equivalent?

**The synthesis:** Homotopy type theory discovered that *types naturally behave like spaces* and *equality proofs naturally behave like paths*. This wasn't imposed—it was already there, waiting to be noticed. The result: a foundation where "equivalent things are equal" is literally true (univalence), and where equality itself has structure.

**The core move:** Instead of sets-with-elements, think spaces-with-paths. Instead of "equal or not" (boolean), think "paths between" (a space of ways to be equal). Proof becomes construction. Equality becomes homotopy.

---

### B. CORE OBJECTS & MORPHISMS

| Object | What it is | Notation |
|--------|-----------|----------|
| **Type** | Simultaneously: a proposition, a set, a space. The things that exist. | A, B, X, Y or 𝒰 (universe of types) |
| **Term / Inhabitant** | An element of a type. A point in the space. A proof of the proposition. | a : A means "a is of type A" |
| **Identity type** | The type of paths/equalities between two terms | Id_A(a,b) or a =_A b or Path_A(a,b) |
| **Path** | A term of an identity type—a *witness* that two things are equal | p : a = b |
| **Function type** | Functions from A to B | A → B |
| **Dependent type** | A family of types varying over a base | B(x) for x : A, written Π(x:A).B(x) or Σ(x:A).B(x) |
| **Equivalence** | A function with contractible fibers—the "right" notion of isomorphism | A ≃ B |
| **n-type (h-level)** | How much "higher structure" a type has | Sets are 0-types, propositions are (-1)-types |

**Morphisms:** Functions f : A → B. But crucially, functions *respect paths*—they're automatically "continuous" in the homotopy sense. If p : a = a', then ap_f(p) : f(a) = f(a').

---

### C. CENTRAL INVARIANTS

- **Homotopy level (h-level / n-type):** How complicated is the equality structure?
  - **(-2)-type (contractible):** Exactly one point, no interesting paths
  - **(-1)-type (proposition):** At most one point—"truth value"
  - **0-type (set):** Points may differ, but any two paths between same points are equal
  - **1-type (groupoid):** Paths between paths may differ, but 3-paths are trivial
  - **...and so on**

- **Equivalence:** A ≃ B means A and B are "the same" in the strongest sense. Univalence makes this literal equality.

- **Truncation:** Forgetting higher structure. ||A|| ("mere proposition") remembers only whether A is inhabited, not how.

**What counts as "the same":** Two types are the same if they're equivalent. Two paths are the same if there's a path between them (a 2-path). This keeps going up—equality *at every level* is itself structured.

---

### D. SIGNATURE THEOREMS

**1. The Univalence Axiom**
> *(A ≃ B) ≃ (A = B)*
> *Equivalence of types is equivalent to equality of types.*

**Why it matters:** This is the heart of HoTT. It says: *things that behave the same ARE the same*. If two types are equivalent (isomorphic in the appropriate sense), there's a path between them in the universe of types. You can *transport* along this path—anything you prove about A automatically applies to B.

This is what mathematicians always wanted but set theory couldn't provide. "The reals as Dedekind cuts" and "the reals as Cauchy sequences" are *definitionally equal* once you establish equivalence.

**2. Function Extensionality (follows from univalence)**
> *If f(x) = g(x) for all x, then f = g*

**Why it matters:** Two functions that give the same outputs are equal. Obvious, right? But it's unprovable in basic type theory. Univalence gives it to you. This is essential for reasoning about functions as first-class objects.

**3. Higher Inductive Types (HITs)**
> *You can define types by specifying not just points but also paths (and higher paths) as constructors.*

**Why it matters:** This lets you build spaces directly. Want a circle? One point, one non-trivial loop. Want a sphere? One point, one 2-path. Want to quotient by an equivalence relation? Add paths between equivalent points. HITs are how HoTT captures topology synthetically.

**Example:** The circle S¹ is defined by:
- base : S¹ (a point)
- loop : base = base (a path from base to itself)

That's it. This *is* the circle, not a representation of it.

---

### E. BRIDGES TO OTHER DOMAINS

| Domain | Connection |
|--------|------------|
| **Topology** | Types are spaces, paths are paths, higher paths are homotopies. n-types correspond to n-groupoids. Fundamental group π₁ emerges naturally. |
| **Category Theory** | Types and functions form a category. Higher structure makes it an ∞-category/∞-groupoid. Univalence = "the universe is a univalent (∞,1)-category." |
| **Logic (Curry-Howard)** | Types = propositions, terms = proofs, identity type = equality proposition. A proof of a=b is evidence they're equal. Different proofs = different paths = equality has structure. |
| **Proof Assistants** | Implemented in Agda, Coq (with axioms), Lean (partly), and fully in Cubical Agda, Cubical Type Theory. Proofs are programs. |
| **Higher Category Theory** | HoTT is a synthetic theory of ∞-groupoids. What took pages of simplicial machinery becomes native. |
| **Physics** | Gauge equivalence as paths. "Physical states" as equivalence classes = truncation. Some speculate HoTT-like structure in quantum gravity. |

**Pattern-linking gold:**

The Curry-Howard-Lambek correspondence extends:
- **Propositions ↔ Types ↔ Objects**
- **Proofs ↔ Terms ↔ Morphisms**  
- **Proof simplification ↔ Computation ↔ 2-morphisms**

HoTT adds:
- **Equality proofs ↔ Paths ↔ Isomorphisms**
- **Paths between paths ↔ Homotopies ↔ Natural transformations**

*It's all the same structure viewed from different angles.*

---

### F. COMMON MISCONCEPTIONS

1. **"Identity type = definitional equality"** — No! Definitional equality (a ≡ b) is computational, automatic, no content. *Identity type* (a = b) is propositional equality—it has terms (paths), and there can be many distinct paths. The whole point is that propositional equality *has structure*.

2. **"A path is a continuous function [0,1] → X"** — That's the classical picture. In HoTT, paths are *primitive*. The interval isn't a type we define first; paths are basic, and the interval emerges from them. Paths are evidence of equality, not maps from a separate interval type.

3. **"Univalence says isomorphic things are identical"** — Close but imprecise. Univalence says there's a *canonical equivalence* between "A ≃ B" and "A = B". It doesn't collapse everything—it enriches equality to track *how* things are the same.

4. **"HoTT is just topology dressed up"** — HoTT is *synthetic* homotopy theory. It's not that we model types as spaces; types *are* spaces, primitively. The homotopy interpretation guided discovery, but HoTT stands alone as a foundation.

5. **"This is too abstract to compute with"** — Cubical type theory gives computational content to univalence. Paths are now concrete. This is implemented and works.

6. **"Equality is simple—things either are or aren't equal"** — This is the deepest misconception. In HoTT, *how* things are equal matters. The space of equalities can be non-trivial. A loop (a path from x to x) is a non-trivial self-equality. Symmetries live here.

---

### G. NOTATION SURVIVAL KIT

| Symbol | Meaning |
|--------|---------|
| a : A | "a is a term of type A" / "a inhabits A" / "a is a point in A" |
| A → B | Function type (non-dependent) |
| Π(x:A).B(x) or ∀(x:A).B(x) | Dependent function: for each x:A, produces something in B(x) |
| Σ(x:A).B(x) or ∃(x:A).B(x) | Dependent pair: a point x:A together with something in B(x) |
| a = b or Id_A(a,b) | Identity type: the type of paths from a to b |
| refl_a or refl | The trivial path from a to itself |
| p⁻¹ | Path reversal: if p : a = b, then p⁻¹ : b = a |
| p · q or p ∙ q | Path concatenation: if p : a = b and q : b = c, then p·q : a = c |
| ap_f(p) or f(p) | "Action on paths": applying f to path p gives path f(a) = f(b) |
| transport or tr | Moving along a path in a dependent type: if p : a = b and u : B(a), get tr_p(u) : B(b) |
| A ≃ B | A is equivalent to B (the "right" notion of sameness for types) |
| 𝒰 or Type | The universe of (small) types |
| ‖A‖ or ∥A∥ | Propositional truncation: "A is merely inhabited" |
| isContr(A) | A is contractible (has exactly one point up to paths) |
| isProp(A) | A is a mere proposition (any two inhabitants are equal) |
| isSet(A) | A is a set (no higher path structure) |

---

### H. ONE WORKED MICRO-EXAMPLE

**The problem:** Show that the identity type of Bool has exactly two paths from true to true in a set-like interpretation—but in full HoTT, we need to *construct* this.

Actually, let's do something more illuminating:

**Path induction (the fundamental tool):**

Suppose we want to prove something about all paths. Path induction says:

> To define a function on all paths p : a = b, it suffices to define it when p is refl_a : a = a.

**Intuition:** Any path is homotopic to the trivial path (if we're allowed to move the endpoint). So proofs/constructions for refl extend to all paths.

**Micro-example: Symmetry of equality**

**Goal:** Given p : a = b, produce p⁻¹ : b = a.

**Construction via path induction:**
- We need to define, for all a, b : A and p : a = b, something of type b = a.
- By path induction, it suffices to handle p = refl_a.
- When p = refl_a : a = a, we need something of type a = a.
- We have refl_a : a = a. Done.

So: p⁻¹ is defined by "if p is refl, then p⁻¹ is refl."

**Why this is profound:** We didn't *check* that equality is symmetric—we *constructed* the symmetry. The proof *is* a function that transforms paths. This function has computational content. In cubical type theory, you can actually run it.

**Slightly deeper example: Transport**

If B : A → 𝒰 is a type family and p : a = a' is a path, then transport gives:

tr_p : B(a) → B(a')

"You can move inhabitants of B along the path p."

**Construction:** By path induction, it suffices to handle p = refl_a. But then B(a) = B(a'), so we just need the identity function. Done.

**Why this matters:** Transport is how univalence becomes useful. If you prove A ≃ B, univalence gives you a path p : A = B in the universe. Then for any type family F over the universe, transport along p moves things: F(A) → F(B). Theorems about A become theorems about B *automatically*.

---

### For your work specifically:

**Convergence Thesis:** HoTT formalizes "equivalent structures are identical." If cognitive architectures are constrained by mathematical necessities, and those constraints determine structure up to equivalence, HoTT says there's *essentially one* such structure. The paths between equivalent solutions aren't just metaphor—they're the formal content of "same solution found different ways."

**Protein folding / cognitive architecture:** Both involve finding stable configurations under constraints. The HoTT angle: the "space of solutions" has homotopical structure. Distinct folding pathways that reach the same fold are *paths between paths*. The fold itself is a point; the pathways are 1-paths; pathway-equivalences are 2-paths. If the solution space is contractible (all paths collapse), there's essentially one answer.

**Kat's insight about type equivalence:** When two explanations "feel equivalent," you're detecting a path. When two problems are "secretly the same," there's an equivalence. HoTT makes these intuitions *loadbearing*—they're not just heuristic, they're structure.

The quote you included—"Every time I reach for an analogy, I'll feel the natural transformation operating"—that's exactly right. HoTT reveals that these cognitive moves *are* the mathematics, not approximations to it.

---
