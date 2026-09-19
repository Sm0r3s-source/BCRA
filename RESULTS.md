# BCRA v1 Results

This document summarizes the principal experimental findings that led to the frozen BCRA v1.0.0 architecture.

BCRA was developed through a sequence of controlled experiments examining recurrent dynamics, biological topology, topology perturbation, temporal memory, interference, and sequence processing.

The complete machine-readable experiment reports should be treated as the primary record of numerical results.

---

## Final BCRA v1 operating regimes

BCRA v1.0.0 contains two validated operating regimes:

### BCRA-Native

Uses the retained biological connectome topology without topology relaxation.

### BCRA-Relaxed10

Uses the same BCRA architecture with a 10% global destination-permutation topology relaxation.

BCRA-Relaxed10 was selected before the final confirmation experiment based on the preceding topology-dissection studies.

---

# Final confirmation experiment

The final confirmation study used:

- the full retained connectome;
- 138,584 neurons;
- 3,732,460 directed edges;
- 16 fresh paired evaluation seeds;
- frozen recurrent cores;
- no topology-fraction tuning;
- no recurrent-dynamics tuning.

Compared systems included:

- BCRA-Relaxed10 with leaky-tanh dynamics;
- BCRA-Native with leaky-tanh dynamics;
- BCRA-Native with soft-reset LIF dynamics;
- a conventional ESN baseline;
- a zero-recurrence sanity control.

---

## Delayed-memory results

Mean memory balanced scores:

| System | Memory balanced score |
|---|---:|
| BCRA-Relaxed10 | 0.4623 |
| BCRA-Native / leaky tanh | 0.3781 |
| BCRA-Native / soft-reset LIF | 0.3676 |
| ESN baseline | 0.3420 |
| Zero recurrence | 0.03125 |

BCRA-Relaxed10 exceeded BCRA-Native/leaky in all 16 paired seeds.

Mean paired difference:

`+0.0842`

Holm-adjusted exact paired sign-flip p-value:

`0.0001526`

BCRA-Relaxed10 also exceeded the soft-reset-LIF BCRA condition in all 16 paired seeds.

Mean paired difference:

`+0.0947`

Holm-adjusted p-value:

`0.0001526`

---

## Clean temporal memory

BCRA-Relaxed10 achieved:

- clean delayed-recall AUC: `0.6483`
- pooled-time decoder AUC: `0.5891`

BCRA-Native/leaky achieved:

- clean delayed-recall AUC: `0.5102`
- pooled-time decoder AUC: `0.4555`

This indicates that modest topology relaxation substantially increased clean temporal decodability under the frozen leaky-tanh dynamics.

---

## Interference tradeoff

The topology relaxation did not improve every property.

Interference AUC:

| System | Interference AUC |
|---|---:|
| BCRA-Native / soft-reset LIF | 0.3540 |
| ESN baseline | 0.2949 |
| BCRA-Native / leaky tanh | 0.1687 |
| BCRA-Relaxed10 | 0.1496 |

Therefore the higher composite score of BCRA-Relaxed10 was driven by its large improvements in clean delayed recall and pooled temporal decoding.

It did not have the strongest resistance to interfering input.

This is an important limitation and an important property of BCRA v1: different recurrent/topological regimes produce different computational tradeoffs.

---

# Sequence-order experiment

A second task family was introduced during final confirmation to determine whether BCRA's useful temporal state generalized beyond the original single-cue delayed-recall task.

The experiment used:

- 32 ordered-sequence classes;
- different training and testing temporal gaps;
- test timing gaps not used during training;
- first-cue ablation;
- chance accuracy of `0.03125`.

Mean sequence accuracy:

| System | Accuracy |
|---|---:|
| BCRA-Native / leaky tanh | 0.3704 |
| BCRA-Relaxed10 | 0.3457 |
| ESN baseline | 0.1839 |
| BCRA-Native / soft-reset LIF | 0.1465 |
| Zero recurrence | 0.03125 |

BCRA-Relaxed10 significantly exceeded the ESN baseline in the pre-specified paired test.

However, BCRA-Relaxed10 did not significantly outperform BCRA-Native.

The mean candidate-minus-native difference was:

`-0.0247`

with Holm-adjusted:

`p = 0.0800`

The result therefore does not establish superiority of either BCRA topology regime for this sequence-order task.

---

## Sequence-history ablation

Removing the first cue reduced sequence accuracy.

Mean history gain:

- BCRA-Native/leaky: `0.1875`
- BCRA-Relaxed10: `0.1396`
- soft-reset LIF: `0.1214`
- ESN: `0.0902`
- zero recurrence: `0.0000`

This shows that BCRA sequence performance depends partly on information retained from earlier sequence elements.

The comparison of history gain between BCRA configurations was exploratory and should not be interpreted as a pre-specified confirmatory statistical result.

---

# Principal findings

The BCRA v1 experiments support the following conclusions:

1. A real biological connectome can function as a recurrent computational substrate.

2. Recurrent dynamics have a major effect on the usefulness of that substrate.

3. Globally uniform leaky-tanh dynamics produced substantially stronger clean temporal-memory behavior than the earliest tested BCRA dynamics.

4. Exact biological micro-wiring is not universally optimal for the artificial tasks tested.

5. A small amount of topology relaxation substantially improves clean delayed-memory and pooled-time decoding.

6. Native biological topology retains different properties, including stronger interference resistance under the leaky-tanh regime and a stronger sequence-history signal in the final experiment.

7. There is no single demonstrated topology configuration that is best for every temporal computation tested.

---

# What these results do not establish

BCRA v1 does not demonstrate that:

- biological connectomes are universally superior to conventional neural architectures;
- BCRA is a general-purpose replacement for transformers;
- BCRA reproduces the biological function of the Drosophila brain;
- the provisional neurotransmitter-sign model perfectly represents real synaptic physiology;
- BCRA-Native or BCRA-Relaxed10 is universally optimal;
- the artificial tasks used here are equivalent to biological behavior.

BCRA v1 should therefore be interpreted as a validated experimental connectome-based recurrent architecture.

---

# BCRA v1 status

BCRA v1.0.0 is frozen.

Further architectural development belongs to BCRA v2.

Additional experiments on BCRA v1 should be treated as validation, benchmarking, ablation, mechanistic investigation, or application work rather than changes to the v1 architecture.
