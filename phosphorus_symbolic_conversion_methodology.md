# Symbolic Conversion Methodology
## From Rational Encoding to Irrational Structural Encoding
### Phosphorus v1 → v2 · TSA/ISPCC Framework

---

## What Changed and What Did Not

Everything in the Phosphorus classifier except the three encoding functions is
identical between v1 and v2: the structural constants, data loading, fingerprint
computation, k-d tree search, display, and all command-line behaviour are
unchanged. The conversion is confined to:

- `phi_pi(x)` — the Π-basis (cascade character)
- `phi_e(x)` — the Ε-basis (equilibrium character)
- `phi_b(x)` — the Β-basis (boundary character)

The structural claim of the classifier — that 12 elemental properties collapse
onto three physically motivated coordinates — is identical in both versions.
What changed is the mathematical substance of what those coordinates express.

---

## The Conversion Principle

Every rational structure in v1 is replaced in v2 with the algebraically
motivated irrational equivalent. Four substitution rules govern the conversion.
They are applied simultaneously, not sequentially.

---

## Rule 1 — Replace Rational Normalisers with Irrational Combinations

**v1:** Normalisers are counts of terms expressed as integers.

```
phi_pi: normaliser = 11  (sum of integer weights 5+1+1+3+1)
phi_e:  normaliser =  5  (sum of integer weights 2+2+1)
phi_b:  normaliser =  1  (single term, no explicit normaliser)
```

The normaliser 11 asserts: "this function returns a value in the range of
a weighted sum of five terms with integer weights." The 11 is a bookkeeping
number, not a structural constant.

**v2:** Normalisers are algebraic combinations of the two structural constants π and e.

```
phi_pi: normaliser = π + e − 1  ≈ 4.860
phi_e:  normaliser = e          ≈ 2.718
phi_b:  normaliser = π + e      ≈ 5.860
```

The normaliser π+e−1 asserts: "the combined contribution of these five terms
is bounded by the algebraic relationship between the two fundamental irrational
constants of the encoding system." It is derived from the structure of the
function, not chosen to make the weights sum to one.

**The conversion step:** For any rational normaliser N, find the combination
of {π, e, π²,  π+e, π−e, π·e, π/e, e/π} whose value is closest to N and
whose form is algebraically motivated by the basis type. For the Π-basis
(five terms, π-dominated), π+e−1 is the natural combination. For the Ε-basis
(three terms, e-dominated), e alone is the natural combination. For the Β-basis
(three terms, balanced between π and e at the boundary), π+e is natural.

---

## Rule 2 — Replace Integer Exponents with Irrational Ratios of π and e

**v1:** x is passed directly to trigonometric and exponential functions.

```python
# phi_pi v1
math.sin(PI * x)          # period = 2, repeats at x = 2, 4, 6, 8, 10
math.sin(PI**2 * x)       # period = 2/π ≈ 0.637
```

`sin(πx)` completes exactly 5 full cycles on x ∈ [0, 10]. It returns to the
same value at x = 2, 4, 6, 8, 10. The function is periodic at rational
multiples of the input. For a cascade variable — one that is explicitly
non-returning by TSA definition — a periodic basis is a structural mismatch.

**v2:** x is first raised to an irrational exponent before being passed to
trigonometric functions.

```python
# phi_pi v2
u_ie  = x ** (1 / E)      # x^(1/e)  ≈ x^0.368 — irrational exponent
u_ipi = x ** (1 / PI)     # x^(1/π)  ≈ x^0.318 — irrational exponent
u_epi = x ** (E / PI)     # x^(e/π)  ≈ x^0.865 — irrational exponent
u_pie = x ** (PI / E)     # x^(π/e)  ≈ x^1.156 — irrational exponent

math.sin(PI * u_ie)       # sin(π · x^(1/e)) — never periodic on rational interval
math.sin(PI**2 * u_epi)   # sin(π² · x^(e/π)) — never periodic on rational interval
```

