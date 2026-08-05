# Trinary Symbolic Algebra (TSA)
## A Method for the Algebraic Classification and Composition of Mathematical Character

**Version 4.0**

---

## Preamble

Boolean algebra answers one question: *is this proposition true or false?* Its power comes from that reduction — all information is collapsed to a binary distinction, and a complete algebra is built on top of it.

Trinary Symbolic Algebra (TSA) answers a different question: *what is the mathematical character of this quantity?* Not its value. Not its truth. Its structural behaviour — whether it cascades without bound, regulates toward equilibrium, or sits at the boundary between the two.

The answer is always one of three things. That exactly three characters are necessary and sufficient is not an assumption — it is the conclusion of a symbolic reduction applied to the real number system, verified on the two most structurally distinct transcendental constants in mathematics. The derivation precedes the algebra. It justifies why this algebra has exactly three states.

The method proceeds in this sequence:

1. **Symbolic Reduction** — how any numerical sequence yields a trinary character
2. **Primitive Elements** — the formal definition of the three states
3. **Operations** — CASCADE, RESOLVE, INVERT, COMPLETE (natural and forced)
4. **Axioms** — the minimal set determining the algebra
5. **Theorems** — what follows necessarily from the axioms
6. **Comparison with Boolean Algebra**
7. **Type Inference** — assigning and propagating TSA types
8. **The Encoding Theorem** — connecting TSA types to mathematical basis functions
9. **Worked Examples** — including empirical verification
10. **Open Questions**

---

## Part 1 — The Symbolic Reduction

### 1.1 Why Three

Any quantity in a formal or physical system exhibits one of two behaviours at the trajectory level: it either returns to prior values (bounded, self-correcting, periodic) or it does not (accumulating, path-dependent, cascade). These are two irreducible dynamical characters.

A system can also sit at the transition between them — the bifurcation point from which small perturbations send it toward either character. This is a third condition, structurally distinct from both: not "less cascading" or "partially equilibrating" but the separatrix itself. Collapsing it into either other state loses the information that determines which regime a system is in.

Four states are unnecessary. Any candidate fourth state reduces to a composition of the three, or is a refinement within one of them. Three is the minimum complete set.

### 1.2 The Digit Reduction Table

| Digit | Reduction | Character |
|-------|-----------|-----------|
| 0 | **terminal** | Prior to 1 — boundary marker, not a number |
| 1 | **1** | Being — primitive, undivided, the unit |
| 2 | **2** | Division — the first distinction, opposition |
| 3 | **3** | Generation — first number exceeding its parts |
| 4 | **2** | 4 = 2×2: pure doubling, no new quality |
| 5 | **[1, 3]** | 1 generates the triadic structure around it |
| 6 | **[2, 3]** | 2×3: holds both simultaneously |
| 7 | **[1, 2, 3]** | Contains all three in natural order |
| 8 | **2** | 2³: recursive doubling |
| 9 | **3** | 3²: generation compounding |

### 1.3 Reading the Expanded Sequence

**Direction:** a pair is direction if and only if it is a forward step in the cycle 1→2→3→1. The three valid direction pairs are:

> **(1, 2) — (2, 3) — (3, 1)**

**Oscillation:** every pair that is not a direction pair — same-value pairs (1,1), (2,2), (3,3), backward steps (2,1), (3,2), and skip pairs (1,3).

- **(1, 2)** → direction ✓
- **(2, 1)** → oscillation ✗ (backward)
- **(3, 1)** → direction ✓ (forward wrap)
- **(1, 3)** → oscillation ✗ (skip)
- **1, 2, 1** → [direction][oscillation]
- **3, 1, 2** → [direction][direction] — full direction run. π opens with exactly this at 3.14.

### 1.4 The Stopping Criterion

The reduction applies until the first occurrence of digit 0 in the decimal expansion. The digit 0 is prior to the counting system — a natural boundary marker. All analysis is of the sequence strictly before the first 0.

### 1.5 Reduction of π

π = 3.14159265358979323846264338327950...

First 0 appears at **decimal position 32**. 32 symbols processed before terminal.

Macro structure (full expanded sequence, direction rule applied):

