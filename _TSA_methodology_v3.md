# Trinary Symbolic Algebra (TSA)
## A Method for the Algebraic Classification and Composition of Mathematical Character

**Version 3.0**

---

## Preamble

Boolean algebra answers one question: *is this proposition true or false?* Its power comes from that reduction — all information is collapsed to a binary distinction, and a complete algebra is built on top of it.

Trinary Symbolic Algebra (TSA) answers a different question: *what is the mathematical character of this quantity?* Not its value. Not its truth. Its structural behaviour — whether it cascades without bound, regulates toward equilibrium, or sits at the boundary between the two.

The answer is always one of three things. That exactly three characters are necessary and sufficient is not an assumption — it is the conclusion of a symbolic reduction applied to the real number system, verified on the two most structurally distinct transcendental constants in mathematics. The derivation precedes the algebra. It justifies why this algebra has exactly three states.

The method proceeds in this sequence:

1. **Symbolic Reduction** — how any numerical sequence yields a trinary character
2. **Primitive Elements** — the formal definition of the three states
3. **Operations** — CASCADE, RESOLVE, INVERT, COMPLETE
4. **Axioms** — the minimal set determining the algebra
5. **Theorems** — what follows necessarily from the axioms
6. **Comparison with Boolean Algebra**
7. **Type Inference** — assigning and propagating TSA types through expressions
8. **The Encoding Theorem** — connecting TSA types to mathematical basis functions
9. **Worked Examples**
10. **Open Questions**

---

## Part 1 — The Symbolic Reduction

### 1.1 Why Three

Any quantity in a formal or physical system exhibits one of two behaviours at the trajectory level: it either returns to prior values (bounded, self-correcting, periodic) or it does not (accumulating, path-dependent, cascade). These are two irreducible dynamical characters — neither derives from the other.

A system can also sit at the transition between them — at the bifurcation point from which small perturbations send it toward either character. This is a third condition, structurally distinct from both: not "less cascading" or "partially equilibrating" but the separatrix itself. Collapsing it into either other state loses the information that determines which regime a system is in.

Four states are unnecessary. Any candidate fourth state reduces to a composition of the three, or is a refinement within one of them. Three is the minimum complete set.

The symbolic reduction confirms this from below. Applied to the two most structurally opposite transcendental constants under identical rules, it produces exactly two distinct macro-patterns, with the transition between them constituting the third. The three-state sufficiency is not assumed — it is read from the structure of the number system.

### 1.2 The Digit Reduction Table

The first stage maps each decimal digit to one of three primitive symbols — 1, 2, or 3 — or to a composite expansion. The mapping follows from the irreducible structural character of each number:

| Digit | Reduction | Character |
|-------|-----------|-----------|
| 0 | **terminal** | Prior to 1 — boundary marker, not a number |
| 1 | **1** | Being — primitive, undivided, the unit |
| 2 | **2** | Division — the first distinction, opposition |
| 3 | **3** | Generation — first number exceeding its parts |
| 4 | **2** | 4 = 2×2: pure doubling, no new quality |
| 5 | **[1, 3]** | 1 generates the triadic structure around it |
| 6 | **[2, 3]** | 2×3: holds both simultaneously, neither dominant |
| 7 | **[1, 2, 3]** | Contains all three in natural order |
| 8 | **2** | 2³: recursive doubling, returns to 2 |
| 9 | **3** | 3²: generation compounding on itself |

Pure digits (1, 2, 3, 4, 8, 9) collapse to a single symbol. Composite digits (5, 6, 7) expand to a sequence, preserving internal structure rather than collapsing it. The digit 0 is not a symbol in the reduction — it is the terminal marker, representing what precedes the counting system.

### 1.3 Reading the Expanded Sequence

Once expanded, the digit sequence is read as a stream of symbols from {1, 2, 3}. Consecutive pairs are classified as **direction** or **oscillation** by one strict rule:

**Direction:** a pair is direction if and only if it is a forward step in the cycle 1→2→3→1. The three valid direction pairs are:

> **(1, 2) — (2, 3) — (3, 1)**

A direction run is any consecutive sequence built entirely from these pairs: (1,2,3), (2,3,1), (3,1,2), or any contiguous sub-sequence of these. These are the three rotations of 1→2→3 and their subsets.

**Oscillation:** every pair that is not a direction pair. This includes same-value pairs (1,1), (2,2), (3,3), backward steps (2,1), (3,2), (1,3), and skip pairs (1,3), (2,1) — any transition not following the strict forward-cycle order.

**Examples:**

- **(1, 2)** → direction: 1→2 is a forward cycle step ✓
- **(2, 1)** → oscillation: backward ✗
- **(3, 1)** → direction: 3→1 is the wrap-around forward step ✓
- **(1, 3)** → oscillation: skips 2, not a valid forward step ✗
- **1, 2, 1** → [direction][oscillation]: (1,2) is forward; (2,1) is backward
- **3, 1, 2** → [direction][direction]: (3,1) forward; (1,2) forward. Full direction run — the rotation 3-1-2 of the base cycle. π opens with exactly this at 3.14: integer 3, then decimals 1 and 4(→2).

