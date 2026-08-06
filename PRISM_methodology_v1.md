# PRISM — Predictive Regime-split Intentional Symbolic MaxiMin
## Method Specification v1

**Position:** PRISM is a method within the ISPCC framework, sitting alongside 3SIMM.

| Layer | Name | Role |
|---|---|---|
| Theorem | TSA | Trinary Symbolic Algebra |
| Framework | ISPCC | Intentional Symbolic Pre-Cognitive Computing |
| Method (budget-constrained) | 3SIMM | 3 Staged Intentional MaxiMin |
| Method (data-rich) | **PRISM** | Predictive Regime-split Intentional Symbolic MaxiMin |

PRISM and 3SIMM share the same ISPCC foundation — structural constants, TSA variable classification, pi/e encoding, and K-dimensional IntentionalMaxiMin. They differ at the grammar stage, and that difference is the subject of this document.

---

## Stage 0 — Starting Point: Where 3SIMM Reaches Its Limit

3SIMM's Stage 1 fits one Ridge grammar on all training points simultaneously. Its coefficients represent the average structural relationship across the full domain — across both the Ε-regime (before ⊘Ε fires) and the Π-regime (after it). In domains where these two regimes are structurally distinct, a single grammar cannot be simultaneously correct in both.

**What this means in practice:** In the Ε-regime, the grammar overstates the influence of Π-type variables whose cascade character is attenuated by the equilibrium structure of that regime. The grammar assigns a coefficient derived from a mixed-regime population to a regime where the physics does not support it. The RF dialect then receives residuals that contain two things simultaneously: genuine physical texture it cannot pre-load (irreducible), and systematic grammar misfit from the wrong-regime assignment (removable by architecture). The RF cannot separate them.

**The key observation:** The grammar misfit is not a data-volume problem. Adding more training points from the same mixed-regime pool makes the grammar more precisely wrong in each regime, because a larger sample converges faster to the mixed-regime coefficient. The problem is structural, not statistical.

**What this demands:** A grammar fitted separately on each regime's training points, directed by a gate derived from the domain's confirmed Β-anchor. Not discovering the regime boundary from data — deriving it from confirmed structural constants, then applying it before the grammar fits.

---

## Stage 1 — The Implicit Gate: What CSP Showed

Before designing the explicit regime gate, it is necessary to establish whether an explicit gate is needed at all. The CSP bearing domain demonstrates why.

In the CSP pipeline, the feature `rms_bif_dist = max(0, rms_env − RMS_BIFURCATION)` is zero by construction in every healthy-phase snapshot and positive only after the ⊘Ε event (RMS crossing 0.5g). Its Ridge coefficient therefore contributes exactly zero to every healthy-phase prediction regardless of the coefficient's fitted value. The feature design implements the regime gate silently — the healthy-phase grammar is automatically restricted to the non-cascade features without any explicit split in the model architecture. This is implicit PRISM. The unified 3SIMM grammar and the explicit regime-split grammar produce equivalent predictions when the feature engineering already zeros out the wrong-regime features in each regime by construction.

**The applicability check:** Before implementing PRISM, verify whether any cascade-specific features self-silence in the Ε-regime by construction (i.e., are defined as `max(0, x − C_x)` or equivalent). If they do, and if they cover the regime-specific grammar difference, the explicit gate adds no predictive value. If the same non-zero feature is active in both regimes but carries structurally different information in each — as `gap` does in the EM domain, where the waveguide attenuates its cascade influence in the wg regime while the unified Ridge assigns it the full mixed-regime coefficient — the explicit gate is architecturally motivated and the implicit gate check is failed.

This check is the first step. CSP passes it by already having implicit PRISM. The EM domain fails it — gap is non-zero in both regimes and carries structurally different physics in each — making PRISM architecturally motivated there.

Failing the implicit gate check does not confirm PRISM will outperform 3SIMM. It confirms the architecture is applicable. The EM domain was tested with PRISM (4SIMM, v8) and underperformed 3SIMM at every sample size from N=10 to N=200. The reason was not architectural — the regime split and E-only grammar are structurally correct for the wg regime — but data volume: the wg pool contained only 43 of 200 points, giving roughly 17 wg training points per CV fold, below the stability floor for the E-feature sub-grammar. Below that floor, Stage P2a converges toward the wg log-mean rather than learning a grammar, and the RF receives the full wg signal as its residual target rather than regime-purified residuals. The unified 3SIMM grammar, despite its structural misfit, has enough training data to outperform a mean predictor with an RF correction applied on top.

