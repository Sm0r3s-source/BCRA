# BCRA

**Bio-Connectome Recurrent Architecture**

BCRA is a recurrent artificial-intelligence architecture built from a real biological connectome.

The project investigates a simple question:

> Can a real biological connectome function as the recurrent computational substrate of an artificial intelligence system?

BCRA uses the FlyWire Drosophila connectome as a large sparse recurrent graph and studies how biological topology, recurrent dynamics, topology relaxation, and readout design affect temporal computation.

---

## BCRA v1.0.0

**Status: FROZEN**

BCRA v1.0.0 is the first frozen research architecture in the BCRA family.

Frozen specification:

- FlyWire FAFB snapshot: `v783`
- Retained neurons: `138,584`
- Directed edges: `3,732,460`
- Recurrent matrix orientation: `W[post, pre]`
- Edge magnitude: `log1p(synapse_count)`
- Biological weight scale: `0.5`
- Recurrent dynamics: globally uniform leaky tanh
- Leak: `0.25`
- Recurrent gain: `0.01`
- Recurrent core: frozen during task-specific training

The recurrent update is:

```text
x[t+1] = 0.75*x[t] + 0.25*tanh(0.01*W@x[t] + input[t])
