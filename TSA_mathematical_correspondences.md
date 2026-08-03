# Trinary Symbolic Algebra — Mathematical Correspondences

A companion to the TSA methodology document (v3). Each section states an established mathematical result, maps it onto TSA, and notes what the correspondence confirms or illuminates. Connections are graded: **exact** (the mapping is precise and provable), **structural** (the mapping holds at the level of classification), or **suggestive** (the parallel is meaningful but requires further formalisation).

---

## 1. Thales' Circle Theorem [exact]

**The theorem:** If AC is a diameter of a circle and B is any point on the circle distinct from A and C, then angle ABC = 90°.

**TSA mapping:**

The circle is the Β-manifold — the set of all points equidistant from the centre. Points strictly inside the circle are bounded and contained (Ε-type). Points strictly outside are unbounded relative to the enclosure (Π-type). Points on the circle itself are at the structural boundary (Β-type).

Thales' theorem states that any point in the Β-condition (on the boundary) produces exactly 90° — the unique angle that is its own complement. In TSA: the unique state whose complement is itself is Β, satisfying ¬Β = Β (Theorem 9, Fixed-Point Theorem). The right angle is the geometric expression of self-complementarity.

Concretely: an angle less than 90° would place B inside the circle (Ε-regime); greater than 90° would place B outside (Π-regime). Exactly 90° is the Β-condition — neither less nor greater, self-complementary. The theorem is a geometric proof that the Β-condition uniquely determines self-complementarity.

**What this confirms:** Theorem 9 (¬Β = Β) has a classical geometric precedent in Thales. The self-complementarity of the boundary state is not a construction of TSA — it is a feature of boundary conditions in Euclidean geometry.

---

## 2. Thales' Intercept Theorem [structural]

**The theorem:** If two lines are drawn from a point and cut by two parallel lines, the ratios of corresponding segments are equal (AB/BD = AC/CE).

**TSA mapping:**

Parallel lines are Ε-type structures: they maintain constant separation, self-regulating against convergence or divergence. The proportional ratios they produce are also Ε-type — fixed, bounded, self-correcting under any affine transformation that preserves parallelism.

When the lines are not parallel, they converge to a point (if extended) or diverge without bound — Π-type behaviour. The critical condition — exactly parallel, neither converging nor diverging — is the Β-state of the line angle. The theorem holds precisely at that Β-condition.

More precisely: the ratio AB/BD is an Ε-type quantity (bounded, preserved under the Ε-type parallel structure). Perturb the parallel line to non-parallel and the ratio cascades (Π-type) — it changes without bound as the line tilts. The intercept theorem is the Ε-type theorem of proportionality that holds exactly and only at the Β-condition of parallelism.

**What this confirms:** Ε-type relationships (proportional ratios) are preserved by Ε-type structures (parallel lines). Disrupting the Ε-structure (tilting toward convergence) produces Π-type behaviour. The Β-condition (exact parallelism) is the structural boundary between the two regimes.

---

## 3. Euler's Identity [structural]

**The identity:** e^(iπ) + 1 = 0

**TSA mapping:**

This identity relates the five fundamental constants of mathematics. Three of them are directly TSA-significant:

- π: the Π-state constant. Its decimal sequence has cascade character — direction-fragmented, asymmetric, non-repeating.
- e: the Ε-state constant. Its decimal sequence has equilibrium character — oscillation-dominant, rhythmic, stable.
- 0: the terminal marker. In the symbolic reduction, 0 is prior to the counting system — the boundary before being.

The imaginary unit i is the rotation operator — multiplication by i rotates by 90° in the complex plane. 90° is the Β-angle from Thales' theorem: the self-complementary angle. The exponential e^(iπ) takes the Ε-state base e, raises it to the Π-state exponent π, in the Β-direction (imaginary axis), and arrives at -1 — which is the additive complement of 1.

