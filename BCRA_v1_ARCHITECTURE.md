# BCRA v1.0.0 — Frozen Architecture Specification

**BCRA**: Bio-Connectome Recurrent Architecture

Status: **FROZEN**

## Connectome

- FlyWire FAFB snapshot: v783
- Retained neurons: 138,584
- Directed edges: 3,732,460
- Matrix orientation: `W[post, pre]`
- Edge magnitude: `log1p(synapse_count)`
- Biological weight scale: `0.5`

## Recurrent dynamics

```text
x[t+1] = 0.75*x[t] + 0.25*tanh(0.01*W@x[t] + input[t])
```

The recurrent core is frozen during task-specific training.

## Operating regimes

### BCRA-Native
Untouched retained FlyWire topology.

### BCRA-Relaxed10
Select 10% of directed edge records and permute destinations among those selected records.
The selected destination multiset is preserved pre-coalesce.

Public reference release seed: `20260919`.

The seed exists only for exact reproducibility and was not selected from benchmark performance.

## Versioning

Any architectural change belongs to BCRA v2 or a separately named experimental branch.