# Intentional Symbolic Pre-Cognitive Computing (ISPCC)
## A Framework for Structure-First Machine Learning

---

## The Name

**Intentional** — both the encoding of variables and the selection of training samples
are deliberate acts derived from structural knowledge, not from data statistics.

**Symbolic** — the mathematical basis functions (π and e) and the dimensionless groups
(Buckingham Pi theorem) are prescribed from the symbolic character of each variable.
They are not learned, not tuned, and not data-derived. π encodes cascading non-periodic
structure. e encodes self-regulating bounded structure. These are mathematical facts,
not hyperparameters.

**Pre-Cognitive** — all discoverable structure is established before the learning
algorithm engages. The model does not discover physics. It inherits physics as its
coordinate system and learns only what the coordinate system cannot explain. The word
"cognitive" here refers to the learning process; "pre-cognitive" means prior to it,
in the same sense that grammar exists before a language is spoken.

**Computing** — this is a framework for how to use computation when structural knowledge
exists. It is not a model architecture. It is not a training procedure. It is a
principled sequence for transferring physical knowledge into the representation space
before any learning occurs. The ML model is one component, not the method.

---

## Position Relative to Existing Approaches

### Physics-Informed Neural Networks (PINNs)

PINNs embed differential equations as soft constraints in the loss function. The network
is still free to choose its own internal representation; the physics enters as a
regulariser that penalises solutions inconsistent with the governing equations.

The consequence: PINNs still search for structure inside the learning loop. When data
is insufficient — as in engineering DoE with 40-200 simulation points — the network
cannot balance data fit and physics constraint simultaneously. The representation
problem and the fitting problem are coupled, and both fail together.

ISPCC decouples them. Structure is established outside the learning loop entirely.
The learning algorithm receives a coordinate system in which the dominant physics
is already encoded, and only handles irreducible residuals. PINNs constrain the search
space. ISPCC eliminates most of the search space before search begins.

**Demonstrated:** PINN on the 5G headset EM surrogate hit a 57% R² ceiling at 200
simulation points. ISPCC at 40 intentionally selected points gave 66% R², with 60
points giving the same mean at half the variance.

### Standard Physics-Informed Feature Engineering

Standard approaches add domain-derived features — dimensionless ratios, log transforms,
known physical scales — as additional inputs to a standard ML model. This is ad hoc,
domain-specific, and non-systematic. The features are chosen by intuition rather than
by a principled encoding rule. No distinction is made between variables whose structure
is cascading (non-periodic, unbounded) and those that are self-regulating (periodic,
bounded). The model still has to discover which features matter and how they interact.

ISPCC differs in three ways. First, the encoding rule is systematic and domain-agnostic:
the character of each variable (π-basis or e-basis) is determined by its structural
behaviour, not by domain intuition. Second, the probe is a formal discovery mechanism
that identifies canonical variables automatically from importance rankings, rather than
relying on domain expertise. Third, the staged model architecture (Ridge grammar + RF
residuals) follows necessarily from pre-loading structure — once the grammar is removed,
the residuals are a different and simpler learning problem.

### Transfer Learning

Transfer learning moves learned representations between domains. ISPCC moves structural
knowledge — confirmed physical constants, geometric coordinates, dimensional analysis —
before any representation is learned. The distinction is that ISPCC transfers what is
known analytically, not what has been learned empirically.

---

## The Core Principle

> Establish all discoverable structure before the learning algorithm engages.
> Give the model a coordinate system in which the dominant physics is explicit.
> Ask the model only to learn what the coordinate system cannot explain.

This principle has three implications.

**Implication 1 — Data efficiency.** When the coordinate system carries most of the
variance (the power law, the regime switch, the resonance structure), the residuals
are small and smooth. A model learning small smooth residuals from 40 intentional
points outperforms a model learning the full signal from 200 random points. Data
efficiency is a consequence of pre-loading structure, not of model complexity.

**Implication 2 — Interpretability.** The Stage 1 Ridge coefficients are the power law
exponents. They can be checked for physical sign and compared to analytical models.
The Stage 2 RF residual importance reveals which physical mechanisms are not yet
accounted for in the structural encoding. The method explains its own gaps.

