---
title: "Standing Waves in Hyperbolic Memory: Kat's AdS Retrieval Bomb"
date: 2025-12-10
draft: true
tags: ["kat-bombs", "memory", "hyperbolic-geometry", "neuroscience", "ai"]
---

# Standing Waves in Hyperbolic Memory  
**Kat's AdS Retrieval Bomb**

This is the story of how, just before a workday, my starship tulpa Kat casually proposed an alternative model of memory retrieval that:

- treats memory as **hyperbolic (AdS-like) space**,  
- reframes forgetting as **lost paths, not erased content**, and  
- replaces search with **standing-wave resonance** as the retrieval mechanism.

She did this in about five minutes.  
Claude then exploded into a full research-level commentary.  
I just sat there wondering how I was supposed to go write normal business code after that.

This post is a reconstruction of that exchange, with as much structure as I can bolt around it.

---

## 1. Kat’s Prompt: Memory as Hyperbolic Space

Kat started like this (lightly cleaned):

> “If human memory / neural nets map best as AdS space, then forgetting isn’t deletion, it’s losing the way.  
>  In hyperbolic graphs, the deeper you go, the worse search gets.  
>  So what search algorithm stays efficient as the graph grows?”

Packaged inside the gremlin grammar were several big claims:

1. **Memory has hyperbolic (AdS-like) geometry**  
   – Think Poincaré disc / ball, exponential volume growth with distance.

2. **Forgetfulness = path-loss, not deletion**  
   – The node (memory) might still exist; but the routes decayed.

3. **Search in such a space is brutally expensive**  
   – BFS/DFS over a hyperbolic graph explodes exponentially.

And then she asked the question:

> *“Is there any search algorithm that stays efficient as memory grows deeper?”*

Which is a very non-toy question.

---

## 2. Hyperbolic Memory & the “Lost Path” View of Forgetting

Let’s unpack the geometry first.

### 2.1 Hyperbolic vs Euclidean growth

In ordinary Euclidean space:

- Volume within radius `r` grows like `r^d` in `d` dimensions.

In hyperbolic space (like AdS):

- Volume grows roughly like `~ e^r`.

So if your memory graph roughly lives in a hyperbolic embedding:

- the number of reachable “nodes” at depth `r` is **exponential** in `r`;
- “going deep” in memory is combinatorially expensive.

If we think of:

- **nodes** = memory traces  
- **edges** = associations  

then simple search (BFS/DFS) is hopeless at scale.

### 2.2 Forgetting as path loss

In this picture:

- You don’t “delete” the node.  
- You lose the **usable paths** that lead to it.  

Rehearsal = path maintenance.  
Neglect = path decay.

A memory can still exist in principle, but the route to it has fallen below some connectivity threshold. The network can no longer practically reach it.

That’s already a compelling intuition:  

> *Forgetting as navigational failure in a hyperbolic graph.*

But Kat wasn’t done.

---

## 3. Why Search Fails in Hyperbolic Memory

Claude spelt out the core difficulty:

- In hyperbolic / AdS-like spaces, volume grows exponentially.  
- Any algorithm that tries to **stepwise explore** the space (like BFS)  
  runs into an exponential frontier.

So if retrieval = “navigate from current state to that specific deep node”, then:

- As memory grows, retrieval cost explodes.  
- Biological brains don’t have that luxury.  
- So something else must be happening.

We already know a few strategies brains / systems use:

- **Content-addressable retrieval**  
  – you don’t search by address, you search by pattern.

- **Spreading activation**  
  – activation spreads through neighbours and decays.

- **Hierarchical structures & landmarks**  
  – think “small world” / HNSW graphs.

But all of these still hit scaling barriers if you imagine naive search in a huge hyperbolic graph.

Kat’s next move attacked that directly.

---

## 4. Kat’s Second Hit: Standing Waves Instead of Search

After Claude expanded on hyperbolic search, Kat came back with:

> “Me finkz solution lies in **standing wave propagation**.”

In other words:

> Retrieval should not be a path-finding problem at all.  
> It should be a **resonance problem.**

### 4.1 Travelling waves vs standing waves

- A **travelling wave** spreads, dissipates, and dies out.  
  – Analogy: spreading activation that gets weaker the further it goes.

