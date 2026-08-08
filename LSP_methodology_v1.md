# Language Structure Parser (LSP)
## TSA-Informed Academic Argument Classification and Comparison

---

## Problem Statement

Academic documents contain argument structures with distinct dynamical character.
Claims advance positions irreversibly. Definitions bound terms. Hedges sit at the
boundary between commitment and retraction. Standard text comparison methods operate
on semantic similarity — shared vocabulary, topic overlap, embedding distance. They
do not classify the structural character of the argument itself.

The Language Structure Parser (LSP) applies TSA variable classification to sentence-
level rhetorical features, producing a typed argument representation for each document.
Two documents can then be compared at the level of structural character: where their
cascading claims align or diverge, where they share the same bounded definitions,
and where both hedge on the same unresolved question.

The system runs entirely locally. No external API, no GPU, no large language model.

---

## Structural Constants (Rhetorical, Derived from Argumentation Theory)

All normalisation scales are derived from formal argumentation theory before any
document is examined.

**Π-anchor:** A sentence with maximum epistemic commitment — a direct causal or
existential claim with no qualification. Assertion strength = 1.0.

**Ε-anchor:** A sentence with maximum epistemic containment — a formal definition
or citation of established prior work. Hedge density = 1.0 within the bounded set.

**Β-anchor:** A sentence at the rhetorical separatrix — a concession that partially
affirms and partially retracts, or a research gap statement that neither asserts nor
defines.

**Rhetorical bifurcation constant:** The ratio of Π-signal to Ε-signal at which a
sentence crosses from one regime to the other. Set at 1.5 (Π/Β boundary) and 0.60
(Β/Ε boundary), consistent with the LSP scoring formula below. Subject to calibration
against a reference corpus.

---

## Variable Classification (From Rhetorical Structure)

**π-type (cascade — advances the argument irreversibly):**

| Feature | Rhetorical justification |
|---|---|
| assertion_strength | Density of strong epistemic verbs (demonstrates, proves, shows, confirms, establishes) — accumulates toward a committed position |
| novelty_density | Density of novelty markers (we propose, we introduce, for the first time) — directional, non-returning claim |
| causal_density | Density of causal connectors (therefore, thus, because, consequently) — logical cascade from premise to conclusion |
| sentence_position | Topic sentence of paragraph — primary advancing function |
| negation_strength | Strong negation of prior claims (contradicts, refutes, disproves) — directional reversal, non-returning |

**ε-type (equilibrium — bounds and self-corrects):**

| Feature | Rhetorical justification |
|---|---|
| hedge_density | Density of epistemic hedges (possibly, may, suggests, appears, could) — bounds the claim, self-corrects against overstatement |
| citation_density | Citations per sentence — appeals to bounded established knowledge |
| definition_marker | Presence of definitional structure (is defined as, refers to, we use X to mean) — bounded, convergent |
| elaboration_signal | Elaboration connectors (specifically, for example, that is, namely) — self-correcting, contained within established claim |
| area_containment | Sentence within body of paragraph, not topic or transition position — contained function |

**Β-type markers (boundary — sits at the rhetorical separatrix):**

| Feature | Rhetorical justification |
|---|---|
| contrast_density | Contrast markers (however, nevertheless, although, despite, yet) — regime change signal |
| concession_structure | Concession pattern (while X, Y; although X, Y) — partially affirms, partially retracts |
| gap_marker | Research gap signal (remains unclear, little is known, has not been addressed) — neither asserts nor defines |
| uncertainty_explicit | Explicit uncertainty (it is unclear whether, this raises the question of) — at the decision boundary |

---

## Feature Extraction (Per Sentence)

From each sentence, 14 features are extracted using spaCy for tokenisation, POS
tagging, and dependency parsing. No trained model required beyond the base spaCy
pipeline.

**Π-features (5):** assertion_strength, novelty_density, causal_density,
sentence_position, negation_strength.

**Ε-features (6):** hedge_density, citation_density, definition_marker,
elaboration_signal, area_containment, avg_sentence_length_norm.

**Β-markers (3):** contrast_density, concession_structure, gap_marker.