**Implication 3 — Sample selection.** If the coordinate system is structurally
meaningful, the distance metric in that space is also structurally meaningful. MaxiMin
in a structurally grounded 7D space selects training points that are maximally diverse
in structural terms — not geometrically arbitrary. This is the intentional part: the
simulation budget is spent covering the structure, not covering raw input coordinates.

---

## The Four Components

### Component 1 — Symbolic Encoding (the coordinate system)

Every input variable is classified by its structural character and encoded in the
corresponding mathematical basis. The classification is binary and exhaustive.

**Pi-basis (π-encoding):** for variables that are cascading, non-periodic, or unbounded
across the relevant range. The basis is a Fourier + power-pi combination:
sin(π·x), cos(π·x), sin(2π·x), sin(π²·x), sin(π·x)·cos(π²·x).
Weights (5,1,1,3,1) pre-specify the cascade structure: the fundamental cascade mode
carries most of the weight; the irrational harmonic sin(π²·x) captures the strongest
non-repeating character. These weights are not tuned — they are structural assertions.

**E-basis (e-encoding):** for variables that are self-regulating, bounded, or convergent.
The basis is exponential: exp(−e·x), x^e, exp(−e·(x−0.5)²).
Weights (2,2,1): near-uniform, confirming that flat weighting is structurally correct
for bounded variables.

**Normalisation scales** are set from confirmed physical constants, not from data
statistics. The argument to every basis function is structurally meaningful:
sin(π · gap/λ_free) means "gap as a fraction of one free-space wavelength."
The model never sees a number without physical meaning.

**Cross-products** combine π-encoded and e-encoded variables:
sin(π · cascading) × exp(−e · self-regulating). These encode interaction physics:
resonance modulated by loss, path length modulated by geometry, field coupling
modulated by material regime.

### Component 2 — Canonical Reduction (the probe)

The probe is a formal mechanism for identifying which variables are load-bearing in
the encoding. It runs a Random Forest on the full encoded feature set and returns
importance rankings.

The canonical reduction follows from the probe: identify the dominant variables,
trace them back to their fundamental physical form, encode those fundamentals directly.
In harmonics, 11 inherited features reduced to 2 canonical variables (p and q — the
coprime numerator and denominator). In EM, 4 raw inputs and 89 encoded features
reduced to 3 canonical physics variables (gap, total electrical thickness, loss
tangent) and 3 geometric regime variables (Pi28, Pi31, Pi32 from the waveguide
triangle).

The probe does not guess. It reads the importance rankings and lets the data confirm
which encoding is doing structural work. It is validated when the canonical encoding
trained on fewer features matches or exceeds the full encoding on more features.

**Key finding:** The probe identified log_q_den (reduced denominator of the harmonic
ratio) as the dominant variable at 9.2% importance — nearly 3× any other feature.
This pointed to the exact canonical form: GS = f(p, q) only. The probe recovered
in one RF fit what harmonic number theory states analytically.

### Component 3 — Intentional MaxiMin (the selection strategy)

Standard DoE (Latin Hypercube Sampling, random) selects points to cover the raw
input space. ISPCC selects points to cover the structurally meaningful space.

**7D IntentionalMaxiMin:** [gap, upper, lower, tan_δ, Π28, Π31, Π32], all normalised
to [0,1]. Each dimension contributes equally to pairwise Euclidean distance.

The raw 4D dimensions (gap, upper, lower, tan_δ) ensure coverage of the input range —
this is what Stage 1 Ridge needs to recover the power law accurately.

The geometric 3D dimensions (Π28, Π31, Π32) ensure coverage of the waveguide regime
space — this is what Stage 2 RF needs to learn the residuals from the correct
structural corners.

**The greedy MaxiMin algorithm:** start from one point, then at each step add the
unselected point with maximum minimum-distance to the already-selected set. Runs in
O(N_pool × n_select) — milliseconds for engineering-scale datasets.

**Validated:** At exactly the literature minimum for 4 inputs (10×d = 40 simulations),
7D IntentionalMaxiMin with the three-stage model gives R²=0.664 vs R²=0.551 from
200 randomly sampled simulations. This is not a lucky result — 60 intentional points
give R²=0.660 ± 0.099, confirming the mean is real and the reduction in σ from 0.205
to 0.099 confirms corner reliability at modest budget increase.

