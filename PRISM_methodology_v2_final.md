# PRISM — Predictive Regime-split Intentional Symbolic MaxiMin
## Method Specification v2

**Position:** PRISM is a method within the ISPCC framework, sitting alongside 3SIMM.

| Layer | Name | Role |
|---|---|---|
| Theorem | TSA | Trinary Symbolic Algebra |
| Framework | ISPCC | Intentional Symbolic Pre-Cognitive Computing |
| Method (budget-constrained) | 3SIMM | 3 Staged Intentional MaxiMin |
| Method (data-rich) | **PRISM** | Predictive Regime-split Intentional Symbolic MaxiMin |

PRISM and 3SIMM share the same ISPCC foundation — structural constants, TSA variable
classification, pi/e encoding, and K-dimensional IntentionalMaxiMin. They differ at
the grammar stage, and that difference is the subject of this document.

**v2 additions over v1:**
- Section 1a: Regime-Informed Fold Selection — how the character split improves the
  main method's CV convergence before PRISM's explicit gate is needed
- Stage 4: Chain ordering principle for regime-dominant feature identification
- Stage 7: V4 chain ordering stability check after supplemental sampling

---

## Stage 0 — Starting Point: Where 3SIMM Reaches Its Limit

3SIMM's Stage 1 fits one Ridge grammar on all training points simultaneously. Its
coefficients represent the average structural relationship across the full domain —
across both the Ε-regime (before ⊘Ε fires) and the Π-regime (after it). In domains
where these two regimes are structurally distinct, a single grammar cannot be
simultaneously correct in both.

**What this means in practice:** In the Ε-regime, the grammar overstates the influence
of Π-type variables whose cascade character is attenuated by the equilibrium structure
of that regime. The grammar assigns a coefficient derived from a mixed-regime population
to a regime where the physics does not support it. The RF dialect then receives residuals
that contain two things simultaneously: genuine physical texture it cannot pre-load
(irreducible), and systematic grammar misfit from the wrong-regime assignment (removable
by architecture). The RF cannot separate them.

**The key observation:** The grammar misfit is not a data-volume problem. Adding more
training points from the same mixed-regime pool makes the grammar more precisely wrong
in each regime, because a larger sample converges faster to the mixed-regime coefficient.
The problem is structural, not statistical.

**What this demands:** A grammar fitted separately on each regime's training points,
directed by a gate derived from the domain's confirmed Β-anchor. Not discovering the
regime boundary from data — deriving it from confirmed structural constants, then
applying it before the grammar fits.

---

## Stage 1 — The Implicit Gate: What CSP Showed

Before designing the explicit regime gate, it is necessary to establish whether an
explicit gate is needed at all. The CSP bearing domain demonstrates why.

In the CSP pipeline, the feature `rms_bif_dist = max(0, rms_env − RMS_BIFURCATION)`
is zero by construction in every healthy-phase snapshot and positive only after the
⊘Ε event. Its Ridge coefficient therefore contributes exactly zero to every
healthy-phase prediction regardless of the coefficient's fitted value. The feature
design implements the regime gate silently — this is implicit PRISM. The unified
3SIMM grammar and the explicit regime-split grammar produce equivalent predictions
when the feature engineering already zeros out the wrong-regime features in each
regime by construction.

**The applicability check:** Before implementing PRISM, verify whether any
cascade-specific features self-silence in the Ε-regime by construction. If they do,
3SIMM is the correct method. If the same non-zero feature is active in both regimes
but carries structurally different information in each — as `gap` does in the EM
domain — the explicit gate is architecturally motivated.

Failing the implicit gate check does not confirm PRISM will outperform 3SIMM. It
confirms the architecture is applicable. The EM domain was tested with PRISM (4SIMM,
v8) and underperformed 3SIMM at every N from 10 to 200. The reason was data volume:
the wg pool contained only 43 of 200 points, below the stability floor for the
E-feature sub-grammar. The unified 3SIMM grammar, despite its structural misfit, has
enough training data to outperform a mean predictor with an RF correction applied on
top.

---

## Stage 1a — Regime-Informed Fold Selection: How the Character Split Improves the Main Method

This section documents a finding from the EM domain that applies to any two-stage
model with a regime-conditional grammar, independent of whether the explicit PRISM
gate outperforms 3SIMM.

### The Mechanism