All features are normalised to [0, 1] using rhetorical constants as scales.
avg_sentence_length_norm is normalised by SENT_LENGTH_SCALE = 60 words (the
approximate upper bound for a single coherent academic sentence).

---

## Pi/e Encoding

The same encoding functions and weights as all ISPCC domains. No domain-specific
tuning.

**Pi-encoding** (for Π-type features):

$$\Phi_\Pi(\tilde{x}) = \left(\frac{5}{11}\sin(\pi\tilde{x}),\ \frac{1}{11}\cos(\pi\tilde{x}),\ \frac{1}{11}\sin(2\pi\tilde{x}),\ \frac{3}{11}\sin(\pi^2\tilde{x}),\ \frac{1}{11}\sin(\pi\tilde{x})\cos(\pi^2\tilde{x})\right)$$

Applied to: assertion_strength, novelty_density, causal_density, sentence_position,
negation_strength.

**E-encoding** (for Ε-type features):

$$\Phi_E(\tilde{x}) = \left(\frac{2}{5}e^{-e\tilde{x}},\ \frac{2}{5}\tilde{x}^e,\ \frac{1}{5}e^{-e(\tilde{x}-0.5)^2}\right)$$

Applied to: hedge_density, citation_density, definition_marker, elaboration_signal,
area_containment, avg_sentence_length_norm.

**Cross-products (Π × Ε):**

Three cross-products encoding rhetorical interaction:
- sin(π × assertion_n) × exp(−e × hedge_n): strong claim modulated by qualification
- sin(π × causal_n) × exp(−e × citation_n): logical cascade modulated by evidence containment
- sin(π × novelty_n) × exp(−e × definition_n): novelty claim modulated by definitional grounding

The full encoded feature set: 25 Π-encoded + 18 Ε-encoded + 3 cross-products = **46
features** per sentence.

---

## Rhetorical Score and Classification

$$S = 0.45 \cdot \bar{\Phi}_\Pi + 0.35 \cdot (1 - \bar{\Phi}_\varepsilon) + 0.20 \cdot \bar{\Phi}_\times$$

where $\bar{\Phi}_\Pi$ is the mean of Π-encoded features, $\bar{\Phi}_\varepsilon$ is
the mean of Ε-encoded features, and $\bar{\Phi}_\times$ is the mean of cross-product
features.

**Classification thresholds:**

| Score | TSA type | Rhetorical character |
|---|---|---|
| S > 1.5 | Π | Cascading claim — advances argument irreversibly |
| 0.60 ≤ S ≤ 1.5 | Β | Boundary sentence — hedge, concession, gap statement |
| S < 0.60 | Ε | Equilibrium sentence — definition, elaboration, citation |

**User overrides:**

`--assert SENT_ID`: Force Π regardless of score. For sentences where the analyst
asserts directional function independent of surface markers.

`--bound SENT_ID`: Force Ε regardless of score. For definitional sentences with
atypical surface form.

`--flag SENT_ID`: Force Β regardless of score. For sentences the analyst is uncertain
about — classification is held for review.

---

## Document-Level Argument Representation

Once all sentences are classified, each document is represented as a typed argument
graph:

- **Nodes:** sentences, typed as Π, Ε, or Β
- **Edges:** sequential adjacency and logical dependency (subject to dependency parse)
- **Graph character:** derived by CASCADE ⊕ across connected nodes

Document-level TSA type is computed by applying the CASCADE operation across all
sentence types in the document. A predominantly Π document is making a sustained
directional argument. A predominantly Ε document is establishing bounded context.
A Β-heavy document is sitting at multiple unresolved boundaries simultaneously.

**Section-level typing** follows document structure conventions:

| Section | Expected TSA type | Rhetorical function |
|---|---|---|
| Abstract | Β | Boundary summary — neither full cascade nor full containment |
| Introduction | Ε → Π | Context establishment then directional commitment |
| Method | Ε | Bounded, reproducible, self-correcting |
| Results | Π | Directed, accumulating, non-returning |
| Discussion | Β | At the boundary between what is proved and what is not |
| Conclusion | ↓Π or ↓Ε | COMPLETE — cascade resolved or hedged back to equilibrium |

---

## Two-Document Comparison

Given two typed argument graphs A and B, the comparison produces four outputs.