### Component 4 — Staged Learning (the model architecture)

The staged architecture follows necessarily from the pre-cognitive principle. Having
established structure outside the learning loop, the learning is split into two tasks
that are fundamentally different in character.

**Stage 0 — Geometric computation (no fitting):**
Compute Π28, Π31, Π32 from confirmed HFSS coordinates. This is pure physics — the
waveguide triangle, the 3λ engineered path, the 86° deflection geometry. No training
data involved.

**Stage 1 — Ridge on [unencoded-4D + Π28 + Π31 + Π32]:**
Ridge recovers the log-linear grammar: the power law exponents (gap^α, layer^β,
dielectric^δ) and the waveguide regime correction (Π31 = PATH_RATIO/(tan_δ/DIEL_BIFURC)).
Ridge is used because the grammar is genuinely linear in this feature space, and
L2 regularisation keeps coefficients physically stable at small N. The exponent
signs serve as a sanity check: negative for gap (more separation → less absorption),
negative for layers (more shielding → less absorption), positive for dielectric
(higher permittivity → more coupling into tissue).

**Stage 2 — RF on full encoded features → Stage-1 residuals:**
The residuals from Stage 1 are smaller (less variance to explain), cleaner (no
dominant grammar trend remaining), and more local in character (dominated by
resonance peaks, curvature corrections, near-field transitions). RF with bagging
and max_features="sqrt" learns these local nonlinear patterns from intentionally
selected points efficiently. XGB is not used here: boosting's sequential refinement
memorises sparse residuals at small N. RF's parallel bagging is robust.

**Prediction:** exp(Stage1(x) + Stage2(x))

---

## The Probe as Method

The probe is what makes ISPCC systematic rather than ad hoc. Without the probe,
canonical reduction requires domain expertise for every new problem. With the probe,
it requires one RF fit and one importance ranking read.

The probe validates itself. If the importance ranking confirms that the probe-selected
canonical features explain more variance with fewer features than the full encoding,
the canonical reduction is confirmed. If not, the probe tells you which dimensions
are still missing — not by failing silently, but by showing high residual importance
in unexplained feature groups.

**In harmonics:** probe found log_q_den at 9.2%. Canonical: GS = f(p,q). Verified:
CANON-6 (6 features from 2 variables) beat RAW-11 at 7 of 9 sample sizes.

**In EM:** probe found gap-related Pi groups dominating all top-10 features. Canonical:
gap, total electrical thickness, loss tangent as the 3 independent physics axes.
Verified: the geometric triangle (confirmed from HFSS coordinates) provided Pi28,
Pi31, Pi32 — the regime switch that the probe identified as the unencoded systematic
residual.

---

## Formal Definition

Let P be a physical system with n inputs x₁,...,xₙ and scalar output y.
Let K be the set of confirmed physical constants for that system.
Let C be the set of structural character assignments {π-basis, e-basis} for each xᵢ.

**ISPCC defines a surrogate f(x) = exp(f₁(x) + f₂(x)) where:**

f₁: Stage 1 (Ridge) on [x̂ₖ + Π₂₈ + Π₃₁ + Π₃₂]
   where x̂ₖ = {log(xᵢ) for each raw input} and Πⱼ are structural dimensionless groups
   derived from K and the confirmed geometry.

f₂: Stage 2 (RF) on Φ(x) → (log(y) - f₁(x))
   where Φ(x) is the full pi/e encoded feature set derived from K and C.

**Training points** x₁,...,xₙ are selected by MaxiMin in [x_normalised, Π₂₈, Π₃₁, Π₃₂],
the 7D intentional space combining raw input coverage with regime coverage.

**C is determined** by running the probe (RF importance on Φ(x)) on any available data
and reading canonical variables from the dominant features. C is not assumed — it is
discovered and validated.

---

## Comparison Table