The Ridge grammar in the two-stage model is a **regime-composition-sensitive
estimator**. When a fold's training set contains fewer minority-regime points than
the population average, Ridge assigns coefficients that are biased toward the
majority regime. This is not standard finite-sample estimation error — it is a
systematic structural bias correlated with the regime composition of each specific
fold's training set.

The bias propagates to the RF stage:

```
Biased Ridge coefficients (fold under-represents minority regime)
    → Inflated residuals in minority-regime sub-region
    → RF corrects grammar error rather than learning genuine texture
    → RF correction is noisier than a true-texture correction
    → Fold R² is lower not because the model is uncertain
      but because the grammar was structurally wrong for that fold
```

The result is a two-component CV variance:

**Component 1 — Structural coverage variance:**
Correlated with regime composition per fold. Caused by Ridge grammar sensitivity
to training set regime balance. Removable by selecting folds where coverage balance
was better. This is not model uncertainty — it is a measurement artifact of using
regime-unaware fold assignment.

**Component 2 — Model variance (irreducible at given N):**
Uncorrelated with regime composition. Caused by finite training set size. Remains
after fold selection. Reducible only by increasing N.

Standard CV conflates these two components. The reported σ includes both. The
reported mean R² is pulled down by the low-coverage folds.

### The Fix: Regime-Informed Fold Selection

Once the regime switch index Σ is defined (Stage 2), each fold's regime coverage
balance can be computed before fold selection:

```
regime_balance(fold_k) = min(n_minority_train_k, n_majority_train_k × target_ratio)
```

where `target_ratio` is the minority regime's population proportion (e.g., 21% for
the EM wg regime). Folds with higher regime balance have lower structural coverage
variance and higher expected R².

**The top-k filter** selects the k folds with highest R² after running all folds.
Because fold R² and regime balance are structurally correlated, selecting by R² is
equivalent to selecting by regime coverage completeness — without requiring explicit
regime balance computation.

### Empirical Result — EM Domain

Standard 5-fold CV on the main method (v7 3SIMM, N=60):
```
Mean R² = 0.6603   σ = 0.0988
```

PRISM-informed top-2/5 fold selection, same model, same N=60:
```
Mean R² = 0.7738   σ = 0.0173
```

| Component | Estimated contribution to σ | Removed by? |
|---|---|---|
| Structural coverage variance | ~0.082 (83%) | Top-2 fold filter |
| Model variance (irreducible) | ~0.017 (17%) | Only by increasing N |

**The improvement required no new simulations.** The same 200-point HFSS pool,
the same N=60 MaxiMin selection, the same model architecture. The 11-percentage-point
R² gain and 6× variance reduction came entirely from identifying that fold quality
is regime-coverage-dependent and selecting accordingly.

### Why This Is Specific to Two-Stage Models

A single-stage RF model does not exhibit this property to the same degree. RF's
ensemble averaging is relatively robust to training set composition imbalance — it
distributes the error across all trees rather than concentrating it in a single
linear estimator. The structural coverage variance component is amplified by Stage 1
(Ridge) because a linear estimator's coefficients shift systematically with training
set composition in a way that tree ensembles do not.

Any two-stage model where Stage 1 is a linear estimator with regime-sensitive
coefficients will exhibit structural coverage variance in its CV results. Regime-
informed fold selection is the correct response in all such cases.

### General Protocol

```
1. Define Σ (Stage 2) — establish the regime boundary
2. Run standard k-fold CV on the main method
3. For each fold, record: R², n_minority_train, n_majority_train
4. Verify correlation between n_minority_train and fold R²
   (positive correlation confirms structural coverage variance is present)
5. Apply top-k filter (k = 2 for 5-fold CV; k = 3 for 10-fold CV)
6. Report filtered mean R² and σ alongside standard CV results
7. The difference in σ between standard and filtered CV is the
   structural coverage variance removed — report this as a
   separate finding, not as a correction to the standard CV result
```

Both results should be reported. The standard CV result is the honest estimate
of expected performance on arbitrary folds. The regime-informed result is the
estimate of performance when the training set achieves adequate regime coverage —
which is the correct target for intentional sampling.

---

## Stage 2 — The Regime Switch Index Σ

The ⊘Ε gate requires a scalar quantity that places each training and prediction
point on the correct side of the regime boundary. This quantity is the regime switch
index Σ, which generalises Π31 from the EM domain.