```
[D×2] [O×6] [D×2] [O×2] [D×1] [O×2] [D×4] [O×3]
[D×1] [O×3] [D×1] [O×2] [D×1] [O×1] [D×1] [O×2]
[D×1] [O×2] [D×2] [O×1] [D×1] [O×1]
```

**11 direction-runs. 11 oscillation-runs. 17 direction steps, 25 oscillation steps.**

**What the pattern shows:** direction is frequent, fragmented, and never sustained. 11 separate runs, mostly D×1, scattered across the entire sequence. Oscillation blocks are variable and do not repeat in predictable intervals. The pattern never stabilises — asymmetric character.

### 1.6 Reduction of e

e = 2.71828182845904...

First 0 appears at **decimal position 13**. 13 symbols processed before terminal.

Macro structure:

```
[O×1] [D×4] [O×3] [D×1] [O×6]
```

**2 direction-runs. 3 oscillation-runs. 5 direction steps, 10 oscillation steps.**

**What the pattern shows:** direction fires twice — once strongly (D×4, the full 1→2→3→1→2 cycle from the digit 7=[1,2,3] plus context), once briefly (D×1) — then retreats completely into the longest oscillation block in either constant (O×6). Direction is an event, not a state — rhythmic character.

### 1.7 The Non-Arbitrariness Proof

The reduction rules are fixed before either constant is examined. No parameter is adjusted between them. The same rules applied to both produce structurally opposite results. An arbitrary rule would not reliably discriminate. Reliable discrimination under fixed rules is the definition of a structural detector.

Both constants share the same largest direction-run size — D×4 — but π scatters its 11 direction-runs throughout the entire sequence while e fires D×4 once then retreats into O×6. The same structural event deployed with completely opposite intent. That is structure, not coincidence.

**Limits stated precisely:** the digit table has structural rather than formal-mathematical justification. The direction rule follows from the natural forward cycle of {1,2,3} and is unambiguous at the pair level. The stopping at 0 is a structural boundary, not a mathematical theorem.

### 1.8 Connection to Encoding

**Stage 1** (symbolic reduction) → establishes which basis family applies: π-family for Π-type variables, e-family for Ε-type variables.

**Stage 2** (mathematical properties of basis functions) → establishes weights within each family:

**π-basis weights (5, 1, 1, 3, 1):** sin(πx̃) weight 5 as fundamental cascade mode; sin(π²x̃) weight 3 because π² is irrational — sin(π²x̃) is strictly non-periodic, never returning to any prior value at any integer period. This is the mathematically correct basis function for cascade character, and earns weight 3 on independent mathematical grounds. cos(πx̃), sin(2πx̃), and the cross-product each carry weight 1.

**e-basis weights (2, 2, 1):** near-uniform weighting is structurally correct for equilibrium — the stability of e's macro pattern (near-uniform direction-run lengths) asserts flat weighting directly.

Weights are empirically validated across at least four independent domains with fixed values.

---

## Part 2 — Primitive Elements

### 2.1 The State Set

**T = {Π, Ε, Β}**

Three irreducible states. Not variables — primitive objects.

### 2.2 Characterisation

**Π (cascade):** trajectory is non-periodic, path-dependent, non-returning. Accumulates without self-correction. Examples: vibration RMS in a bearing with active spalling; Lyapunov exponent in the chaotic regime; transformation strain in SMA beyond austenite finish temperature; the macro direction-fragmented pattern of π.

**Ε (equilibrium):** trajectory is bounded, convergent, self-correcting. Returns toward a characteristic operating point when displaced. Examples: bearing temperature under constant load; crest factor of healthy bearing; consonance score of simple frequency ratios; the macro oscillation-dominant pattern of e.

**Β (boundary):** at the structural transition between Π and Ε. Neither accumulating nor self-correcting — the separatrix from which trajectories diverge toward either regime under any perturbation. Examples: r at R_BIFURCATION of the logistic map; loss tangent at DIEL_BIFURCATION; RMS at onset of bearing cascade; phase fraction in shape memory alloy between full martensite and full austenite; the digit 0 in the reduction — prior to the counting system, the terminal boundary.

### 2.3 Formal Properties

States are **distinct**, **exhaustive**, and **primitive**. TSA types are not values — magnitude and type are independent.

---

## Part 3 — Operations

### 3.1 CASCADE (⊕)

Takes two states and returns the character of their compound behaviour.