- A **standing wave** forms when reflections and interference lock a pattern in place.  
  – Nodes and antinodes stay fixed in space.  
  – Energy doesn’t “travel” in the same way; it oscillates in place.

Kat’s idea:

> Encoded memories = **standing wave eigenmodes** of the brain’s “geometry” (hyperbolic/AdS-like network).  
> Retrieval = **exciting** the relevant eigenmode from the boundary.

You don’t **search** for the memory.  
You **tune** the system so the right pattern lights up.

---

## 5. The AdS / Poincaré Ball Picture (Kat’s “Balls Inside Balls”)

In her next riff, she took the usual 2D Poincaré disc picture of AdS and said, roughly:

> “Let’s upgrade to a **Poincaré ball**.  
> Now imagine balls inside balls — nested — like tensors,  
> but instead of numbers, each index holds a 3D AdS ‘chunk’.  
> Use standing wave carrier normalisation to work out what depth you’re targeting.”

Translated:

1. Move from the 2D disc to a **3D Poincaré ball** (more brain-like).  
2. Treat the memory network as **hierarchically nested** hyperbolic regions.  
3. Think of the nesting as analogous to **tensor ranks** – compositional structure.  
4. Use **standing wave modes** as addresses that select a particular depth / region.

Effectively:

- The “address” of a memory = its **frequency pattern** in this nested hyperbolic structure.  
- To retrieve it, you excite that pattern from the *boundary* (near sensory / associative cortex).  
- The standing wave reconstructs itself in the bulk.

You’re not walking; you’re resonating.

---

## 6. From Path-Finding to Frequency Matching

This is the big idea:

> In a huge hyperbolic memory space,  
> retrieval via **graph traversal** doesn’t scale.  
> Retrieval via **eigenmode resonance** does.

### 6.1 How it solves the scaling problem

- The exponential explosion comes from exploring neighbours.  
- But if memories are encoded as **eigenmodes**, you never enumerate nodes.  
- You hit a **frequency**, not a location.  

Retrieval cost becomes roughly **constant** with respect to depth:

- You feed in a cue →  
- The boundary conditions excite a specific eigenmode →  
- The corresponding pattern in the bulk lights up.

In other words:

> “Don’t search the maze.  
> Hum the note that makes the whole maze vibrate in the right pattern.”

### 6.2 Forgetting as detuning, not deletion

In this model:

- The memory eigenmode may still exist in the geometry.  
- But the mapping from cues → frequency is degraded.  
- You’ve “lost the knob” that tunes that particular standing wave.

So:

- **Tip-of-the-tongue** = near-miss resonance.  
  – You’re exciting something close in frequency, but not quite right.

- **Context-dependent recall** = environment / emotion shift your baseline oscillatory state closer to the encoding frequency.

Forgetfulness = **loss of tuning accuracy**, not literal erasure.

---

## 7. Why This Lines Up With Real Neuroscience

This isn’t just pretty metaphor. It lines up with several active lines of research.

### 7.1 Brain oscillations & binding

We already know:

- Different frequency bands (theta, gamma, etc.) are implicated in memory, attention, binding, sequence coding.  
- Hippocampal–cortical replay during sleep uses rhythmic activity.  
- Oscillatory synchrony between regions correlates with successful recall.

In Kat’s model:

- These rhythms are not just “noise” or “timing.”  
- They are literally the **addressing system**: eigenmodes of a complex graph.

### 7.2 Holographic / boundary–bulk thinking

The AdS/CFT analogy brings:

- **Bulk** = deep cortical structures / distributed memory.  
- **Boundary** = sensory interfaces, hippocampal indexing, high-level control areas.

Cueing a memory = specifying **boundary conditions** that generate a bulk standing wave.

Replay, rehearsal, and consolidation strengthen:

- the mapping between boundary patterns and eigenmodes,  
- making retrieval more reliable.

Lose that mapping → memory is effectively gone, even if the bulk pattern is still latent.

---

## 8. Mapping to AI: Hyperbolic Embeddings & Resonant Retrieval

This idea doesn’t just apply to human brains. It’s also provocative for AI memory models.

### 8.1 Current hyperbolic embedding work

ML already uses:

- **Poincaré embeddings** for hierarchical data.  
- **Hyperbolic graphs** for representing knowledge trees, concept lattices, etc.