In TSA terms: e^(iπ) = -1 means the Ε-type exponential, driven by the Π-type constant through the Β-direction, produces the complement of the multiplicative unit. Adding 1 (the unit) to its complement: 1 + (-1) = 0 = the terminal. This is the complementation law (Theorem 2): x ⊕ ¬x = Π reaches the extreme, and what is prior to the system (0) is what closes it.

Euler's identity is not a proof of TSA structure, but it is the most compressed statement in classical mathematics that places π and e in complementary relationship, separated by the 90°-rotation (the Β-direction), with the terminal (0) as the natural closure.

**What this confirms:** The choice of π and e as the two encoding constants is not arbitrary in the numerical sense either — they are already in a known complementary relationship in complex analysis, with the imaginary axis (the Β-direction) as the separator.

---

## 4. De Morgan's Laws [exact]

**The laws:** ¬(A ∨ B) = ¬A ∧ ¬B and ¬(A ∧ B) = ¬A ∨ ¬B

**TSA mapping:**

TSA Theorem 1 is the direct analog: ¬(x ⊕ y) = ¬x ⊗ ¬y and ¬(x ⊗ y) = ¬x ⊕ ¬y.

The proof structure is identical: RESOLVE is defined as the De Morgan dual of CASCADE (x ⊗ y = ¬(¬x ⊕ ¬y)), so De Morgan duality holds by construction, as it does for AND/OR defined by De Morgan from each other.

The difference: in Boolean algebra, De Morgan duality coexists with distributivity and absorption, making the full structure a Boolean algebra. In TSA, De Morgan duality holds but distributivity and absorption fail (Theorems 7 and 8). TSA has De Morgan's law in a non-distributive, non-absorbing algebra — a combination not present in Boolean algebra or standard three-valued logics including Kleene's.

**What this establishes:** TSA extends the domain of De Morgan's law to algebras that are not lattices. The law is more general than its Boolean context suggests.

---

## 5. Lyapunov Stability Theory [exact]

**The theory:** A dynamical system is Lyapunov stable at an equilibrium point x* if there exists a function V(x) > 0 with V(x*) = 0 and dV/dt ≤ 0 along trajectories. Asymptotic stability requires dV/dt < 0 strictly away from x*.

**TSA mapping:**

Lyapunov stability is the Ε-type condition formalised. A Lyapunov function is an Ε-type quantity: it is bounded below (by 0), it self-corrects (decreasing along trajectories), and it certifies convergence to equilibrium. The equilibrium point x* is the Ε-attractor: the state to which the system returns when displaced.

Instability (no Lyapunov function exists, trajectories diverge) is the Π-type condition: the system accumulates distance from equilibrium without self-correction.

The boundary of the stability region — the set of initial conditions from which some trajectories converge and others diverge — is the Β-manifold. Points on this boundary are neither stable nor unstable; they are the bifurcation surface in state space.

TSA's COMPLETE operation (↓) maps directly to Lyapunov's asymptotic stability result: ↓Ε = Ε (stable systems converge to their equilibrium) and ↓Β = Ε (boundary states without forcing tend toward equilibrium — the boundary is unstable and resolves).

**What this establishes:** The TSA type system is the character-level abstraction of Lyapunov stability classification. Ε-type = Lyapunov stable. Π-type = Lyapunov unstable. Β-type = on the boundary of the stability region. COMPLETE (↓) is the TSA operation corresponding to the long-time limit of a Lyapunov-governed flow.

---

## 6. Feigenbaum Constants [structural]

**The constants:** In period-doubling cascades (e.g., the logistic map), the ratio of successive bifurcation intervals converges to δ ≈ 4.66920... (Feigenbaum's first constant). The ratio of successive orbit widths converges to α ≈ 2.50290... (Feigenbaum's second constant). Both are universal — they appear in all one-dimensional maps with a quadratic maximum.

**TSA mapping:**

Feigenbaum's constants are universal Β-anchors. They do not characterise any particular system — they characterise the rate at which Β-conditions (bifurcation points) accumulate as a control parameter increases toward the onset of chaos.