The composition of a periodic function with an irrational power is provably
aperiodic on any rational interval: `sin(π · x^(1/e))` returns to the same
value only if `x^(1/e)` differs by exactly 2 between two inputs, which requires
the two inputs to differ by `2^e ≈ 6.580` — an irrational number, so no two
rational inputs produce identical function values. The non-returning character
of the Π-type variable is now encoded in the mathematics of the basis function,
not just asserted by the weight structure.

**The four irrational exponents and their motivation:**

| Exponent | Value | Structural meaning |
|---|---|---|
| 1/e | ≈ 0.368 | Sub-linear stretch — emphasises differences near zero |
| 1/π | ≈ 0.318 | Sub-linear stretch — slightly stronger than 1/e |
| e/π | ≈ 0.865 | Near-linear — preserves relative scale with slight irrational warp |
| π/e | ≈ 1.156 | Super-linear stretch — emphasises differences near the upper bound |

The four exponents are all ratios of the two structural constants of the
encoding system. They are not chosen by optimisation. They are the four
non-trivial ratios {1/e, 1/π, e/π, π/e} of the set {1, π, e}, excluding
trivial cases {1/1, π/π, e/e} and their reciprocals already in the set.

---

## Rule 3 — Replace Geometric Centre Points with Structural Attractors

**v1:** Centre points are geometric — the midpoint of the input range.

```python
# phi_e v1 — Gaussian centred at x = 0.5
math.exp(-E * (x - 0.5) ** 2)

# phi_b v1 — Gaussian centred at x = 0.5
math.exp(-E * (x - 0.5) ** 2)
```

x = 0.5 is the midpoint of [0, 1]. It is chosen by symmetry: the centre of
the bounded input range. This is a geometric argument, not a structural one.

**v2:** Centre points are structural attractors derived from the basis constants.

```python
# phi_e v2 — Gaussian centred at x = 1/e ≈ 0.368
math.exp(-(E / PI) * (u - 1.0 / E) ** 2)
```

The centre `1/e ≈ 0.368` is the natural Ε-attractor of the unit interval
under the e-basis. The function `e^{-ex}` on [0,1] has its mean value at
approximately `1/e` when integrated against the equilibrium-weighted measure.
More precisely: the fixed point of the self-referential equation x = e^{-ex}
that lies in (0,1) is `x ≈ 1/e`. This is the equilibrium point that the
e-basis naturally produces, not a geometric midpoint.

```python
# phi_b v2 — Gaussian in v = (x − 0.5)² space, raised to irrational exponents
v = (u - 0.5) ** 2
math.exp(-PI * v ** (1.0 / E))    # Gaussian in v^(1/e) space
math.exp(-E  * v ** (1.0 / PI))   # Gaussian in v^(1/π) space
math.exp(-(PI**2 / E) * v)        # Gaussian with symbolic width π²/e
```

The Β-basis remains centred at x = 0.5 because the separatrix is by
definition the midpoint between the two regimes — this is a structural
constraint, not a geometric convenience. What changes is the shape of the
Gaussian: rather than a simple Gaussian in x-space, v2 uses three Gaussians
in `v^(1/e)` and `v^(1/π)` space, producing a basis that is sharper near the
boundary (x = 0.5) and heavier-tailed than a standard Gaussian, which better
matches the behaviour of a true physical boundary where the transition is
rapid near the separatrix and gradual far from it.

---

## Rule 4 — Replace Independent Terms with Compounding Terms

**v1:** All terms are additive and independent. Each term contributes a fixed
fraction of the total signal regardless of the value of x.

```python
# phi_pi v1 — five independent additive terms
(5/11) * sin(πx)
+ (1/11) * cos(πx)
+ (1/11) * sin(2πx)
+ (3/11) * sin(π²x)
+ (1/11) * sin(πx) * cos(π²x)   # ← this one is a product, but of functions of the SAME x
```

The weight of each term is constant: `5/11` of the signal always comes from
`sin(πx)`, regardless of whether x is 0.1 or 9.9.

**v2:** Terms compound each other. Each term modulates the next using a
different irrational transform of x.