The EM PRISM result therefore confirms two things simultaneously: the architecture is correct (the regime split is motivated by the physics), and the data requirement is binding (it cannot be bypassed by architectural correctness alone). For EM, the path to a working PRISM is supplemental wg-targeted sampling, not a change to the model structure.

---

## Stage 2 — The Regime Switch Index Σ

The ⊘Ε gate requires a scalar quantity that places each training and prediction point on the correct side of the regime boundary. This quantity is the regime switch index Σ, which generalises Π31 from the EM domain and the regime switch index from the CSP bearing domain.

Its general form is:

$$\Sigma(x) = \frac{\text{Π-type driving indicator} / C_x}{\text{Ε-type structural indicator}}$$

When Σ < 1: the Ε-type structure dominates — the system is in the Ε-regime, before ⊘Ε.
When Σ > 1: the Π-type driving force dominates — the system is in the Π-regime, after ⊘Ε.
When Σ = 1: the ⊘Ε boundary — both contributions equal, the Β condition.

Σ is computed from confirmed structural constants only. It is not fitted from data. The threshold value Σ = 1 is the physical boundary, not a tuned hyperparameter.

**Domain instances:**

| Domain | Gating variable | Β-anchor C_x | Σ expression |
|---|---|---|---|
| EM surrogate | tan_δ | 0.107 (DIEL_BIFURCATION) | (tan_δ / C_x) / PATH_RATIO |
| CSP bearing | RMS_env | 0.5g (RMS_BIFURCATION) | (RMS/C_x) / (temp_dev/TEMP_BIF) |
| SMA hysteresis | Phase fraction | Transformation band (A_s, A_f, M_s, M_f) | Driving force / Clausius-Clapeyron scale |

Σ is included as one of the K dimensions in the IntentionalMaxiMin selection space. This ensures the greedy MaxiMin distributes training points across the ⊘Ε boundary as part of its structural coverage objective, not as an afterthought.

---

## Stage 3 — Supplemental Targeted Sampling

The explicit gate only works if there are enough training points on each side of it. The minority regime — the smaller of the two regime populations in the training pool — sets the binding constraint.

The minimum requirement is straightforward. Ridge with L2 regularisation can technically operate with fewer training points than parameters, but below approximately 4× the number of P2a features, the dominant contribution to the fitted coefficients comes from shrinkage toward zero rather than from structural signal in the data. The grammar converges toward predicting the minority-regime mean. This is what the EM 4SIMM test demonstrated: the wg pool (43 of 200 points) gave roughly 17 wg training points per CV fold against 6–15 E-features, which is below the stability floor by a factor of 2–5. The result was indistinguishable from a mean predictor in the wg regime, which is why all four 4SIMM variants underperformed the unified 3SIMM grammar.

**The threshold:** $N_{\text{minority, train}} \geq 4 \times n_{\text{P2a features}}$. For 5-fold CV: $N_{\text{minority, pool}} \geq 5 \times n_{\text{P2a features}}$.

When the standard DoE or measurement protocol undersamples the minority regime, the required action is supplemental targeted sampling within the minority-regime subspace — the set of input values satisfying Σ(x) on the minority side of C_x. The supplemental points are pooled with the original training set before K-dimensional MaxiMin selection. No changes to the model architecture are required.

**EM domain example:** Minority regime is wg (tan_δ < 0.059). The 4SIMM test (v8, 05-Aug-26) confirmed the failure mode precisely: with 43 wg points in the pool, MaxiMin selects approximately 17 wg training points per CV fold, which is below the stability floor for both the 6-feature and 15-feature E-only grammars. All four 4SIMM variants underperformed 3SIMM at every tested N (10 to 200). PRISM in the EM domain requires 57–77 supplemental HFSS runs constrained to tan_δ < 0.059, bringing the wg pool to 100–120 before the explicit gate produces a stable sub-grammar.

In domains where data is computationally free to generate, the supplemental sampling problem disappears — the minority regime can be over-sampled deliberately at zero marginal cost, and the regime split is the only architectural decision that matters.

---

## Stage 4 — Regime-Dominant Feature Identification

Before fitting either sub-grammar, the probe is run separately on Ε-regime and Π-regime training subsets. This is the same probe mechanism used throughout ISPCC — RF importance ranking on the encoded feature set — applied twice: once restricted to points with Σ < 1 (Ε-regime), once restricted to points with Σ ≥ 1 (Π-regime).

The two importance distributions identify the features that are structurally dominant in each regime. These are the inputs to Stage P2a and Stage P2b respectively.

**The P2a feature set is not universally E-only.** This is the key finding from the CSP analysis. The correct P2a input is the feature subset dominant in the Ε-regime for the specific domain — which may be E-encoded variables, or Π-type variables specific to the pre-⊘Ε phase, or both:

- In the EM domain, the Ε-regime (waveguide active) is E-feature-dominant: standing-wave resonance in the rubber layers governs SAR-proxy variation. P2a uses E-encoded layer thickness features. Gap is non-zero but attenuated; its attenuated contribution goes to the RF as a residual.

- In the CSP bearing domain, the Ε-regime (healthy phase) is Π-feature-dominant: `life_frac` governs rul_norm variation before the cascade starts. P2a in CSP would use `life_frac` as its dominant feature and exclude `rms_bif_dist` and `regime_switch`, which are structurally zero or uninformative in the healthy phase. This is why CSP satisfies the implicit gate check and does not require PRISM — the feature engineering already performs this exclusion through the `max(0, ...)` construction.

The probe output resolves this in any domain: it returns the actual importance distribution for the regime subset, not the theoretical TSA expectation. The probe result confirms or revises the analytical prediction.

---

## Stage 5 — Regime-Conditioned Grammar

With the regime-dominant feature sets identified, the Ridge grammar is fitted separately for each regime.

**Stage P2a — Ε-regime sub-grammar:**

Ridge fitted on Ε-regime training points only, using the P2a feature set identified in Stage 4. Because P2a trains on the minority-regime subset rather than the full training pool, regularisation strength may need to be higher than in 3SIMM Stage 1 — the exact value is domain-dependent and is set by inspecting coefficient stability across CV folds. In the EM domain, the Ε-regime grammar uses E-encoded layer thickness features; layer resonance governs SAR-proxy variation in the waveguide-active regime.

**Physical check:** If P2a coefficients are dominated by regularisation shrinkage toward zero — all coefficients small, predictions near the Ε-regime log-mean — the minority-regime training N is below the stability floor. Supplemental sampling is required. This failure mode is distinct from a structural failure: the feature set may be correct but underpowered by data volume.

**Stage P2b — Π-regime sub-grammar:**

Ridge fitted on all training points, using the full structural grammar feature set — the same input and regularisation as 3SIMM Stage 1, including Σ.

Fitting on all training points, not only Π-regime points, gives Stage P2b awareness of the Ε-regime shape near the boundary. Ε-regime training points inform Ridge that cascade-specific features carry less signal there, drawing coefficients toward physically correct values across the boundary and preventing prediction discontinuities at Σ ≈ 1.

**Physical sign check:** all Π-type variable coefficients in Stage P2b must have physically correct directional signs. A sign inversion indicates regime contamination or P4 floor violation.

**Residuals for the RF:** Each training point's residual is computed from whichever sub-grammar was applied to it. The RF receives regime-purified residuals — residuals no longer contaminated by the cross-regime coefficient assignment error.

---

## Stage 6 — RF on Regime-Purified Residuals

The RF stage is structurally identical to 3SIMM Stage 2. RF (500 trees, max_features=√p, min_samples_leaf=2) on the full encoded feature set, targeting the regime-purified residuals from Stage 5.