**1. Cascade alignment (Π ∩ Π):**

Π sentences from document A compared against Π sentences from document B by cosine
similarity in the encoded feature space. High similarity: both documents advance the
same directional claim. Low similarity: the cascading arguments point in different
directions. This is agreement vs disagreement at the level of primary assertion.

**2. Definitional alignment (Ε ∩ Ε):**

Ε sentences from A compared against Ε sentences from B. High similarity: shared
definitional ground — both documents operate within the same bounded conceptual space.
Low similarity: terminological conflict — the documents use different boundaries for
the same conceptual territory.

**3. Open question overlap (Β ∩ Β):**

Β sentences from A compared against Β sentences from B. Overlap identifies questions
both authors recognise as unresolved. This is the shared gap space — where a third
document or empirical result would be most structurally productive.

**4. Orthogonal structure (MaxiMin in encoded space):**

IntentionalMaxiMin applied across both documents' encoded sentence vectors finds
the maximally structurally distant sentence pairs — the points where the two arguments
are not merely in disagreement but are operating in orthogonal rhetorical regimes.
These are the sentences that are most structurally incompatible: not because they
say opposite things, but because one is a cascade claim and the other is a definitional
containment of the same concept.

---

## Sentence Recommendation

For a query sentence q (typed and encoded), the system finds the k most structurally
similar sentences across both documents by cosine similarity in the encoded feature
space. Similarity is structural, not semantic: a Π sentence making a causal claim
in document A finds the most similar Π sentence in document B regardless of shared
vocabulary.

Output: ranked list of (sentence, document, structural similarity score, TSA type
match).

---

## Probe (Structural Confirmation)

The RF probe is applied to confirm that the variable classification is structurally
correct for academic text. Expected result: Π-encoded features dominate importance
for Π-classified sentences; Ε-encoded features dominate for Ε-classified sentences.

If cross-product features dominate globally, the document contains predominantly
Β-character argument structure — neither cascade nor equilibrium dominates, and the
argument is at multiple simultaneous boundaries. This is the correct null result for
a document that hedges throughout.

---

## Implementation Stack (Local)

| Component | Library | Function |
|---|---|---|
| PDF parsing | pdfplumber or PyMuPDF | Extract raw text and section structure |
| Tokenisation and POS | spaCy (en_core_web_sm) | Sentence boundary, dependency parse, POS tags |
| Feature extraction | Python (regex + spaCy) | 14 rhetorical features per sentence |
| Encoding | NumPy | Pi/e encoding, cross-products |
| Probe | scikit-learn RF | Importance confirmation |
| Comparison | NumPy (cosine similarity) | Cross-document structural comparison |
| MaxiMin | NumPy | Orthogonal structure detection |

No internet connection required after initial spaCy model download. Full pipeline
runs on a standard laptop CPU. Processing time scales with document length —
approximately linear in sentence count.

---

## Validation Protocol

**Unit test:** Classify sentences from a set of known rhetorical types — a formal
definition, a strong causal claim, a concession, a research gap statement. Confirm
the probe returns the expected TSA type with the expected dominant feature group.

**Cross-document test:** Apply to two papers from the same field taking opposing
positions on a known debate. Confirm that cascade alignment (Π ∩ Π) returns low
similarity for the main claims and that Β ∩ Β returns high similarity for the shared
open questions.

**Threshold validation:** Calibrate the 1.5 and 0.60 score thresholds against a
manually annotated sentence corpus. This is the rhetorical equivalent of solver
validation in the mesh probe — the thresholds are engineering rules until validated
against a reference annotation.

---

## Relationship to ISPCC Framework

LSP is the first ISPCC application in the symbolic rather than numerical domain.
Physical variables have numerical values encoded by pi/e basis functions. Sentences
have rhetorical character classified by the same typed feature extraction mechanism.
The structural constants are rhetorical rather than physical, but their role is
identical: they normalise raw features into dimensionless ratios with fixed structural
meaning before any document is examined.

The domain-agnostic claim extends to natural language: the same algebra, the same
encoding functions, the same probe mechanism, applied to a domain where the variables
are linguistic and the constants are derived from argumentation theory rather than
physics or mathematics.

---

*Working methodology — threshold validation pending reference corpus.*