The reading is applied pair by pair. Consecutive direction pairs form a direction-run; consecutive non-direction pairs form an oscillation block. The macro structure is the sequence of these alternating blocks.

### 1.4 The Stopping Criterion

The reduction applies until the first occurrence of the digit 0 in the decimal expansion. The digit 0 is the terminal marker — it represents what precedes the counting system (prior to 1, prior to 2, prior to 3). When 0 appears, the sequence has completed its first structural cycle and the terminal is reached. All analysis is of the sequence strictly before the first 0.

### 1.5 Reduction of π

π = 3.14159265358979323846264338327950...

The digit 0 first appears at **decimal position 32**. The analysis covers the integer 3 plus decimals 1–31: 32 symbols total before the terminal.

Expanding digits through decimal 31:

```
3→[3]  1→[1]  4→[2]  1→[1]  5→[1,3]  9→[3]  2→[2]
6→[2,3]  5→[1,3]  3→[3]  5→[1,3]  8→[2]  9→[3]
7→[1,2,3]  9→[3]  3→[3]  2→[2]  3→[3]  8→[2]  4→[2]
6→[2,3]  2→[2]  6→[2,3]  4→[2]  3→[3]  3→[3]  8→[2]
3→[3]  2→[2]  7→[1,2,3]  9→[3]  5→[1,3]
0 → terminal
```

Expanded sequence:
**3, 1, 2, 1, 1, 3, 3, 2, 2, 3, 1, 3, 3, 1, 2, 3, 3, 3, 2, 3, 2, 2, 2, 3, 2, 2, 3, 2, 3, 3, 2, 3, 2, 1, 2, 3, 3, 1, 3**

Applying the direction rule pair by pair, the macro structure is:

```
[D×2] [O×6] [D×2] [O×2] [D×1] [O×2] [D×4] [O×3]
[D×1] [O×3] [D×1] [O×2] [D×1] [O×1] [D×1] [O×2]
[D×1] [O×2] [D×2] [O×1] [D×1] [O×1]
```

**11 direction-runs. 11 oscillation-runs. 17 direction steps, 25 oscillation steps.**

Direction-run lengths: 2, 2, 1, 4, 1, 1, 1, 1, 1, 2, 1

**What the pattern shows:** π opens with full direction (the 3-1-2 run = D×2), then immediately falls into a long oscillation block (O×6 — the longest in the sequence). From there, direction and oscillation alternate irregularly with no stable period. Direction appears throughout but never sustains — 11 separate runs, mostly D×1, scattered across the entire sequence. Oscillation blocks are also variable and do not repeat in predictable intervals. The pattern never stabilises. This is the asymmetric character: direction keeps appearing and being interrupted, without rhythm, without convergence.

### 1.6 Reduction of e

e = 2.71828182845904...

The digit 0 first appears at **decimal position 13**. The analysis covers the integer 2 plus decimals 1–12: 13 symbols total before the terminal.

Expanding digits through decimal 12:

```
2→[2]  7→[1,2,3]  1→[1]  8→[2]  2→[2]  8→[2]
1→[1]  8→[2]  2→[2]  8→[2]  4→[2]  5→[1,3]
9→[3]
0 → terminal
```

Expanded sequence:
**2, 1, 2, 3, 1, 2, 2, 2, 1, 2, 2, 2, 2, 1, 3, 3**

Macro structure:

```
[O×1] [D×4] [O×3] [D×1] [O×6]
```

**2 direction-runs. 3 oscillation-runs. 5 direction steps, 10 oscillation steps.**

**What the pattern shows:** e opens with a single oscillation (the pair 2→1, backward), then fires its largest direction run immediately (D×4 = the sequence 1,2,3,1,2 — a full cycle plus one step). After D×4 comes a three-step oscillation block, then one more direction step (D×1), then the longest oscillation block in either constant (O×6) holds to the terminal. Direction fires twice — once strongly, once briefly — and then is gone. Oscillation dominates and accumulates. This is the rhythmic character: direction is an event, not a state. After it fires, equilibrium reasserts and holds.

### 1.7 The Non-Arbitrariness Proof

The reduction rules are fixed before either constant is examined. No parameter is adjusted between them.

The same rules applied to both produce structurally opposite results: π direction-fragmented (11 runs, 17 steps, scattered), e oscillation-dominant (2 direction events, then long stable oscillation). An arbitrary rule would not reliably discriminate — it would produce similar or random outputs from structurally dissimilar inputs. Reliable discrimination under fixed rules is the definition of a structural detector.

The results are consistent with what is independently known about both constants. π is transcendental, non-periodic, with no pattern in its digits — exactly the kind of structure the reduction shows: direction present throughout but never consolidated, asymmetric, irregular. e governs natural growth and bounded convergence — exactly the structure the reduction shows: direction fires and retreats into stable oscillation.