**What the residuals now contain:** In the Ε-regime, Stage P2a has removed the dominant regime-specific grammar signal. What reaches the RF is the attenuated cross-regime contribution (e.g., gap's dampened influence in the EM wg regime) and genuine physical texture that no grammar can pre-load — resonance peaks, near-field transitions, domain-specific nonlinear interactions. These are structurally smaller and more local than the residuals the unified 3SIMM grammar leaves in the same regime.

**What the residuals do not contain** that 3SIMM's residuals do: the systematic grammar misfit from applying a mixed-regime coefficient to a single-regime prediction. That component is removed by the explicit gate. The RF is not asked to correct a grammar error — it is asked only to learn what the grammar cannot reach.

**Final prediction:**

$$\hat{y}(x) = \exp\!\left(\hat{y}_{P2}(x) + \hat{\varepsilon}_{P3}(x)\right)$$

where $\hat{y}_{P2}$ is Stage P2a or P2b depending on the regime of x, and $\hat{\varepsilon}_{P3}$ is the RF correction. The exponential applies when the target is constrained positive; it is omitted when the target is defined on ℝ.

---

## Stage 7 — Verification

Three checks confirm that the regime split is doing structural work after the first PRISM CV run.

**V1 — Stationarity of Ε-regime residuals after Stage P2a.** Apply an ADF stationarity test to Stage P2a residuals on Ε-regime test points. If Stage P2a has removed the dominant Ε-regime grammar signal, these residuals are more stationary than the raw Ε-regime targets. Persistent non-stationarity points to either insufficient N_Ε_train or an incomplete P2a feature set — the probe on the Ε-regime subset should be rerun to check for missing features.

**V2 — Per-regime R² decomposition.** Report R² separately for Ε-regime and Π-regime test points across CV folds. PRISM's gain relative to 3SIMM is concentrated in the Ε-regime, where the unified grammar misfits. Π-regime R² is expected to be approximately equal to 3SIMM at the same N.

**V3 — Prediction bias per regime.** Where the domain has a known systematic prediction direction (underprediction or overprediction of extreme configurations), compute the bias separately per regime. A per-regime bias that is more stable than the full-domain bias confirms the grammar split is capturing the structural source of the error rather than averaging across structurally different failure modes.

---

## What Each Stage Contributed

| Stage | What it removed from the problem | Method |
|---|---|---|
| Implicit gate check | Established whether explicit gate is needed | Feature design inspection |
| Regime switch index Σ | Placed each training point on the correct side of the ⊘Ε boundary | Structural constants, no fitting |
| Supplemental sampling | Ensured minority-regime training N above stability floor | Targeted DoE in minority subspace |
| Regime-dominant probe | Identified which features govern the target in each regime | RF importance on regime subsets |
| Stage P2a (Ε-regime Ridge) | Ε-regime dominant grammar signal removed from residuals | Ridge on regime-restricted training points |
| Stage P2b (Π-regime Ridge) | Full grammar with correct boundary-aware coefficients | Ridge on all training points |
| RF on purified residuals | Attenuated cross-regime contributions + genuine contextual texture | Random Forest on full encoded set |

---

## Summary: The Full Pipeline

```
3SIMM reaches its limit:
    unified grammar misfits each regime because it fits both simultaneously
        ↓
Implicit gate check
    does the feature design already zero out wrong-regime features by construction?
    YES → 3SIMM = implicit PRISM → use 3SIMM
    NO  → explicit gate required → continue
        ↓
Regime switch index Σ
    derived from confirmed Β-anchor C_x and structural constants
    Σ < 1 → Ε-regime (before ⊘Ε)
    Σ ≥ 1 → Π-regime (after ⊘Ε)
    Σ included in K-dimensional MaxiMin space
        ↓
Supplemental targeted sampling (if minority regime below P4 floor)
    constrain generation to minority-regime subspace Σ(x) < 1 (or > 1)
    pool with original training set
        ↓
Regime-dominant feature identification
    probe separately on Ε-regime and Π-regime subsets
    P2a feature set = dominant features in Ε-regime subset
    P2b feature set = full structural grammar (same as 3SIMM Stage 1)
        ↓
Regime-conditioned grammar
    Stage P2a: Ridge on Ε-regime training points → Ε-regime grammar
    Stage P2b: Ridge on all training points → Π-regime grammar
    Residuals computed per point from its own sub-grammar
        ↓
RF on regime-purified residuals
    same architecture as 3SIMM Stage 2
    residuals no longer contain grammar misfit
        ↓
Verification
    V1: ADF stationarity of Ε-regime residuals
    V2: per-regime R² decomposition
    V3: per-regime prediction bias stability
        ↓
Result: expected improvement concentrated in Ε-regime
        Π-regime performance approximately equal to 3SIMM
        EM domain: implicit gate check failed (gap active in both regimes)
        PRISM tested (4SIMM v8) and underperformed 3SIMM at all N — P4 violated (43 wg points)
        path to retest: 57–77 supplemental HFSS runs in wg subspace
        No successful PRISM run yet achieved in any domain
```

---

## Domain Status

| Domain | Implicit gate check | Minority regime | Status |
|---|---|---|---|
| EM surrogate | Fails — gap non-zero in both regimes | wg (43/200 points) | **PRISM tested (4SIMM v8) and fails** — underperforms 3SIMM at all N from 10 to 200 including full pool; wg pool (43/200) below P4 floor; explicit gate architecturally correct but data-volume constraint not satisfied at current DoE |
| CSP bearing | Passes — rms_bif_dist zeros in healthy phase | — | 3SIMM is correct method |
| Logistic map | — | — | 1D input; MaxiMin cannot distribute across regimes |
| Harmonics | Fails — q active in both regimes | Low-q consonant subset | Assessment pending |

| Enigma (null test) | — | — | No Β-anchor for substitution offset; not applicable |

---

*PRISM v1. Version history: derived from 4SIMM concept (EM v8 test, 05-Aug-26); renamed PRISM and generalised to domain-agnostic method specification; implicit gate check from CSP analysis added, P2a generalised from E-only to regime-dominant feature subset, CSP identified as genealogical origin (05-Aug-26).*