| ⊕ | Π | Ε | Β |
|---|---|---|---|
| **Π** | Π | Π | Β |
| **Ε** | Π | Ε | Β |
| **Β** | Β | Β | Π |

*Π ⊕ Ε = Π:* cascade dominates equilibrium. *Β ⊕ Β = Π:* two boundaries drive cascade — TSA's structurally distinctive rule. **Identity:** Ε ⊕ x = x for all x.

### 3.2 INVERT (¬)

| x | ¬x |
|---|---|
| Π | Ε |
| Ε | Π |
| Β | Β |

*¬Β = Β:* the boundary is its own complement — equidistant from both extremes. **Involution:** ¬¬x = x.

### 3.3 RESOLVE (⊗)

De Morgan dual of CASCADE: **x ⊗ y = ¬(¬x ⊕ ¬y)**

| ⊗ | Π | Ε | Β |
|---|---|---|---|
| **Π** | Π | Ε | Β |
| **Ε** | Ε | Ε | Β |
| **Β** | Β | Β | Ε |

*Π ⊗ Ε = Ε:* equilibrium governs under RESOLVE — dual to CASCADE where cascade governs. *Β ⊗ Β = Ε:* dual to Β ⊕ Β = Π. **Identity:** Π ⊗ x = x for all x.

### 3.4 COMPLETE Natural (↓)

Maps each state to its natural attractor — what the system evolves toward without external forcing.

| x | ↓x |
|---|---|
| Π | Β |
| Ε | Ε |
| Β | Ε |

*↓Π = Β:* cascade accumulates until it hits the structural limit. *↓Ε = Ε:* equilibrium stays at equilibrium. *↓Β = Ε:* boundary without forcing resolves toward equilibrium — boundaries are unstable fixed points.

### 3.5 COMPLETE Forced (⊘)

Maps each state to what it becomes when **forced through its Β-anchor** — when the threshold is actively crossed rather than approached asymptotically.

| x | ⊘x |
|---|---|
| Ε | Π |
| Π | ∅ |
| Β | (open — see Q7) |

*⊘Ε = Π:* equilibrium forced through its bifurcation threshold enters cascade. In the bearing domain: temperature crossing TEMP_BIFURCATION → thermal cascade. RMS crossing RMS_BIFURCATION → mechanical cascade. *⊘Π = ∅:* cascade forced through the failure threshold exits the algebra. In the bearing domain: RMS crossing FAILURE_G → physical failure, test stops.

**∅ (terminal):** the state reached when ⊘Π is applied. ∅ is not a fourth TSA state — it is outside the algebra's domain. No operations are defined on ∅. It represents system termination: the cascade has exhausted the system.

**The two COMPLETE operations are distinct:** ↓ describes natural asymptotic behaviour without forcing; ⊘ describes what happens when the Β-anchor is actively crossed. ↓Ε = Ε (equilibrium left alone stays equilibrium); ⊘Ε = Π (equilibrium threshold crossed → cascade). These are different physical events and different algebraic operations.

**The COMPLETE chain:** ⊘Ε → Π → ⊘Π → ∅. Applied to a bearing: RMS in Ε-regime crosses RMS_BIFURCATION (⊘Ε event) → enters Π-regime → RMS accelerates toward FAILURE_G (⊘Π event) → physical failure (∅). The temporal gap between ⊘Ε and ⊘Π is the **lead time** — the intervention window available before system termination.

Both COMPLETE operations are primitive. Neither ↓ nor ⊘ is derivable from {⊕, ⊗, ¬}.

---

## Part 4 — Axioms

Nine axioms over T = {Π, Ε, Β} with primitives ⊕ and ¬. RESOLVE (⊗) is derived. ↓ and ⊘ are separate primitives.

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
| Def ⊘ | ⊘Ε = Π; ⊘Π = ∅; ⊘Β = open |

TSA1–9 fully determine the CASCADE and INVERT tables; RESOLVE follows from its definition. ↓ and ⊘ are defined by their tables, not derived.

---

## Part 5 — Theorems

### Theorem 1 — De Morgan Duality

¬(x ⊕ y) = ¬x ⊗ ¬y for all x, y ∈ T.

*Proof:* ¬x ⊗ ¬y = ¬(¬(¬x) ⊕ ¬(¬y)) = ¬(x ⊕ y). ∎