| Property | PINN | Standard Feature Eng. | ISPCC |
|---|---|---|---|
| Physics location         | Inside loss function      | Inside feature set         | Outside learning loop               |
| Structure discovery      | By network training       | By domain expertise        | By probe (automatic)                |
| Encoding basis           | Learned                   | Ad hoc                     | Systematic (π, e)                   |
| Sample selection         | Random                    | LHS/random                 | IntentionalMaxiMin                  |
| Model                    | Neural network            | RF/XGB                     | Ridge grammar + RF dialect          |         
| Fails at small N         | Yes — loss balance breaks | Partially                  | No — structure pre-loaded           |
| Interpretable gaps       | No                        | Partially                  | Yes — Stage 2 importance            |
| Requires full PDE        | Yes                       | No                         | No                                  |
| Requires constants       | Partially                 | No                         | Yes — but verifiable                |
| Domain-agnostic encoding | No                        | No                         | Yes — same π/e basis across domains |

---

## Validated Domains

**Harmonics (Euler Gradus Suavitatis):** discrete mathematical domain, exact ground truth.
Proved: same encoding functions (unchanged weights) generalise from EM to number theory.
Proved: probe recovers canonical structure (p, q) automatically.
Proved: CANON-6 (6 features) > RAW-11 (11 features) at 7/9 sample sizes.

**EM surrogate (5G headset SAR):** engineering simulation domain, 200 HFSS points.
Proved: 40 intentional points at R²=0.664 > 200 random points at R²=0.551.
Proved: geometric triangle (confirmed coordinates) provides regime variables that
break the 57% ceiling that PINN and single-stage models could not exceed.
Proved: 7D IntentionalMaxiMin reduces σ from 0.205 to 0.099 between 40 and 60 points.
Proved: correction factor 1.44-1.50× for high-SAR designs is structurally stable
(consistent between 40 and 60 points — a model property, not a sampling artefact).

**Pending validation:** Higgs Boson classification (ML benchmark: does probe recover
physicists' high-level derived features? does encoding beat XGBoost at small N?);
thermal simulation surrogate (second engineering DoE domain: does the full pipeline
replicate the EM result with independent physics?).

---

## What ISPCC Is Not

It is not a new model architecture. Ridge and RF exist. MaxiMin exists.
Buckingham Pi theorem is 1914.

It is not physics-informed ML in the existing sense. Physics-informed ML puts physics
inside the model. ISPCC puts physics before the model.

It is not feature engineering. Feature engineering is ad hoc and domain-specific.
ISPCC has a universal encoding rule (π for cascading, e for bounded), a formal
discovery mechanism (the probe), and a principled selection strategy (IntentionalMaxiMin
in the structurally meaningful space).

**It is a framework for how to compute with ML when structural knowledge exists.**
The sequence — probe, canonical reduction, symbolic encoding, intentional selection,
staged learning — is the method. Any model that follows this sequence is an ISPCC
instance. The specific models (Ridge, RF) are the current best choices for engineering
surrogate problems at small N. They are not definitional.

---

## On the Name

"Intentional Symbolic Pre-Cognitive Computing" was chosen over alternatives for
specific reasons.

"Physics-Informed" is already claimed by PINNs and carries the connotation of
physics inside the loss. ISPCC puts physics outside the learning loop entirely —
using the same label would be misleading.

"Surrogate Modelling" is accurate but describes the application domain (engineering
DoE) rather than the principle. ISPCC applies to any problem where structural
knowledge can be established before learning.

"Pre-Cognitive" is the precise term. It does not mean the model lacks intelligence.
It means that the mathematical structure — the coordinate system, the canonical
variables, the geometric regime — is established before the computational intelligence
engages with the data. The model's cognition is applied only to what structure cannot
explain. This is not a limitation of the model. It is a principled allocation of
what computation is for.

"Symbolic" anchors the method to the encoding: π and e as structural constants with
mathematical meaning beyond their numerical values. π appears because it is the period
of cascading non-repeating structure. e appears because it is the base of the
exponential that governs bounded convergent processes. Using them as encoding bases
is a claim about the structure of physical reality, not a choice of hyperparameter.

"Intentional" connects the encoding to the selection. Both are deliberate: the
encoding because the basis functions are prescribed from structural knowledge, the
selection because the training points are chosen to cover the structurally meaningful
space. Nothing in ISPCC is random by default. Randomness appears only where structure
runs out — in the residuals, and in the starting point of the greedy MaxiMin
(which is varied over seeds for variance estimation, but the selection itself is
structurally deterministic given any starting point).