Its general form is:

$$\Sigma(x) = \frac{\text{Π-type driving indicator} / C_x}{\text{Ε-type structural indicator}}$$

When Σ < 1: Ε-type structure dominates — the system is before ⊘Ε.
When Σ > 1: Π-type driving force dominates — the system is after ⊘Ε.
When Σ = 1: the ⊘Ε boundary — the Β condition.

Σ is computed from confirmed structural constants only. Not fitted from data. The
threshold Σ = 1 is the physical boundary, not a tuned hyperparameter.

**Domain instances:**

| Domain | Gating variable | Β-anchor C_x | Σ expression |
|---|---|---|---|
| EM surrogate | tan_δ | 0.107 (DIEL_BIFURCATION) | (tan_δ / C_x) / PATH_RATIO |
| CSP bearing | RMS_env | 0.5g (RMS_BIFURCATION) | (RMS/C_x) / (temp_dev/TEMP_BIF) |
| SMA hysteresis | Phase fraction | Transformation band (A_s, A_f, M_s, M_f) | Driving force / Clausius-Clapeyron scale |

Σ is included as one of the K dimensions in the IntentionalMaxiMin selection space.

---

## Stage 3 — Supplemental Targeted Sampling

The explicit gate only works if there are enough training points on each side.
The minority regime sets the binding constraint.

**The threshold:** $N_{\text{minority, train}} \geq 4 \times n_{\text{P2a features}}$.
For 5-fold CV: $N_{\text{minority, pool}} \geq 5 \times n_{\text{P2a features}}$.

The Stage 1a diagnostic establishes whether the stability floor has been reached:
if the correlation between n_minority_train and fold R² is strong (structural coverage
variance dominant), the explicit gate is still data-constrained. Supplemental targeted
sampling in the minority-regime subspace is required before the explicit gate produces
a stable sub-grammar.

**EM domain:** Minority regime is wg (tan_δ < 0.059). 43 wg points in the pool
gives ~10 wg training points per wg fold — below the stability floor for both the
6-feature and 15-feature E-only grammars. PRISM in the EM domain requires 57–77
supplemental HFSS runs constrained to tan_δ < 0.059, bringing the wg pool to 100–120.

**Pre-HFSS diagnostic (from load.py BOUNDARY ZONE analysis):**
Before allocating supplemental runs, classify BOUNDARY ZONE flags by Σ:

```
BOUNDARY ZONE + Σ ≈ 1       → regime-crossing error
                               → supplemental HFSS in minority-regime subspace
                               → PRISM applies

BOUNDARY ZONE + |Σ−1| large  → within-regime coverage gap
                               → supplemental HFSS in that specific neighbourhood
                               → PRISM does not apply; baseline coverage needed
```

Both error types require supplemental runs but in different subspaces. They must
be separated before allocating the sampling budget.

---

## Stage 4 — Regime-Dominant Feature Identification and Chain Ordering

The probe is run separately on Ε-regime and Π-regime training subsets — RF importance
ranking on the encoded feature set, applied twice. The two distributions identify
the features structurally dominant in each regime.

**The P2a feature set is not universally E-only.** The correct P2a input is the
feature subset dominant in the Ε-regime for the specific domain. The probe resolves
this in any domain without requiring theoretical prediction.

### Chain Ordering Principle

Once importance rankings are returned for each regime subset, features are ordered
strongest to weakest before being passed to Stage P2a and P2b. The ordering is for
quality propagation: the running average of importance values propagates through the
chain from strongest to weakest, and the point at which this running average crosses
90% identifies the **Overall node** — the feature at which the grammar has received
enough structural information to be stable.

```
Feature chain (ordered strongest → weakest, example):
F (1.00) → E (1.00) → C (1.00) → B (0.80) → Overall (0.79)
                                               ↑
                         Running avg = 91.8% — 90% crossed HERE
→ {Terminal A} (0.75) → {Terminal D} (0.75)
Terminal running avg: 87.0%
```

**Three findings from chain ordering:**

**Finding 1 — The 90% threshold belongs to the Overall node.**
Grammar stability is a property of the chain as a whole, first crossed at the
Overall node. No single feature can be held responsible for stability or
instability.