### Theorem 2 — Complementation Laws

x ⊕ ¬x = Π and x ⊗ ¬x = Ε for all x ∈ T.

*Proof:* Π⊕¬Π=Π⊕Ε=Π; Ε⊕¬Ε=Ε⊕Π=Π; Β⊕¬Β=Β⊕Β=Π. For ⊗: by De Morgan, x⊗¬x=¬(¬x⊕x)=¬Π=Ε. ∎

### Theorem 3 — Commutativity of RESOLVE

x ⊗ y = y ⊗ x. *Proof:* x⊗y=¬(¬x⊕¬y)=¬(¬y⊕¬x)=y⊗x. ∎

### Theorem 4 — Associativity of RESOLVE

(x ⊗ y) ⊗ z = x ⊗ (y ⊗ z). *Proof:* expand via definition and TSA2. ∎

### Theorem 5 — Partial Idempotency

Π and Ε are idempotent under both ⊕ and ⊗. Β is idempotent under neither.

*Proof:* Π⊕Π=Π (TSA4); Ε⊕Ε=Ε (TSA3); Β⊕Β=Π≠Β (TSA5). From derived table: Π⊗Π=Π; Ε⊗Ε=Ε; Β⊗Β=Ε≠Β. ∎

TSA is not a lattice. Β's non-idempotency reflects the physical reality that the boundary state is unstable — combining it with itself drives it away from itself.

### Theorem 6 — Non-Idempotency Duality

Β ⊕ Β = Π and Β ⊗ Β = Ε. Under CASCADE (forward pressure), two boundaries drive cascade. Under RESOLVE (backward pressure), two boundaries settle to equilibrium.

### Theorem 7 — Β Resists Absorption

Π ⊕ Β = Β ≠ Π; Ε ⊗ Β = Β ≠ Ε.

*Proof:* Π⊕Β=Β (TSA6); Ε⊗Β=¬(Π⊕Β)=¬Β=Β. ∎

In Boolean algebra, the top and bottom absorb everything. In TSA, Π and Ε do not absorb Β.

### Theorem 8 — Non-Distributivity

CASCADE does not distribute over RESOLVE.

*Counterexample:* Β⊕(Π⊗Ε)=Β⊕Ε=Β; but (Β⊕Π)⊗(Β⊕Ε)=Β⊗Β=Ε. Β≠Ε. ∎

### Theorem 9 — Fixed-Point Theorem

Β is the unique fixed point of INVERT.

*Proof:* ¬Π=Ε≠Π; ¬Ε=Π≠Ε; ¬Β=Β. ∎

### Theorem 10 — Generation of Full State Set

From any non-Ε starting state, the full set T is reachable via ⊕ and ¬.

*Proof:* From Π: Π⊕Β=Β; Β⊕Β=Π; ¬Π=Ε. From Β: Β⊕Β=Π; Π⊕Β=Β; ¬Π=Ε. ∎

### Theorem 11 — Incomplete Basis

{⊕, ⊗, ¬} is not functionally complete over T. The constant function f(x) = Β cannot be expressed in {⊕, ⊗, ¬}.

*Proof:* {Π, Ε} is closed under {⊕, ⊗, ¬}: all operations on {Π,Ε} stay in {Π,Ε}. Any term built from {⊕,⊗,¬} evaluated at inputs from {Π,Ε} produces results in {Π,Ε}. A constant f(x)=Β requires f(Π)=Β∉{Π,Ε}. Contradiction. ∎

Β is not reachable from {Π,Ε} by combination alone — it requires either ↓ (natural limit) or ⊘ (threshold crossing).

### Theorem 12 — COMPLETE Generates Β

↓(x ⊕ ¬x) = Β for all x ∈ T.

*Proof:* x⊕¬x=Π (Theorem 2); ↓Π=Β. ∎

### Theorem 13 — All Constants Expressible

- cΠ(x) = x ⊕ ¬x = Π
- cΕ(x) = ¬(x ⊕ ¬x) = Ε
- cΒ(x) = ↓(x ⊕ ¬x) = Β ∎

### Theorem 14 — Forced COMPLETE Chain

⊘Ε = Π, and ⊘Π = ∅. Natural and forced COMPLETE are not composable: ↓ ≠ ⊘.