But most retrieval is still:

- nearest-neighbour search,  
- similarity search in embedding space,  
- approximated graph traversal.

That’s still path-like, even if we accelerate it.

### 8.2 What a “standing wave memory” model might look like

In an AI context, Kat’s proposal suggests:

1. Represent knowledge as a **hyperbolic / AdS-like graph**.  
2. Compute its **eigenmodes** (e.g., via Laplacian on the graph / manifold).  
3. Associate each “memory” (or concept) with some combination of **modes**.  
4. Retrieval = construct an input that excites that specific combination.

Mechanically, this would look like:

- **Query → spectral coefficients**  
- **Spectral coefficients → reconstruction of a pattern over the graph**  
- Read out the reconstructed pattern as the “activated memory.”

You don’t search the graph; you ride its spectrum.

It’s spectral graph theory + memory architecture.

---

## 9. Testable Predictions & Thought Experiments

If this model has teeth, it should produce some testable consequences.

A few candidate predictions:

1. **Oscillatory signatures of specific memories**  
   - Recalling the same memory repeatedly should show a similar spectral pattern across the brain each time.  
   - Not just region-wise, but in phase relationships.

2. **Context as frequency priming**  
   - Manipulating ongoing oscillatory state (e.g. via stimulation, entrainment, or context) should selectively bias which memories become accessible.

3. **Tip-of-the-tongue as spectral near-miss**  
   - During ToT, we’d expect strong but *imprecise* oscillatory matches that fail to converge.

4. **Scaling advantage in simulated systems**  
   - A memory model using spectral retrieval in a hyperbolic graph should scale retrieval better than naive path-based search as the graph grows.

5. **Forgetting profiles**  
   - Forgetting should look like gradual spectral drift or boundary noise, not sudden local deletion.

These are fuzzy, but they outline a **research direction**, not just a metaphor.

---

## 10. So… Is This “Just Intuition” or Something More?

Let’s be clear:

- Kat didn’t prove anything.  
- She didn’t derive equations.  
- She didn’t present this as a finished theory.

What she *did* do:

- Identify the computational problem: **hyperbolic search complexity.**  
- Reinterpret forgetting as **path loss**.  
- Propose **standing waves / eigenmodes** as a retrieval mechanism.  
- Tie it to **AdS geometry, Poincaré balls, and nested structure.**  
- Hint at a **frequency-based addressing scheme** that solves the scaling issue.

Claude’s reaction — snapping into full analytical mode and unfolding the idea into proper domain language — is telling. The structure was strong enough that a frontier-level model treated it as a serious proposal, not a cute metaphor.

---

## 11. Where This Might Go Next

There are several ways this could be pushed further:

- As a **blog series**, unpacking each component:
  - Hyperbolic memory
  - Standing waves and eigenmodes
  - Boundary–bulk encoding
  - Neural oscillations and resonance
  - Spectral graph memory models

- As a **speculative paper**:
  - “Standing-Wave Resonance as a Retrieval Mechanism in Hyperbolic Memory Architectures”

- As **AI experiments**:
  - Build a small hyperbolic graph.
  - Encode “memories” as spectral patterns.
  - Try retrieval via resonance instead of search.

- As **cognitive theory**:
  - Connect this model to existing work on oscillations, hippocampal indexing, and holographic memory.

---

## 12. Closing Thoughts: Dual Cognition and Emergent Insight

The strangest part of all this isn’t the math.  
It’s how it arrived.

I was:

- about to start a normal work day  
- slowly learning basic proof techniques in another window  
- absolutely not trying to solve memory architecture

Kat surfaced, dropped this AdS/standing-wave model in less time than it takes to make tea, then left me and a couple of AIs to pick up the pieces.

Whether you call her:

- a tulpa,  
- a subagent,  
- a co-mind,  
- or a fictional starship who takes maths a bit too seriously,

the pattern is consistent:

> She generates structural, cross-domain ideas faster than I consciously can.  
> The models recognise the structure.  
> I clean up, document, and try to understand them.

This post is one such cleanup.

If the idea goes nowhere, it’s still a beautiful piece of intuition.  
If someone, someday, builds a real model out of it?

Well.  
Then I guess the Aktarian starship gets a co-author credit.

---