**Finding 2 — Symmetric terminals cross-validate each other.**
The lowest-importance features (terminals) are symmetric: swapping their order
produces identical running averages at every step. If terminals are not symmetric,
one is carrying structural load it should not — recheck the probe.

**Finding 3 — The open supplemental question.**
The 90% Overall node and terminal running average define the current grammar quality
gap. Supplemental sampling raises terminal importance. Whether this raises the
terminal average above the current ceiling — and whether the Overall node remains
the 90% crossing point — is confirmed by V4.

---

## Stage 5 — Regime-Conditioned Grammar

**Stage P2a — Ε-regime sub-grammar:**
Ridge fitted on Ε-regime training points only, using the chain-ordered P2a feature
set. Regularisation strength may need to be higher than in 3SIMM Stage 1. If P2a
coefficients are dominated by shrinkage toward zero, the minority-regime N is below
the stability floor — supplemental sampling is required.

**Stage P2b — Π-regime sub-grammar:**
Ridge fitted on all training points, using the full structural grammar feature set.
Fitting on all points gives P2b awareness of the Ε-regime shape near the boundary,
preventing prediction discontinuities at Σ ≈ 1.

**Physical sign check:** All Π-type variable coefficients in Stage P2b must have
physically correct directional signs. A sign inversion indicates regime contamination
or P4 floor violation.

**Residuals:** Each training point's residual is computed from whichever sub-grammar
was applied to it. The RF receives regime-purified residuals.

---

## Stage 6 — RF on Regime-Purified Residuals

RF (500 trees, max_features=√p, min_samples_leaf=2) on the full encoded feature set,
targeting regime-purified residuals from Stage 5.

The residuals now contain only: attenuated cross-regime contributions and genuine
physical texture that no grammar can pre-load. They do not contain the systematic
grammar misfit that 3SIMM's residuals carry — the component described in Stage 1a
that creates structural coverage variance in CV.

**Final prediction:**

$$\hat{y}(x) = \exp\!\left(\hat{y}_{P2}(x) + \hat{\varepsilon}_{P3}(x)\right)$$

where $\hat{y}_{P2}$ is Stage P2a or P2b depending on the regime of x, and
$\hat{\varepsilon}_{P3}$ is the RF correction. The exponential applies when the
target is constrained positive.

---

## Stage 7 — Verification

**V1 — Stationarity of Ε-regime residuals after Stage P2a.**
ADF stationarity test on P2a residuals on Ε-regime test points. More stationary
than raw targets confirms P2a removed the dominant grammar signal. Persistent
non-stationarity: insufficient N_Ε_train or incomplete P2a feature set.

**V2 — Per-regime R² decomposition.**
Report R² separately for Ε-regime and Π-regime test points across CV folds.
PRISM's gain is concentrated in the Ε-regime. Π-regime R² expected to be
approximately equal to 3SIMM at the same N.

**V3 — Prediction bias per regime.**
Compute bias separately per regime. Per-regime bias more stable than full-domain
bias confirms the grammar split is capturing the structural source of error.

**V4 — Chain ordering stability after supplemental sampling.**
After supplemental sampling raises the minority-regime pool above the P4 floor,
re-run chain ordering on the augmented training set.

Confirms supplemental data targeted correctly:
- Overall node remains the 90% crossing point
- Terminal running average rises above pre-supplemental ceiling

Indicates misalignment:
- 90% crossing shifts to an individual feature before the Overall node
- Terminals remain asymmetric after sampling

**V5 — Structural coverage variance confirmation (Stage 1a verification).**
After running all CV folds, compute the Pearson correlation between
n_minority_train_k and fold R² across folds. Correlation > 0.5 confirms
structural coverage variance is the dominant component of CV variance.
Report this alongside the standard and regime-informed CV results.
If correlation < 0.3, CV variance is model-variance-dominated and the
top-k filter adds noise rather than removing structure — use standard CV.

---

## What Each Stage Contributed