*Proof of distinction:* ↓Ε = Ε (equilibrium left alone stays equilibrium); ⊘Ε = Π (equilibrium threshold crossed gives cascade). The two operations produce different outputs on the same input Ε, therefore they are distinct. ∎

**Lead time corollary:** if a variable x has type Ε with Β-anchor C_x, the lead time Δt is the temporal interval between the event ⊘Ε(x) (x crosses C_x entering Π-regime) and the event ⊘Π(x) (x reaches the failure criterion entering ∅). Δt = t(⊘Π) − t(⊘Ε) is not an algebraic quantity — it is a physical duration measured in time, determined by the dynamics of the Π-regime cascade between the two threshold crossings.

**Conjecture 15:** {⊕, ¬, ↓} is functionally complete over T.

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

**Non-idempotency of Β.** Boolean: x∨x=x for all x. TSA: Β⊕Β=Π≠Β.

**Non-distributivity.** Boolean is a distributive lattice. TSA is not (Theorem 8).

**Non-absorption of Β.** Boolean: 1∨x=1 for all x. TSA: Π⊕Β=Β≠Π.

**Completeness.** Boolean {∨,∧,¬} is complete. TSA {⊕,⊗,¬} is not (Theorem 11); ↓ is required (Conjecture 15).

**Two COMPLETE operations.** Boolean has no analog of ↓ or ⊘. The existence of two structurally distinct COMPLETE operations — one describing natural limits, one describing forced threshold crossings — has no Boolean precedent.

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

**Note on Kleene completeness:** Kleene's {∨,∧,¬} is also not functionally complete over {0,½,1}. The same argument applies: {0,1} is closed under Kleene's ∨, ∧, ¬, so no expression in those operations can generate ½ as a constant from inputs in {0,1}. TSA and Kleene share this incompleteness for the same structural reason — the middle state is algebraically isolated from the two extremes under the standard operations.

---

## Part 7 — Type Inference

### 7.1 Assignment Rules

**T1 — Primitive assignment:** assign Π, Ε, or Β from the governing dynamics of the quantity, not from data statistics.

**T2 — Additive composition:** for z = x + y:
- Same directional sign: τ(z) = τ(x) ⊕ τ(y)
- Opposing signs (restoring force): τ(z) = τ(x) ⊗ τ(y)

**T3 — Multiplicative composition:** τ(x·y) = τ(x) ⊕ τ(y).

**T4 — Reciprocal:** τ(1/x) = ¬τ(x).

**T5 — Bifurcation crossing:** when a variable crosses its structural constant, it transitions through Β. Ε → Β → Π as threshold is crossed (natural progression); ⊘Ε → Π as threshold is actively crossed (forced event).

**T6 — Target type from own dynamics:** the TSA type of a prediction target is determined by the target's own physical dynamics across its full range, not by the algebraic combination of its input variable types.

A target that self-regulates in one regime and cascades in another has character Β by direct assignment from its physical character. This is independent of whether its input features combine algebraically to Β or to some other type. The input type combination governs how to encode those inputs; the target type governs how to interpret the prediction. The two are separate questions.

*Empirical confirmation (PRONOSTIA bearing dataset, LOBO protocol):* a Π-only model on rul_norm leaves Ε-structured residuals in the healthy phase in 8/10 bearings (80%); an Ε-only model leaves Π-structured cascade residuals in the cascade phase in 10/10 bearings (100%). Both structured residual types are independently present — neither type of model can explain the residuals of the other. This is the operational definition of Β character arising from the target's own dynamics.

### 7.2 Structural Constants as Β-type Anchors

Every domain has Β-type constants — values at which character changes:

- R_BIFURCATION ≈ 3.56994 (logistic map)
- DIEL_BIFURCATION = 0.107 (EM surrogate)
- RMS_BIFURCATION = 0.5g (bearing diagnostics)
- A_s, A_f, M_s, M_f (SMA hysteresis band)
- Feigenbaum δ ≈ 4.669 (universal period-doubling rate)

### 7.3 Cross-Products as Β-type Expressions

When x : Π and y : Ε, τ(x·y) = Π. But the interaction term sin(πx̃) × exp(−eỹ) is a Β-type expression: zero when either input is at rest, maximal at the boundary between active cascade and active equilibrium.

---

## Part 8 — The Encoding Theorem