In TSA terms: as a Π-type variable (the cascade-driving control parameter) increases, the system passes through a sequence of Β-conditions. The ratio at which successive Β-conditions appear is δ — a constant that applies universally across all systems with the same topological character. The Β-conditions accumulate (at rate 1/δ per step) toward the Π-onset (R_BIFURCATION in the logistic map).

δ is therefore not a Β-type constant in the usual sense (a threshold for a specific variable) — it is a Π-type quantity about the cascade structure of Β-conditions themselves: the non-repeating, accumulating rate at which bifurcations build toward chaos.

The universality of δ and α across all quadratic maps is the statement that the Β-to-Π transition has Π-type character at the macro level — the cascade of bifurcations follows a non-repeating, universal law regardless of the specific system. TSA predicts this: the cascade of Β-conditions (Β⊕Β=Π) has Π-type character.

**What this establishes:** The rule Β⊕Β=Π (Axiom TSA5) has a quantitative realisation in the Feigenbaum cascade: the accumulation of boundary conditions drives cascade behaviour, universally.

---

## 7. Catastrophe Theory — The Fold Catastrophe [exact]

**The theory (René Thom, 1972):** The fold catastrophe is the simplest elementary catastrophe. A smooth function with control parameter c has a critical point (fold) where the equilibrium surface folds, creating a region with two stable equilibria and one unstable equilibrium. As c crosses the fold, the system jumps discontinuously from one stable equilibrium to another — hysteresis.

**TSA mapping:**

The fold catastrophe is the minimal geometric realisation of the TSA type transition. The equilibrium surface before the fold is the Ε-type regime. After the fold is crossed (the Π-type transition), the system jumps to a new equilibrium — itself Ε-type in the new regime, but reached by a discontinuous cascade.

The fold itself — the singular surface where stable and unstable equilibria coalesce — is exactly the Β-manifold. Points on the fold are neither stable (they are the boundary of the stability region) nor divergent (they have not yet cascaded).

TSA's COMPLETE operation (↓Β = Ε) maps to the catastrophe-theoretic result that the fold resolves: once the fold is crossed, the system falls to the nearest stable equilibrium (Ε). The fold is a Β-type structure that cannot persist without active maintenance of the control parameter precisely at the singular value.

The seven elementary catastrophes (fold, cusp, swallowtail, butterfly, hyperbolic umbilic, elliptic umbilic, parabolic umbilic) classify all possible ways that Β-manifolds can be structured in smooth parameter spaces. TSA identifies these as Β-type structures by character; Thom's classification specifies their topology.

**What this establishes:** Catastrophe theory is the topological classification of Β-manifolds. TSA provides the algebraic character framework within which Thom's classification operates.

---

## 8. Kolmogorov-Arnold-Moser (KAM) Theory [structural]

**The theory:** In near-integrable Hamiltonian systems, most invariant tori (Ε-type structures) from the integrable limit persist under small perturbations. However, resonant tori (those with rational frequency ratios) break first, and as the perturbation grows, successively more irrational tori break, until at large perturbation the system becomes fully chaotic.

**TSA mapping:**