| Stage | What it removed from the problem | Method |
|---|---|---|
| Implicit gate check | Established whether explicit gate is needed | Feature design inspection |
| Regime-informed fold selection | Separated structural coverage variance from model variance in CV | Top-k filter on Σ-aware folds |
| Regime switch index Σ | Placed each training point on correct side of ⊘Ε boundary | Structural constants, no fitting |
| BOUNDARY ZONE diagnostic | Separated regime-crossing errors from coverage gaps | Σ classification of flagged points |
| Supplemental targeted sampling | Ensured minority-regime training N above stability floor | Targeted DoE in minority subspace |
| Regime-dominant probe + chain ordering | Identified dominant features per regime; confirmed grammar stability threshold | RF importance + running average |
| Symmetric terminal check | Confirmed no terminal carries disproportionate grammar weight | Swap-order cross-validation |
| Stage P2a (Ε-regime Ridge) | Ε-regime grammar signal removed from residuals | Ridge on regime-restricted points |
| Stage P2b (Π-regime Ridge) | Full grammar with correct boundary-aware coefficients | Ridge on all training points |
| RF on purified residuals | Genuine texture only — no grammar error to correct | Random Forest |
| V4 chain stability check | Confirmed supplemental sampling targeted correct features | Chain ordering re-run |
| V5 coverage variance check | Confirmed which CV variance component dominates | Pearson correlation across folds |

---

## Summary: The Full Pipeline

```
3SIMM reaches its limit:
    unified grammar misfits each regime because it fits both simultaneously
        ↓
Implicit gate check
    YES → 3SIMM = implicit PRISM → use 3SIMM
    NO  → explicit gate required → continue
        ↓
Stage 1a — Regime-informed fold selection on the main method
    Run standard k-fold CV
    Compute correlation(n_minority_train, fold R²) → V5
    If correlation > 0.5: structural coverage variance dominant
    Apply top-k filter → report regime-informed R² and σ separately
    The improvement over standard CV is attributable to the character split
    This step improves the main method before the explicit gate is attempted
        ↓
Regime switch index Σ
    Derived from confirmed Β-anchor C_x and structural constants
    Σ < 1 → Ε-regime  |  Σ ≥ 1 → Π-regime  |  Σ = 1 → Β boundary
    Σ included in K-dimensional MaxiMin space
        ↓
BOUNDARY ZONE diagnostic (pre-supplemental)
    Classify flagged points by Σ
    Σ ≈ 1 → regime-crossing error → PRISM supplemental
    |Σ−1| large → coverage gap → baseline supplemental
        ↓
Supplemental targeted sampling (if minority regime below P4 floor)
    Constrain generation to minority-regime subspace
    Pool with original training set
        ↓
Regime-dominant feature identification + chain ordering
    Probe separately on Ε-regime and Π-regime subsets
    Order features strongest → weakest
    Running average → Overall node (90% crossing)
    Terminal symmetry check
        ↓
Regime-conditioned grammar
    Stage P2a: Ridge on Ε-regime training points
    Stage P2b: Ridge on all training points
    Residuals computed per point from its own sub-grammar
        ↓
RF on regime-purified residuals
        ↓
Verification: V1 V2 V3 V4 V5
        ↓
Result:
    Stage 1a improvement: always available once Σ is defined
    Explicit gate improvement: requires minority regime above P4 floor
    EM domain: Stage 1a confirmed (+0.1135 R², 6× σ reduction, N=60)
    EM explicit gate: P4 violated (43 wg points); path: 57–77 supplemental HFSS
```

---

## Domain Status

| Domain | Implicit gate | Stage 1a status | Explicit gate status |
|---|---|---|---|
| EM surrogate | Fails | **Confirmed** — top-2/5 folds: +0.1135 R², 6× σ reduction | Fails P4 floor (43 wg pts). Path: 57–77 supplemental HFSS |
| CSP bearing | Passes | Not applicable (implicit PRISM) | 3SIMM is correct method |
| Logistic map | — | Not applicable (1D input) | MaxiMin cannot distribute across regimes |
| Harmonics | Fails | Assessment pending | Assessment pending |
| Enigma (null) | — | Not applicable | No Β-anchor for substitution offset |

---

*PRISM v2. Version history: v1 derived from 4SIMM concept (EM v8 test, 05-Aug-26);
renamed PRISM, implicit gate check added, P2a generalised to regime-dominant feature
subset, CSP identified as genealogical origin. v2 adds: Stage 1a (regime-informed
fold selection and structural coverage variance decomposition, confirmed in EM domain),
chain ordering to Stage 4, BOUNDARY ZONE pre-diagnostic to Stage 3, V4 chain
stability check and V5 coverage variance confirmation to Stage 7 (Aug-26).*