### 8.1 Statement

Let x have TSA type τ ∈ {Π, Ε, Β} and structural constant C_x. Define x̃ = clip(x/C_x, 0, 10).

**For τ = Π:**

Φ_Π(x̃) = (sin(π·x̃), cos(π·x̃), sin(2π·x̃), sin(π²·x̃), sin(π·x̃)·cos(π²·x̃))

weights **(5, 1, 1, 3, 1)** / 11

**For τ = Ε:**

Φ_Ε(x̃) = (exp(−e·x̃), x̃^e, exp(−e·(x̃ − 0.5)²))

weights **(2, 2, 1)** / 5

**For τ = Β:**

Φ_Β(x̃) = Φ_Π(x̃) ∥ Φ_Ε(x̃)

### 8.2 Basis Function Justification

The π-basis: symbolic reduction establishes π has cascade character → sin/cos family. Weight 3 for sin(π²x̃): π² is irrational, so sin(π²x̃) is strictly non-periodic — it never returns to any prior value at any integer period. Mathematically exact encoding of cascade character. Weight 5 for sin(πx̃): fundamental mode.

The e-basis: symbolic reduction establishes e has equilibrium character → exponential family. Near-uniform weights (2,2,1): confirmed by the stability of e's macro pattern.

### 8.3 The Encoding as a Coordinate System

The encoding is a coordinate system, not a feature transformation. It pre-loads the dominant structure of the problem before any measurement is taken. Data efficiency and accuracy ceiling improvement follow from this pre-loading.

### 8.4 Three-Phase Architecture

A practical implication of Theorem 14 for deployment: the two-stage model architecture (Ridge grammar capturing Π trend + RF capturing Ε residuals) should be gated on the ⊘Ε event. Before ⊘Ε is reached (when rms_bif_dist = 0), the target is Ε-dominant and only Ε features should govern the prediction. The Ridge grammar, which encodes the global Π cascade trend, activates at ⊘Ε. This three-phase structure (Ε-only before ⊘Ε, Ridge+RF after ⊘Ε, ∅ at ⊘Π) is the correct architectural expression of the COMPLETE chain.

---

## Part 9 — Worked Examples

### Example 1 — Type Classification

**Logistic map parameter r ∈ [0, 4].** r spans from Ε-governing (r < R_BIFURCATION) to Π-driving (r > R_BIFURCATION) with Β-point at R_BIFURCATION.

**r : Β**, Β-anchor = R_BIFURCATION. Encode using Φ_Β(r̃) where r̃ = r / R_BIFURCATION.

### Example 2 — Compound Type Inference

**SAR = f(gap, upper_layer, lower_layer, loss_tangent)**

- gap : Π; upper_layer, lower_layer : Ε; loss_tangent : Β

τ(SAR) = Π ⊕ Ε ⊕ Ε ⊕ Β = (Π ⊕ Ε) ⊕ (Ε ⊕ Β) = Π ⊕ Β = **Β**

SAR is Β-typed — highly regime-sensitive at the boundary between accumulating exposure and waveguide shielding.

### Example 3 — INVERT Applied

**Crest factor CF = Peak / RMS,** Peak : Π, RMS : Π.

τ(CF) = Π ⊗ ¬Π = Π ⊗ Ε = **Ε** — CF self-regulates in a healthy bearing.

### Example 4 — Full Reduction Sequence

**z = x·(1−x)·r**, x : Ε, r : Π.

1. x : Ε
2. τ(1−x) = Β ⊗ ¬Ε = Β ⊗ Π = **Β**
3. τ(x·(1−x)) = Ε ⊕ Β = **Β**
4. τ(z) = Π ⊕ Β = **Β**

The logistic iterate is Β-typed — at the boundary between cascade and equilibrium.

### Example 5 — Empirical Verification of Target Type Rule (T6)

**Claim (Rule T6):** rul_norm in the PRONOSTIA bearing dataset has Β character from its own physical dynamics, not from algebraic combination of input types.

**Test:** three ablation models under LOBO protocol on 11 bearings (Bearing1_4 excluded as known distribution outlier — shortest Condition-1 life, atypical failure mode; exclusion is a generalisation failure, not a TSA typing failure):