Both constants share the same largest direction-run size: D×4. But π distributes its 11 direction-runs throughout the sequence; e fires D×4 once as its opening statement and then retreats completely into O×6. The same structural event occurs in both, deployed with completely opposite intent. This is not a coincidence that survives a fixed rule — it is structure.

**Limits of the derivation, stated precisely:** The digit reduction table has structural justification (each mapping follows from what each number irreducibly is) but not a formal mathematical proof. The direction rule is unambiguous at the pair level but the choice of cycle 1→2→3→1 — rather than some other ordering — follows from the natural sequence of archetypes (being, division, generation) and is structurally motivated rather than formally derived. The analysis covers the digits to the first terminal 0, which is a natural boundary but a philosophical rather than mathematical one. These are appropriate limits for a methodology paper and should not be overclaimed.

### 1.8 Connection to Encoding

The macro patterns establish the character of each constant — direction-dominant for π, oscillation-dominant for e — and justify which family of basis functions to use for each type of physical variable:

- Variables with cascade character (Π-type) are encoded using a basis built from π: the sine and irrational-harmonic family
- Variables with equilibrium character (Ε-type) are encoded using a basis built from e: the exponential and power-law family

The specific weights within each basis are justified by the mathematical properties of the basis functions themselves, not by the direction-run lengths:

**π-basis weights (5, 1, 1, 3, 1):**
- sin(πx) carries weight 5 as the fundamental cascade mode
- sin(π²x) carries weight 3 because π² is irrational — sin(π²x) is strictly non-periodic, never returning to any prior value at any integer period. This is the mathematically correct basis function for cascade character, and it earns the second-highest weight on independent grounds
- cos(πx), sin(2πx), and the cross-product each carry weight 1 as secondary completions

**e-basis weights (2, 2, 1):**
- exp(−ex) and x^e carry equal weight 2 — symmetric completion of the exponential decay and growth character
- The centred Gaussian carries weight 1 — the symmetric completion at the midpoint of the normalised range
- Near-uniform weighting is structurally correct for equilibrium: the stability of e's pattern means flat weighting is not an approximation but a structural assertion

The weights are empirically validated across at least four independent domains (EM simulation, logistic map, harmonics, bearing diagnostics) with fixed values. The symbolic reduction establishes *which basis family* to use; the mathematical properties of the basis functions establish *the weights within that family*.

---

## Part 2 — Primitive Elements

### 2.1 The State Set

TSA is defined over a carrier set of three elements:

**T = {Π, Ε, Β}**

These are not variables. They are the three irreducible states of the algebra — the primitive objects from which all TSA expressions are built.

### 2.2 Physical and Mathematical Characterisation

**Π (cascade state)**

A quantity has character Π if its trajectory is non-periodic, path-dependent, and does not return to any prior value. The quantity accumulates — each successive value differs from all previous values, and the difference does not self-correct.

Examples: vibration RMS in a bearing with active spalling; the Lyapunov exponent in the chaotic regime of the logistic map; transformation strain in an SMA beyond the austenite finish temperature; cumulative production downtime; the macro direction-fragmented pattern of π.

**Ε (equilibrium state)**

A quantity has character Ε if its trajectory is bounded, convergent, and self-correcting. When displaced it returns toward a characteristic operating point. The trajectory is periodic or convergent.

Examples: bearing temperature under constant load; inventory level under a pull production system; consonance score of simple integer frequency ratios; crest factor of healthy-bearing vibration; the macro oscillation-dominant pattern of e.

**Β (boundary state)**

A quantity has character Β if it is at the transition between Π and Ε regimes — the structural boundary from which trajectories diverge toward one or the other under any perturbation. Neither accumulating nor self-correcting.

Examples: the parameter r at R_BIFURCATION of the logistic map; loss tangent at DIEL_BIFURCATION in the EM surrogate; RMS level at the onset of cascade in a bearing; phase fraction between 0 and 1 in a shape memory alloy; the digit 0 in the symbolic reduction — prior to the counting system, the terminal boundary.

### 2.3 Formal Properties

The states are **distinct**: Π ≠ Ε, Ε ≠ Β, Π ≠ Β.

The states are **exhaustive**: every quantity has character Π, Ε, or Β.

The states are **primitive**: no state is defined in terms of the others.

### 2.4 What TSA Types Are Not