```python
# phi_pi v2 — five compounding terms
t1 = sin(π  · x^(1/e))
t2 = cos(e  · x^(1/π))
t3 = t1 · exp(−x^(1/π) / e)      # t1 attenuated by irrational decay of x^(1/π)
t4 = sin(π² · x^(e/π))
t5 = t2 · sin(e · x^(π/e))       # t2 modulated by orthogonal oscillation in x^(π/e)
```

The contribution of t1 to the total is not a fixed fraction. It depends on
`x^(1/π)` through the decay term in t3. At large x, the decay is strong and
t3 damps t1's contribution. At small x, the decay is weak and t3 amplifies
the cascade signal. The "weight" of each term is determined by x itself
through the other transforms — the function is not decomposable into
independent contributions by any linear method.

**The structural motivation:** A cascade variable does not decompose into
independent contributions. The cascade of a physical process — bearing
degradation, electromagnetic waveguide activation, logistic map bifurcation
— is precisely characterised by the fact that its next state depends on its
current state in a non-separable way. A basis function that decomposes into
independent additive terms cannot fully encode this interdependence. Compounding
terms, where the contribution of each depends on the others through shared
transforms of x, encode the non-separability structurally.

---

## The Three Conversions Applied

### φ_Π — Cascade Basis

| Property | v1 | v2 |
|---|---|---|
| Input domain | x ∈ [0, 10] | u = x ∈ [1e-15, 10] |
| Input transform | None — x passed directly | Four irrational power transforms |
| Term structure | Five additive terms | Three base + two compounding |
| Periodicity | Periodic at rational multiples | Aperiodic on any rational interval |
| Normaliser | 11 (rational, term count) | π + e − 1 (irrational, structural) |
| Term independence | Fully independent | t3 depends on t1 and x^(1/π); t5 depends on t2 and x^(π/e) |

### φ_Ε — Equilibrium Basis

| Property | v1 | v2 |
|---|---|---|
| Input domain | x ∈ [0, 1] | u = x ∈ [1e-15, 1] |
| Gaussian centre | 0.5 (geometric midpoint) | 1/e ≈ 0.368 (structural Ε-attractor) |
| Power in decay | exp(−e·x) | exp(−e · x^(π/e)) — irrational exponent |
| Power term | x^e | x^(e/π) · exp(−x^π / π) — compounded |
| Normaliser | 5 (rational, term count) | e (irrational, structural constant) |

### φ_Β — Boundary Basis

| Property | v1 | v2 |
|---|---|---|
| Centre | x = 0.5 | x = 0.5 (unchanged — structural constraint) |
| Gaussian space | Standard Gaussian in x | Three Gaussians in v^(1/e), v^(1/π), v space |
| Width | e (single width) | π·v^(1/e-1), e·v^(1/π-1), π²/e (irrational widths) |
| Term count | 1 | 3 |
| Normaliser | 1 (implicit) | π + e (sum of structural constants) |

---

## Output Behaviour: What Changes Numerically

The fingerprints produced by v1 and v2 are not numerically identical. The
(Π, Ε, Β) coordinates of each element will differ. However, the relative
ordering of elements in the three-dimensional character space is preserved in
the structurally significant regions — the clusters identified by the classifier
(moderators near each other, absorbers near each other, structural metals near
each other) remain intact. What changes is the resolution of the manifold at
the boundary between regimes: v2's compounding basis functions produce sharper
discrimination near the Β-axis, where v1's fixed-weight functions cannot
distinguish elements that sit close to a structural separatrix from elements
that are genuinely boundary-type.

---

## Summary: The Conversion in One Statement

v1 asks: *how much does each term contribute?*
The answer is a rational fraction, independent of x.

v2 asks: *what is the structural character of this value of x?*
The answer is an irrational function of x, where the character of x
determines the weight of each term through the same transforms that
define the TSA type of the variable.

The conversion from v1 to v2 is the conversion from an encoding that
describes the function to an encoding that embodies the structure.

---

*Working methodology document. Threshold validation of v2 fingerprints against
nuclear performance data pending.*
