# TSA Note — Entropic Gradient and Loss Landscape Character

## The Observation

The loss landscape in a neural network is a high-dimensional surface. Gradient descent
follows local slope without knowing whether that slope leads to a global minimum or a
local trap. Entropic gradient methods — noise injection, annealing, dropout — attempt
to escape local minima by introducing undirected perturbations.

In TSA terms:

| Region | TSA type | Gradient behaviour |
|---|---|---|
| Bowl around a minimum | Ε | Self-correcting — gradient descent converges stably |
| Ridge, plateau, saddle | Π | Cascade away or stall — gradient descent diverges or freezes |
| Saddle point itself | Β | Separatrix — small perturbation determines which basin is reached |

The entropic perturbation is an attempt to artificially trigger ↓Ε at a local minimum
— force the trajectory out of a self-regulating bowl into a cascade that might reach
a better basin. The perturbation is undirected: it does not know whether the escape
direction leads to a better minimum, a worse one, or a plateau. It is a forced ⊘Ε
event without structural knowledge of what is on the other side.

## The TSA Implication

If the local geometry of the loss surface could be classified at each point — genuine
Ε basin (converge) vs false Ε basin (escape required) — the optimiser would know when
to apply the perturbation and in which direction. The regime switch index Σ applied to
the loss landscape would distinguish a global minimum neighbourhood from a local trap
by structural character, not by gradient magnitude alone.

## The Deeper Point

Gradient descent is blind to dynamical character. It follows slope without knowing
whether the slope is Π or Ε. TSA's contribution would be the same as everywhere else:
classify character first, then choose the operation accordingly.

- Descend in confirmed Ε regions
- Perturb at Β (saddle neighbourhoods)
- Escape false-Ε traps by detecting Σ > 1 despite small local gradient

This is why ISPCC outperforms raw gradient-based methods at small N: the encoding
pre-loads structural character so the model does not discover it from gradient signals
alone. Applied to the optimiser itself rather than the feature space, the same
principle would make gradient descent structurally aware rather than geometrically
blind.

## Status

Observation noted. Requires structural constants derivable from loss landscape
geometry for specific architectures before TSA applies formally. The loss landscape
geometry literature is increasingly characterised for specific problem classes —
if those characterisations yield structural constants, the extension is direct.

*Working note — not a proved extension of TSA.*