Integrable Hamiltonian systems are fully Ε-type: they possess a complete set of conserved quantities (Ε-type by Noether's theorem), and trajectories wind on invariant tori — bounded, quasi-periodic, self-regulating.

The onset of chaos is the Π-type regime: trajectories fill regions of phase space without return, accumulating distance from prior states.

The KAM tori are the Β-structures: they are the boundary objects between ordered (Ε) and chaotic (Π) regions in phase space. KAM theory's central result is that Β-type structures (irrational-frequency tori) persist longer than rational-frequency tori under perturbation — the more irrational the frequency ratio, the more the torus resists being destroyed.

This connects to TSA's Encoding Theorem: sin(π²x̃) carries weight 3 in the Π-basis precisely because π² is irrational. Irrational frequency ratios are more resistant to the transition to chaos — they are the longest-surviving Β-structures in phase space. The weight 3 of the irrational harmonic reflects its structural robustness in maintaining non-repeating character before the full cascade into chaos.

**What this establishes:** The irrational harmonic sin(π²x) in the Π-encoding is not merely mathematically non-periodic — it is, by KAM theory, the structural character of the longest-surviving boundary conditions in the transition from order to chaos.

---

## 9. Noether's Theorem [structural]

**The theorem:** For every continuous symmetry of the action of a physical system, there is a corresponding conserved quantity.

**TSA mapping:**

Conserved quantities are Ε-type by definition: they do not accumulate, they self-regulate to their conserved value, and they are bounded by the conservation law. Energy, momentum, angular momentum — all Ε-type.

The symmetry that generates each conserved quantity (time translation for energy, spatial translation for momentum, rotation for angular momentum) is also Ε-type: it is a structure that preserves the system's character under transformation.

When a symmetry is broken — explicitly (by a non-symmetric potential) or spontaneously (by a vacuum state that does not share the symmetry of the action) — the conserved quantity is no longer conserved. Its character shifts from Ε to Π: it begins accumulating, changing without self-correction.

The moment of symmetry breaking — the critical coupling constant or temperature at which the symmetry is broken — is the Β-condition. In spontaneous symmetry breaking: above the critical temperature, the system is symmetric (Ε-type). Below it, the symmetry is broken and a cascade of ordering occurs (Π-type, characterised by the order parameter growing from 0). The critical temperature T_c is the Β-anchor.

**What this establishes:** Noether's theorem is the mathematical basis for classifying conserved quantities as Ε-type. Symmetry-breaking phase transitions are Β-type events. The ordered phase below T_c has a Π-type order parameter (the cascade from disorder to order). The full thermodynamic state classification maps onto {Π, Ε, Β}.

---

## 10. The Basel Problem and π² [structural]

**The result (Euler, 1734):** Σ_{n=1}^{∞} 1/n² = π²/6.

**TSA mapping:**

The encoding basis for Π-type variables includes sin(π²x̃) with weight 3 — the irrational harmonic. The appearance of π² rather than π or 2π is structurally motivated in TSA by the need for a strictly non-periodic basis function. But π² also appears as the natural scale of the Basel problem: the sum of reciprocals of perfect squares.

Reciprocals of perfect squares are Ε-type quantities: each term 1/n² is a bounded, positive quantity that decreases monotonically, and the sum converges — a self-regulating series. The fact that this Ε-type sum converges to π²/6 — where π is the Π-state constant — is a statement that the cumulative equilibrium of all squared reciprocals reaches exactly the Π-scale squared, divided by 6.

6 = 2×3 is the product of the first two non-trivial digits (2 and 3), both primitive in the reduction table. The denominator 6 is the most fundamental composite in the reduction framework.

The Basel problem therefore says: the Ε-type accumulation of reciprocal-square decay converges to exactly the Π-type scale (π²) modulated by the most basic composite (6). This is a quantitative relationship between the Ε-type series character and the Π-type constant — the two fundamental characters of TSA connect through the most natural convergent sum in analysis.

This provides independent numerical confirmation that π² is the structural scale separating the single-period cascade (π) from the higher-order cascade structure — which is why sin(π²x̃) is the correct second-scale Π-basis function and earns weight 3.

**What this establishes:** The weight 3 of sin(π²x̃) in the Π-encoding is confirmed from two independent directions: irrationality (KAM theory correspondence) and the Basel problem (π² as the natural scale of the Ε-to-Π boundary in convergent series).

---

## 11. Poincaré-Bendixson Theorem [structural]

**The theorem:** In a two-dimensional continuous dynamical system, every bounded trajectory converges to either a fixed point (Ε-type), a limit cycle (Ε-type), or a homoclinic or heteroclinic orbit (Β-type). Chaos is impossible in two dimensions.

**TSA mapping:**

The theorem classifies trajectories in 2D exactly according to TSA types — without using TSA's framework. Fixed points are Ε-type (self-correcting attractors). Limit cycles are Ε-type (bounded periodic orbits). Homoclinic and heteroclinic orbits are Β-type (boundary structures connecting saddle points — themselves Β-type — to each other or to themselves).

The theorem states that Π-type behaviour (chaos) requires at least three dimensions. In TSA terms: CASCADE requires more degrees of freedom than RESOLVE. The Π-type character cannot be confined to a 2D phase space; it needs the additional dimension to cascade without return.

This is a dimensional constraint on TSA type realisation: Ε-type and Β-type are achievable in 2D; Π-type requires 3D or higher. The theorem gives a topological reason for why cascade character is structurally more complex than equilibrium character.

**What this establishes:** TSA types have topological dimension constraints. Ε and Β require only 2D phase space; Π requires 3D. This is an independent mathematical confirmation that cascade character (Π) is structurally richer than equilibrium character (Ε) — consistent with the encoding requiring 5 Π-basis functions versus 3 Ε-basis functions.

---

## 12. Gödel's Incompleteness Theorems [suggestive]

**The theorems:** In any consistent formal system powerful enough to express Peano arithmetic, there exist true statements that are neither provable nor disprovable within the system.

**TSA mapping (suggestive):**

The undecidable statements are neither provably true (within the Ε-type closed world of the formal system's theorems) nor provably false (Π-type, contradicted). They are at the structural boundary — Β-type propositions that the system cannot resolve to either character.

The system's own consistency statement is the canonical Β-type object: it is true (the system is consistent, assuming it is) but unprovable within the system. Proving it would either require stepping outside the system (TSA COMPLETE: ↓, the temporal operator that exceeds the algebraic closure) or extending the system with new axioms.

This maps onto TSA's Theorem 11: the constant function f(x) = Β cannot be expressed within {⊕, ⊗, ¬} — the algebraic operations alone cannot generate the boundary state from inside the closed system. COMPLETE (↓) is required to access it, just as a meta-system is required to settle Gödel's undecidable propositions.

**Caveat:** This correspondence is structural and suggestive. A formal mapping between TSA and provability logic would require significant additional development — in particular, a proof-theoretic interpretation of CASCADE and RESOLVE — and is not claimed here. The parallel is noted for its structural depth.

---

## Summary Table

| Mathematical Result | TSA Correspondence | Grade |
|---|---|---|
| Thales' circle theorem | Β-condition = self-complementary angle (¬Β=Β) | Exact |
| Thales' intercept theorem | Ε-type proportionality from Ε-type parallel structure | Structural |
| Euler's identity | π and e in complementary relationship via Β-direction (i) | Structural |
| De Morgan's laws | TSA Theorem 1: ¬(x⊕y)=¬x⊗¬y | Exact |
| Lyapunov stability | Ε = stable, Π = unstable, Β = stability boundary, ↓ = long-time limit | Exact |
| Feigenbaum constants | Β⊕Β=Π: cascade of bifurcations has universal Π-character | Structural |
| Catastrophe theory (fold) | Β-manifold topology; ↓Β=Ε as fold resolution | Exact |
| KAM theory | Irrational tori (Β-structures) resist Π-transition; confirms weight of sin(π²x) | Structural |
| Noether's theorem | Ε = conserved quantity; Β = symmetry-breaking threshold | Structural |
| Basel problem | π²=6·Σ(1/n²): Ε-type convergence reaches Π-type scale; confirms π² as structural scale | Structural |
| Poincaré-Bendixson | Π-type requires 3D; Ε and Β achievable in 2D | Structural |
| Gödel incompleteness | Undecidable propositions as Β-type; COMPLETE as meta-system access | Suggestive |

---

*Companion to TSA Methodology v3. Further correspondences to be developed: Morse theory (Β-type critical points of smooth functions), Renormalisation Group fixed points (Ε-type), and Galois theory (solvable = Ε-type, non-solvable = Π-type).*