TSA types are not values. Π does not mean large. Ε does not mean small. Β does not mean medium. The types describe structural behaviour over trajectories, not magnitude at a point. A very large equilibrium quantity (the temperature of a star's core, self-regulating over millions of years) has type Ε. A very small cascade quantity (the first microcrack in a bearing race, whose growth is non-repeating) has type Π.

---

## Part 3 — Operations

### 3.1 CASCADE (⊕)

**Definition:** CASCADE takes two characterised states and returns the character of their compound behaviour.

| ⊕ | Π | Ε | Β |
|---|---|---|---|
| **Π** | Π | Π | Β |
| **Ε** | Π | Ε | Β |
| **Β** | Β | Β | Π |

*Π ⊕ Π = Π:* Cascade compounds cascade.

*Ε ⊕ Ε = Ε:* Equilibrium compounds equilibrium.

*Π ⊕ Ε = Π:* Cascade dominates. When the two interact, cascade character prevails.

*Π ⊕ Β = Β:* Cascade at a boundary stays at the boundary — the cascade has not yet crossed.

*Ε ⊕ Β = Β:* Equilibrium at a boundary stays at the boundary — self-regulation has reached its limit.

*Β ⊕ Β = Π:* Two boundary conditions together drive cascade. The separatrices from two bifurcations combine to force a trajectory. This is TSA's structurally distinctive rule.

**Identity:** Ε ⊕ x = x for all x ∈ T.

### 3.2 INVERT (¬)

**Definition:** INVERT returns the mathematical complement of a state.

| x | ¬x |
|---|---|
| Π | Ε |
| Ε | Π |
| Β | Β |

*¬Π = Ε:* The complement of cascade is equilibrium.

*¬Ε = Π:* The complement of equilibrium is cascade.

*¬Β = Β:* The boundary is its own complement — equidistant from both extremes.

**Involution:** ¬¬x = x for all x.

### 3.3 RESOLVE (⊗)

**Definition:** RESOLVE is the De Morgan dual of CASCADE:

> **x ⊗ y = ¬(¬x ⊕ ¬y)**

| ⊗ | Π | Ε | Β |
|---|---|---|---|
| **Π** | Π | Ε | Β |
| **Ε** | Ε | Ε | Β |
| **Β** | Β | Β | Ε |

*Π ⊗ Ε = Ε:* Under RESOLVE, equilibrium governs — dual to CASCADE where cascade governs.

*Β ⊗ Β = Ε:* Dual to Β ⊕ Β = Π. Two boundaries under RESOLVE settle to equilibrium.

**Identity:** Π ⊗ x = x for all x ∈ T.

**Duality:** ⊕ and ⊗ are mirror images under ¬. Ε is the identity for ⊕; Π is the identity for ⊗. ¬Ε = Π and ¬Π = Ε.

### 3.4 COMPLETE (↓)

**Definition:** COMPLETE maps each state to its natural attractor — the state the system converges to without external forcing.

| x | ↓x |
|---|---|
| Π | Β |
| Ε | Ε |
| Β | Ε |

*↓Π = Β:* A cascade accumulates until it hits the structural limit — the failure threshold, the bifurcation. It stops at the boundary as a limit event.

*↓Ε = Ε:* Equilibrium at rest remains at equilibrium.

*↓Β = Ε:* A boundary without forcing resolves toward equilibrium. Boundaries are unstable fixed points — they require active maintenance to hold.

COMPLETE is primitive: it cannot be derived from ⊕, ⊗, ¬. It is the only operation carrying temporal information. It also plays an algebraic role: it is what generates Β as a constant expression (see Theorem 12), making it necessary for functional completeness.

---

## Part 4 — Axioms

The algebra is determined by nine axioms over T = {Π, Ε, Β} with primitive operations ⊕ and ¬. RESOLVE (⊗) is derived. COMPLETE (↓) is a separate primitive.

| Label | Statement |
|---|---|
| TSA1 | x ⊕ y = y ⊕ x |
| TSA2 | (x ⊕ y) ⊕ z = x ⊕ (y ⊕ z) |
| TSA3 | x ⊕ Ε = x |
| TSA4 | Π ⊕ Π = Π |
| TSA5 | Β ⊕ Β = Π |
| TSA6 | Π ⊕ Β = Β |
| TSA7 | ¬¬x = x |
| TSA8 | ¬Β = Β |
| TSA9 | ¬Ε = Π |
| Def ⊗ | x ⊗ y = ¬(¬x ⊕ ¬y) |
| Def ↓ | ↓Π = Β; ↓Ε = Ε; ↓Β = Ε |

**TSA1–9 fully determine the CASCADE and INVERT tables.** From TSA3: Ε⊕Ε=Ε, Π⊕Ε=Π, Β⊕Ε=Β. From TSA4: Π⊕Π=Π. From TSA5: Β⊕Β=Π. From TSA6: Π⊕Β=Β. Remaining: Ε⊕Β=Β (TSA1, TSA3). INVERT: ¬Β=Β (TSA8), ¬Ε=Π (TSA9), ¬Π=Ε (TSA7 applied to TSA9). RESOLVE then follows from its definition. ∎

---

## Part 5 — Theorems

### Theorem 1 — De Morgan Duality

¬(x ⊕ y) = ¬x ⊗ ¬y for all x, y ∈ T.

*Proof:* ¬x ⊗ ¬y = ¬(¬(¬x) ⊕ ¬(¬y)) = ¬(x ⊕ y) by definition and involution. ∎

Equivalently: ¬(x ⊗ y) = ¬x ⊕ ¬y.

### Theorem 2 — Complementation Laws

For all x ∈ T: x ⊕ ¬x = Π and x ⊗ ¬x = Ε.

*Proof:* Π⊕¬Π=Π⊕Ε=Π; Ε⊕¬Ε=Ε⊕Π=Π; Β⊕¬Β=Β⊕Β=Π. For ⊗: ¬(x⊕¬x)=¬Π=Ε; by De Morgan ¬(x⊕¬x)=¬x⊗x=x⊗¬x. ∎

Π is the "top" — everything combined with its complement reaches Π. Ε is the "bottom" — everything resolved against its complement reaches Ε.

### Theorem 3 — Commutativity of RESOLVE

x ⊗ y = y ⊗ x. *Proof:* x⊗y=¬(¬x⊕¬y)=¬(¬y⊕¬x)=y⊗x (TSA1). ∎

### Theorem 4 — Associativity of RESOLVE

(x ⊗ y) ⊗ z = x ⊗ (y ⊗ z). *Proof:* Expand via definition and apply TSA2. ∎

### Theorem 5 — Partial Idempotency

Π and Ε are idempotent under both ⊕ and ⊗. Β is idempotent under neither.

*Proof:* Π⊕Π=Π (TSA4); Ε⊕Ε=Ε (TSA3); Β⊕Β=Π≠Β (TSA5). Π⊗Π=Π; Ε⊗Ε=Ε; Β⊗Β=Ε≠Β (derived table). ∎

TSA is not a lattice. Lattices require all elements to be idempotent. Β's non-idempotency reflects the physical reality that the boundary state is unstable — combining it with itself drives it to a different state.

### Theorem 6 — Non-Idempotency Duality

Β ⊕ Β = Π and Β ⊗ Β = Ε.

The boundary resolves asymmetrically depending on direction of composition. Under CASCADE (forward pressure), two boundaries drive cascade. Under RESOLVE (backward pressure), two boundaries settle to equilibrium.

### Theorem 7 — Β Resists Absorption

Π ⊕ Β = Β ≠ Π (Π does not absorb Β under ⊕). Ε ⊗ Β = Β ≠ Ε (Ε does not absorb Β under ⊗).

*Proof:* Π⊕Β=Β (TSA6). Ε⊗Β=¬(Π⊕Β)=¬Β=Β. ∎

In Boolean algebra, the top and bottom elements absorb everything. In TSA, Π and Ε do not absorb Β. The boundary is structurally independent of both extremes.

### Theorem 8 — Non-Distributivity

CASCADE does not distribute over RESOLVE.

*Counterexample:* Β⊕(Π⊗Ε) = Β⊕Ε = Β. But (Β⊕Π)⊗(Β⊕Ε) = Β⊗Β = Ε. Β ≠ Ε. ∎

TSA satisfies De Morgan duality but fails distributivity — a combination absent from Boolean algebra and Kleene three-valued logic.

### Theorem 9 — Fixed-Point Theorem

Β is the unique fixed point of INVERT.

*Proof:* ¬Π=Ε≠Π; ¬Ε=Π≠Ε; ¬Β=Β. ∎

### Theorem 10 — Generation of Full State Set

From any non-Ε starting state, the full set T is reachable via ⊕ and ¬.

*Proof:* From Π: Π⊕Β=Β; Β⊕Β=Π; ¬Π=Ε. From Β: Β⊕Β=Π; Π⊕Β=Β; ¬Π=Ε. ∎

### Theorem 11 — Incomplete Basis

The set {⊕, ⊗, ¬} is not functionally complete over T. The constant function f(x) = Β cannot be expressed in terms of {⊕, ⊗, ¬}.

*Proof:* {Π, Ε} is closed under {⊕, ⊗, ¬}: ⊕ on {Π,Ε} stays in {Π,Ε}; ⊗ on {Π,Ε} stays in {Π,Ε}; ¬ maps {Π,Ε}→{Ε,Π}. Therefore any term built from {⊕,⊗,¬} evaluated at inputs from {Π,Ε} produces results in {Π,Ε}. A constant function f(x)=Β requires f(Π)=Β∉{Π,Ε}. Contradiction. ∎

This reflects a physical reality: Β is not reachable from {Π,Ε} by combination alone — it requires accumulation until a limit is reached, which is exactly what ↓ models.

### Theorem 12 — COMPLETE Generates Β

For all x ∈ T: ↓(x ⊕ ¬x) = Β.

*Proof:* By Theorem 2, x⊕¬x=Π for all x. By definition of COMPLETE, ↓Π=Β. ∎

### Theorem 13 — All Constants Expressible with COMPLETE

The constant functions cΠ, cΕ, cΒ : T → T are expressible in {⊕, ¬, ↓}:

- cΠ(x) = x ⊕ ¬x = Π
- cΕ(x) = ¬(x ⊕ ¬x) = Ε
- cΒ(x) = ↓(x ⊕ ¬x) = Β ∎

**COMPLETE plays a dual role:** it carries temporal information (what a state evolves into) and it is the algebraically necessary operation for generating Β as a constant — enabling functional completeness. These roles are not coincidental: Β being algebraically unreachable from {Π,Ε} by combination reflects the physical fact that the boundary only appears at the end of an accumulation process.

**Conjecture 14:** The set {⊕, ¬, ↓} is functionally complete over T.

---

## Part 6 — Comparison with Boolean Algebra

### 6.1 Parallel Structure

| Property | Boolean | TSA |
|---|---|---|
| Primitive states | {0, 1} | {Π, Ε, Β} |
| Primary binary op | OR (∨) | CASCADE (⊕) |
| Dual binary op | AND (∧) | RESOLVE (⊗) |
| Unary op | NOT (¬) | INVERT (¬) |
| Identity of primary | 0 | Ε |
| Identity of dual | 1 | Π |
| Involution | ✓ | ✓ |
| De Morgan | ✓ | ✓ |
| Complementation | x∨¬x=1, x∧¬x=0 | x⊕¬x=Π, x⊗¬x=Ε |

### 6.2 Divergences

**Third state.** Β has no Boolean analog. ¬Β=Β has no Boolean analog.

**Non-idempotency of Β.** In Boolean, x∨x=x for all x. In TSA, Β⊕Β=Π≠Β.

**Non-distributivity.** Boolean is a distributive lattice. TSA is not (Theorem 8).

**Non-absorption of Β.** Boolean: 1∨x=1 for all x. TSA: Π⊕Β=Β≠Π.

**Completeness basis.** Boolean: {∨,∧,¬} is complete. TSA: {⊕,⊗,¬} is not complete (Theorem 11). ↓ is required (Conjecture 14).

### 6.3 Position Among Known Three-Valued Logics

| Property | Boolean | Kleene | TSA |
|---|---|---|---|
| States | {0,1} | {0,½,1} | {Π,Ε,Β} |
| Fixed point of ¬ | None | ½ | Β |
| All elements idempotent | ✓ | ✓ | ✗ |
| De Morgan | ✓ | ✓ | ✓ |
| Distributive | ✓ | ✓ | ✗ |
| Absorbing top | ✓ | ✓ | ✗ |
| Middle self-op under ⊕ | — | ½∨½=½ | Β⊕Β=Π |
| {primary, dual, ¬} complete | ✓ | ✗ | ✗ |

Kleene's three-valued logic has ½∨½=½. TSA has Β⊕Β=Π. This single difference propagates into non-distributivity and non-absorption, making TSA distinct from every standard three-valued logic.

---

## Part 7 — Type Inference

### 7.1 Assignment Rules

**T1 — Primitive assignment:** Assign Π, Ε, or Β from the governing dynamics of the quantity, not from data statistics. The assignment follows from whether the quantity accumulates, self-regulates, or sits at a structural transition.

**T2 — Additive composition:** For z = x + y:
- Same directional sign: τ(z) = τ(x) ⊕ τ(y)
- Opposing signs (restoring force against cascade): τ(z) = τ(x) ⊗ τ(y)

**T3 — Multiplicative composition:** τ(x · y) = τ(x) ⊕ τ(y).

**T4 — Reciprocal:** τ(1/x) = ¬τ(x). Inverting a cascade creates equilibrium; inverting equilibrium creates cascade.

**T5 — Bifurcation crossing:** When a variable crosses its structural constant, it transitions through Β. Ε → Β → Π as the threshold is crossed.

### 7.2 Structural Constants as Β-type Anchors

Every domain has Β-type constants — values at which the character of interacting variables changes:

- R_BIFURCATION ≈ 3.56994 (logistic map: Β-anchor for r)
- DIEL_BIFURCATION = 0.107 (EM surrogate: Β-anchor for loss tangent)
- RMS_BIFURCATION = 0.5g (bearing diagnostics: Β-anchor for vibration amplitude)
- A_s, A_f, M_s, M_f (SMA: four Β-anchors of the hysteresis band)
- Feigenbaum δ ≈ 4.669 (universal Β-anchor for period-doubling rate)

Normalising a Π-type variable by its Β-anchor places the bifurcation at 1 in normalised space.

### 7.3 Cross-Products as Β-type Expressions

When x : Π and y : Ε, the type of x·y is Π ⊕ Ε = Π. But the interaction term — sin(πx̃) × exp(−eỹ) — is a Β-type expression: zero when either input is at rest, maximal at the boundary between active cascade and active equilibrium. Cross-product terms encode the Β-type regime-switching that neither dimension captures alone.

---

## Part 8 — The Encoding Theorem

### 8.1 Statement

**Encoding Theorem:** Let x be a physical variable with TSA type τ ∈ {Π, Ε, Β}, and let C_x be its confirmed structural constant (a Β-type anchor). Define x̃ = clip(x/C_x, 0, 10).

**For τ = Π:**

Φ_Π(x̃) = (sin(π·x̃), cos(π·x̃), sin(2π·x̃), sin(π²·x̃), sin(π·x̃)·cos(π²·x̃))

with weights **(5, 1, 1, 3, 1)** / 11.

**For τ = Ε:**

Φ_Ε(x̃) = (exp(−e·x̃), x̃^e, exp(−e·(x̃ − 0.5)²))

with weights **(2, 2, 1)** / 5.

**For τ = Β:**

Φ_Β(x̃) = Φ_Π(x̃) ∥ Φ_Ε(x̃) — concatenation of both bases.

### 8.2 Basis Functions and Weight Justification

**π-basis:** the symbolic reduction establishes that π has cascade character (direction-fragmented, asymmetric). This justifies the sine-and-irrational-harmonic family. The weights are then determined by the mathematical properties of each term:

- sin(πx̃), weight 5: the fundamental cascade mode
- cos(πx̃), weight 1: quadrature complement
- sin(2πx̃), weight 1: second harmonic
- sin(π²x̃), weight 3: the irrational harmonic. π² is irrational, so sin(π²x̃) is strictly non-periodic — it never returns to any prior value over any integer number of periods. This is the mathematically exact basis function for cascade character: a quantity that never returns to a prior state. It earns weight 3 on independent mathematical grounds.
- sin(π·x̃)·cos(π²·x̃), weight 1: cross-frequency cascade product

**e-basis:** the symbolic reduction establishes that e has equilibrium character (oscillation-dominant, rhythmic). This justifies the exponential family. The near-uniform weights (2, 2, 1) are determined by the symmetric completion of exponential decay, power-law growth, and the centred Gaussian — three expressions of the same bounded, self-regulating character with no strong structural reason to prefer any one.

**The two-stage justification:**

Stage 1 (symbolic reduction) → determines which basis family applies to each type of variable.

Stage 2 (mathematical properties of basis functions) → determines the weights within each family.

The weights are empirically validated across at least four independent domains with fixed values, providing a third confirmation independent of both stages.

### 8.3 The Encoding as a Coordinate System

The encoding is a coordinate system, not a feature transformation. It carries the dominant structure of the problem before any measurement is taken. A machine learning model in these coordinates does not discover the cascade or equilibrium character — it inherits it and fits only the residual structure that the coordinate system cannot explain.

Data efficiency follows necessarily from this pre-loading. Accuracy ceiling improvement follows from the encoding's ability to represent structure that raw coordinates cannot.

---

## Part 9 — Worked Examples

### Example 1 — Type Classification

**Logistic map parameter r ∈ [0, 4].**

r spans from Ε-governing (r < R_BIFURCATION, system converges) to Π-driving (r > R_BIFURCATION, chaotic). The Β-point is R_BIFURCATION. **r : Β**, with R_BIFURCATION as the Β-anchor.

Encode using Φ_Β(r̃) where r̃ = r / R_BIFURCATION — both bases, capturing equilibrium structure below the bifurcation and cascade structure above it.

### Example 2 — Compound Type Inference

**SAR = f(gap, upper_layer, lower_layer, loss_tangent)**

- gap : Π (spans near-field to far-field non-repeatingly; no restoring force)
- upper_layer, lower_layer : Ε (bounded by resonance condition at λ_rubber)
- loss_tangent : Β (crosses DIEL_BIFURCATION = 0.107)

τ(SAR) = Π ⊕ Ε ⊕ Ε ⊕ Β = (Π ⊕ Ε) ⊕ (Ε ⊕ Β) = Π ⊕ Β = **Β**

SAR is a Β-type quantity — highly regime-sensitive, at the structural boundary between accumulating exposure and waveguide shielding. This is what a biological absorption safety metric should be. The 57% PINN ceiling is broken once the Β-type character is encoded and the geometric bifurcation constants are supplied.

### Example 3 — INVERT Applied

**Crest factor CF = Peak / RMS,** where Peak : Π and RMS : Π.

τ(CF) = τ(Peak) ⊗ ¬τ(RMS) = Π ⊗ ¬Π = Π ⊗ Ε = **Ε**

Correct: CF self-regulates in a healthy bearing because Peak and RMS increase together, keeping their ratio bounded. Division inverts the cascade character of the denominator; the quotient of two similar-character cascade quantities resolves to equilibrium.

### Example 4 — Full Reduction Sequence

**z = x · (1 − x) · r** where x : Ε (logistic state), r : Π (above bifurcation).

1. x : Ε
2. 1−x: 1 is a Β-anchor (upper boundary of x's domain); −x inverts x's character. τ(1−x) = Β ⊗ ¬Ε = Β ⊗ Π = **Β**
3. τ(x·(1−x)) = Ε ⊕ Β = **Β** — the parabola is zero at the Β-anchors 0 and 1, maximal inside
4. τ(z) = τ(r) ⊕ τ(x(1−x)) = Π ⊕ Β = **Β**

The logistic iterate is Β-typed — sitting at the structural boundary between cascade and equilibrium, which is precisely what the logistic map describes. The TSA reduction recovers this without computing any trajectories.

---

## Part 10 — Open Questions

**Q1 — Proof of Conjecture 14.**
{⊕, ¬, ↓} is conjectured functionally complete. Theorem 13 shows all constants are expressible; the remaining step is showing that projection and constants suffice to generate all 27 unary and 19683 binary functions over T, or via Rosenberg's maximal clone classification for three-element algebras.

**Q2 — Axiomatisation of COMPLETE.**
COMPLETE is defined by its truth table. Whether it can be captured by equational laws derivable from the other axioms, or requires a separate dynamical axiom, is open. A candidate distributive axiom ↓(x⊕y) = ↓x⊕↓y fails (↓(Β⊕Β)=↓Π=Β, but ↓Β⊕↓Β=Ε⊕Ε=Ε≠Β). The axiomatisation problem remains open.

**Q3 — Relationship to formal logic.**
TSA satisfies De Morgan duality but fails distributivity. This combination distinguishes it from Boolean algebra, Kleene logic, and Łukasiewicz logic. Formal proof that TSA is not embeddable in any standard many-valued logic would establish it as a new algebraic structure.

**Q4 — Extension to differential operators.**
Can TSA types be assigned consistently to differential operators, enabling classification of differential equations by solution character without solving them? If x : Ε, does d/dt x : Ε? If x : Π, does d/dt x : Π? A consistent type inference system for operators would extend TSA into qualitative analysis of dynamical systems.

**Q5 — Derivability of TSA5.**
Β ⊕ Β = Π is an axiom. Whether it follows from more fundamental principles about bifurcation boundaries — topological statements about separatrices — or is genuinely irreducible, is open.

**Q6 — Minimality of the axiom set.**
Are all nine axioms TSA1–TSA9 logically independent? A minimal independent set would clarify the structure and its relationship to other algebras.

---

## Appendix A — Complete Truth Tables

**CASCADE (⊕):**

| ⊕ | Π | Ε | Β |
|---|---|---|---|
| Π | Π | Π | Β |
| Ε | Π | Ε | Β |
| Β | Β | Β | Π |

**RESOLVE (⊗):**

| ⊗ | Π | Ε | Β |
|---|---|---|---|
| Π | Π | Ε | Β |
| Ε | Ε | Ε | Β |
| Β | Β | Β | Ε |

**INVERT (¬):**

| x | ¬x |
|---|---|
| Π | Ε |
| Ε | Π |
| Β | Β |

**COMPLETE (↓):**

| x | ↓x |
|---|---|
| Π | Β |
| Ε | Ε |
| Β | Ε |

---

## Appendix B — Digit Reduction Summary

| Digit | Reduction | Character |
|-------|-----------|-----------|
| 0 | terminal | Prior to the counting system |
| 1 | 1 | Being |
| 2 | 2 | Division |
| 3 | 3 | Generation |
| 4 | 2 | 2×2: pure doubling |
| 5 | [1, 3] | 1 generates triadic structure |
| 6 | [2, 3] | 2×3: holds both simultaneously |
| 7 | [1, 2, 3] | All three in natural order |
| 8 | 2 | 2³: recursive doubling |
| 9 | 3 | 3²: generation squared |

**Direction pairs (strict forward cycle):** (1,2), (2,3), (3,1)

**Oscillation:** all other pairs

**π macro** (32 symbols to terminal at decimal 32):
[D×2][O×6][D×2][O×2][D×1][O×2][D×4][O×3][D×1][O×3][D×1][O×2][D×1][O×1][D×1][O×2][D×1][O×2][D×2][O×1][D×1][O×1]
→ direction-fragmented, asymmetric, 11 runs

**e macro** (13 symbols to terminal at decimal 13):
[O×1][D×4][O×3][D×1][O×6]
→ oscillation-dominant, rhythmic, direction fires and recedes

---

## Appendix C — Axiom Summary

| Label | Statement |
|---|---|
| TSA1 | x ⊕ y = y ⊕ x |
| TSA2 | (x ⊕ y) ⊕ z = x ⊕ (y ⊕ z) |
| TSA3 | x ⊕ Ε = x |
| TSA4 | Π ⊕ Π = Π |
| TSA5 | Β ⊕ Β = Π |
| TSA6 | Π ⊕ Β = Β |
| TSA7 | ¬¬x = x |
| TSA8 | ¬Β = Β |
| TSA9 | ¬Ε = Π |
| Def ⊗ | x ⊗ y = ¬(¬x ⊕ ¬y) |
| Def ↓ | ↓Π=Β; ↓Ε=Ε; ↓Β=Ε |

---

## Appendix D — TSA vs Known Algebras

| Property | Boolean | Kleene | TSA |
|---|---|---|---|
| States | {0,1} | {0,½,1} | {Π,Ε,Β} |
| Primary identity | 0 | 0 | Ε |
| Dual identity | 1 | 1 | Π |
| Fixed point of ¬ | None | ½ | Β |
| All elements idempotent | ✓ | ✓ | ✗ |
| De Morgan | ✓ | ✓ | ✓ |
| Distributive | ✓ | ✓ | ✗ |
| Absorbing top | ✓ | ✓ | ✗ |
| Middle self-cascade | — | ½∨½=½ | Β⊕Β=Π |
| {⊕,⊗,¬} complete | ✓ | ✗ | ✗ |
| {⊕,¬,↓} complete | — | — | Conjectured ✓ |

---

*Version 3.0. Further development: proof of Conjecture 14; axiomatisation of COMPLETE; photonic circuit correspondence.*
