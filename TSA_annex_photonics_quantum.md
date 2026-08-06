# TSA Annex — Structural Compatibility Notes: Photonics and Quantum Systems

**Companion to TSA Methodology v4**

These notes record structural compatibilities between the TSA algebra and established phenomena in photonics and quantum mechanics. They are not proofs and do not constitute a photonic or quantum extension of TSA. They establish that the algebra's type system and operations admit consistent interpretations in these domains, and identify where formal development would be productive.

---

## P1 — Photonic Circuits

### P1.1 Passive Elements: ↓-governed

A guided photonic mode in a waveguide satisfies the Ε-type conditions: it is bounded by the confinement structure, self-regulating (phase accumulates but field remains contained), and convergent to the guided field distribution under perturbation below cutoff.

Natural COMPLETE (↓) governs these elements. ↓Ε = Ε: a photon in a waveguide left below threshold remains guided. The field is at its natural attractor.

Waveguide propagation, directional couplers below the coupling threshold, and Fabry-Pérot cavities below the lasing threshold are all ↓-governed elements — their behaviour is determined by the natural attractor of the field distribution.

### P1.2 Active Thresholds: ⊘-governed

Mode cutoff is the photonic ⊘Ε event: the confinement condition is violated and the guided mode radiates. The guided field (Ε-type, self-regulating below cutoff) is forced through the cutoff threshold (its Β-anchor) and enters the radiation regime (Π-type, non-returning, cascading into free space). In TSA: ⊘Ε = Π.

Active modulators, switches, and couplers operated above threshold are ⊘-governed elements. Their operation is not a natural evolution of the field — it is a forced threshold crossing at a design-specified Β-anchor. The distinction between ↓-governed and ⊘-governed elements is the structural distinction between passive and active components in a photonic circuit.

### P1.3 Detection: ⊘Π = ∅

A photodetector absorbs an incoming photon and converts it to an electrical signal. The photon exits the photonic domain. In TSA: ⊘Π = ∅. The cascade (propagating field, Π-type in the sense of directed non-returning energy transport) is forced through the absorption threshold and exits the algebra entirely. The ∅ terminal corresponds to the classical electrical output — outside the photonic TSA domain.

This gives a three-class taxonomy for photonic circuit elements:
- **Passive** (waveguides, resonators, splitters below threshold): ↓-governed
- **Active** (modulators, switches, couplers above threshold): ⊘-governed
- **Terminal** (detectors, absorbers): ⊘Π = ∅

### P1.4 The Β-type Junction

The coupler or beam splitter at exactly 50/50 splitting is the Β-type element: it is at the structural boundary between full transmission (Ε-type, self-regulating toward guided confinement) and full reflection (Π-type, non-returning loss or radiation). Operating at the Β condition, it routes field power into two equal output paths.

The formal photonic circuit description on top of TSA will treat each circuit element as a typed operation, composed according to the TSA rules. This development is reserved for the separate photonic gates document.

---

## Q1 — Quantum Systems

### Q1.1 Superposition as Β-type

A qubit in superposition α|0⟩ + β|1⟩ is at the boundary between its two definite states |0⟩ and |1⟩. It is neither self-regulating toward |0⟩ (Ε-type) nor cascading toward |1⟩ (Π-type) — it is at the structural transition between the two. In TSA: the superposition state has character **Β**.

This is not an analogy. The Β-type conditions as defined in TSA — neither accumulating nor self-correcting, the separatrix from which trajectories diverge toward either character under perturbation — are precisely the conditions of quantum superposition before measurement. A superposition is exactly at the boundary from which any perturbation (measurement interaction) resolves it toward a definite outcome.

### Q1.2 Measurement as ⊘Β

Measurement is the forced COMPLETE operation on a Β-type state. The measurement interaction forces the superposition through the decision boundary and resolves it to a definite outcome: ⊘Β → Ε or Π depending on the measurement basis.