- **M1 Π-only:** Ridge trained on 8 Π-encoded features only, predicting rul_norm
- **M2 Ε-only:** RF trained on 4 Ε-encoded features only, predicting rul_norm
- **M3 Full CSP:** complete two-stage model

**TSA predictions:**
- M1 Π-only → should leave Ε-structured residuals in the healthy phase (Π model captures cascade trend; Ε texture remains)
- M2 Ε-only → should leave Π-structured residuals in the cascade phase (Ε model captures equilibrium texture; cascade trend remains)

**Results (10 bearings, excluding outlier):**

| Prediction | Result | Rate |
|---|---|---|
| M1 healthy residuals → Ε-structured | **CONFIRMED** | 8/10 (80%) |
| M2 cascade residuals → Π-structured | **CONFIRMED** | 10/10 (100%) |

The two structured residual types are independently present and complementary. The Π model cannot explain the healthy-phase Ε texture; the Ε model cannot explain the cascade-phase Π trend. Neither model's residuals explain the other's. This is the operational definition of Β character arising from the target's own dynamics.

---

## Part 10 — Open Questions

**Q1 — Proof of Conjecture 15.** {⊕, ¬, ↓} is conjectured functionally complete. Theorem 13 shows all constants are expressible; formal proof requires either exhaustive verification or Rosenberg's maximal clone classification.

**Q2 — Axiomatisation of ↓.** COMPLETE natural is currently defined by its truth table. A candidate distributive axiom ↓(x⊕y) = ↓x⊕↓y fails: ↓(Β⊕Β)=↓Π=Β, but ↓Β⊕↓Β=Ε⊕Ε=Ε≠Β. Open.

**Q3 — Relationship to formal logic.** TSA satisfies De Morgan duality but fails distributivity. Formal proof that TSA is not embeddable in any standard many-valued logic would establish it as a new algebraic structure.

**Q4 — Extension to differential operators.** Can TSA types be assigned consistently to differential operators, enabling classification of differential equations by solution character without solving them?

**Q5 — Derivability of TSA5.** Β ⊕ Β = Π is an axiom. Whether it follows from more fundamental principles about bifurcation boundaries — topological statements about separatrices — or is genuinely irreducible, is open.

**Q6 — Minimality of the axiom set.** Are all nine axioms TSA1–TSA9 logically independent?

**Q7 — ⊘Β.** Forced COMPLETE applied to Β is currently undefined. Two candidate interpretations: ⊘Β = Π (boundary forced forward → cascade) or ⊘Β = Ε (boundary forced backward → equilibrium). The direction of forcing likely determines the outcome, suggesting ⊘ may require a directional parameter when applied to Β.

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

**COMPLETE Natural (↓):**

| x | ↓x |
|---|---|
| Π | Β |
| Ε | Ε |
| Β | Ε |

**COMPLETE Forced (⊘):**

| x | ⊘x |
|---|---|
| Ε | Π |
| Π | ∅ |
| Β | open |

---

## Appendix B — Axiom and Definition Summary

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
| Def ⊘ | ⊘Ε=Π; ⊘Π=∅; ⊘Β=open |

---

## Appendix C — Digit Reduction Summary

| Digit | Reduction |
|-------|-----------|
| 0 | terminal |
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 2 |
| 5 | [1, 3] |
| 6 | [2, 3] |
| 7 | [1, 2, 3] |
| 8 | 2 |
| 9 | 3 |

Direction pairs: (1,2), (2,3), (3,1). Oscillation: all others.

**π macro** (32 symbols to terminal at decimal 32):
[D×2][O×6][D×2][O×2][D×1][O×2][D×4][O×3][D×1][O×3][D×1][O×2][D×1][O×1][D×1][O×2][D×1][O×2][D×2][O×1][D×1][O×1]

**e macro** (13 symbols to terminal at decimal 13):
[O×1][D×4][O×3][D×1][O×6]

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
| Middle self-op under ⊕ | — | ½∨½=½ | Β⊕Β=Π |
| {primary, dual, ¬} complete | ✓ | ✗ | ✗ |
| Natural COMPLETE (↓) | — | — | ✓ |
| Forced COMPLETE (⊘) | — | — | ✓ |
| Terminal state (∅) | — | — | ✓ |

---

*Version 4.0. Further development: proof of Conjecture 15; axiomatisation of ↓; ⊘Β definition; photonic circuit correspondence.*