The directional resolution of ⊘Β — which is Q7 in TSA's open questions — has a natural answer in the quantum context: the measurement basis choice determines the direction. Measuring in the |0⟩/|1⟩ computational basis forces resolution toward Ε (ground state) or Π (excited state). Measuring in a different basis rotates the boundary and produces a different resolution direction. The basis parameter for ⊘Β that TSA currently leaves open is, in quantum mechanics, the measurement operator.

This structural correspondence does not recover the Born rule — TSA operates on types, not amplitudes, and has no probabilistic content. What it recovers is the type-level architecture of collapse: a Β-type state forced through a measurement boundary resolves to one of the two extreme types, with the resolution direction set by a basis parameter external to the algebra.

### Q1.3 Entanglement and Β ⊕ Β

TSA Axiom TSA5 states Β ⊕ Β = Π. The CASCADE of two boundary-type states produces cascade character — the combined state has non-returning, path-dependent character irreducible to either input.

Two qubits in superposition (each Β-typed) combined through an entangling gate (CNOT or equivalent) produce an entangled state whose measurement outcomes are correlated in a way that cannot be reduced to the individual qubits' pre-measurement characters. The combined state has Π-type character at the measurement-correlation level: observing one qubit immediately and irreversibly determines the correlated outcome of the other, a non-returning cascade of information.

The algebraic structure Β ⊕ Β = Π is compatible with this — two boundary states combining to produce an irreducible cascade character. The entangled state is not merely "two superpositions at once"; it has a new character type that TSA's Β ⊕ Β = Π expresses correctly at the level of state character.

### Q1.4 Decoherence as ⊘Ε

A quantum system maintaining coherence over a finite decoherence timescale τ is Ε-type with respect to that timescale: it self-regulates its phase relationships, bounded by the coherence envelope. As environmental coupling exceeds the decoherence threshold, the system crosses its coherence Β-anchor.

Decoherence is the forced COMPLETE event on the coherent state: ⊘Ε = Π. The self-regulating phase relationships are forced through their threshold and enter the cascade regime of classical noise — non-returning, non-correcting, irreversible. The transition from quantum coherence to classical mixed state is a ⊘Ε event.

This is consistent with the known direction of decoherence: it is irreversible in the absence of active error correction, accumulating environmental entanglement in a cascade that does not self-correct. The Π character of the decohered state is the correct TSA assignment.

---

## Summary of Structural Correspondences

| TSA element | Photonic interpretation | Quantum interpretation |
|---|---|---|
| Ε-type | Guided mode below cutoff | Ground state |0⟩; coherent superposition w.r.t. τ |
| Π-type | Radiating mode; propagating field | Excited state |1⟩; decohered mixed state |
| Β-type | 50/50 coupler; at cutoff | Superposition α|0⟩+β|1⟩ |
| ↓ (natural) | Passive propagation | Free evolution under Hamiltonian |
| ⊘Ε = Π | Mode cutoff; modulator above threshold | Decoherence event |
| ⊘Π = ∅ | Photodetection; absorption | — |
| ⊘Β (open) | Active switching at 50/50 point | Measurement collapse |
| Β ⊕ Β = Π | — | Entangling gate on two superpositions |
| ∅ (terminal) | Classical electrical output from detector | Classical measurement outcome |

---

## Note on Scope

These correspondences are structural and operate at the level of character classification. TSA makes no claims about quantum amplitudes, probabilities, or the specific physical mechanisms of photonic propagation. The formal photonic circuit description — with gates, composition rules, and circuit diagrams — is reserved for the photonic extension document, which will build on the TSA algebra as its algebraic foundation. The quantum correspondences are noted here as compatible structural observations. Extending TSA to a full quantum type system would require, at minimum, resolving ⊘Β formally (Q7) and introducing the basis parameter that measurement introduces into the forced COMPLETE operation.

---

*Annex to TSA Methodology v4.*
