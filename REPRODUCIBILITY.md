# Reproducing BCRA v1

This document describes how to reconstruct and verify the frozen BCRA v1.0.0 architecture.

BCRA v1 uses the FlyWire FAFB v783 connectome.

---

# Frozen specification

BCRA v1.0.0 uses:

- FlyWire FAFB snapshot `v783`
- 138,584 retained neurons
- 3,732,460 directed edge records
- recurrent orientation `W[post, pre]`
- edge magnitude `log1p(synapse_count)`
- biological weight scale `0.5`
- globally uniform leaky-tanh dynamics
- leak `0.25`
- recurrent gain `0.01`
- frozen recurrent core

The recurrent update is:

```text
x[t+1] = 0.75*x[t] + 0.25*tanh(0.01*W@x[t] + input[t])
```

---

# Requirements

The reference implementation is designed for Python/PyTorch and was developed and validated primarily in Google Colab.

The original final validation runs used an NVIDIA L4 GPU.

A CUDA-capable GPU with sufficient memory is recommended for running the full 138,584-neuron recurrent system.

Exact performance and memory requirements on other GPU architectures have not yet been systematically characterized.

---

# Source data

The repository does not redistribute ownership of FlyWire data.

The freeze notebook obtains or processes the required FlyWire/Codex FAFB v783 data used to reconstruct the BCRA graph.

Users are responsible for complying with the original dataset terms and citation requirements.

---

# Reconstructing BCRA v1

Open:

`BCRA_v1_Freeze_Release.ipynb`

or the release notebook corresponding to v1.0.0.

In Google Colab:

1. Open the notebook.
2. Select a GPU runtime.
3. Choose `Runtime -> Run all`.
4. Allow the notebook to obtain and process the required data.
5. Do not change the frozen parameters.

A successful run should end with:

```text
BCRA v1.0.0 ARCHITECTURE FREEZE VERIFIED
```

---

# Freeze checks

The notebook verifies:

- BCRA version is `1.0.0`;
- freeze status is active;
- FlyWire snapshot is `v783`;
- neuron count is exactly `138584`;
- directed edge-record count is exactly `3732460`;
- matrix orientation is `W[post, pre]`;
- biological weight scale is `0.5`;
- leak is `0.25`;
- self-memory coefficient is `0.75`;
- recurrent gain is `0.01`;
- recurrent core is frozen;
- Relaxed10 fraction is exactly `0.10`;
- the selected destination multiset is preserved before sparse coalescing;
- BCRA-Native passes its smoke test;
- BCRA-Relaxed10 passes its smoke test.

---

# BCRA-Native

BCRA-Native uses the retained biological topology directly.

No topology-relaxation transform is applied.

---

# BCRA-Relaxed10

BCRA-Relaxed10 selects 10% of directed edge records and permutes destinations among the selected records.

The transformation preserves:

- source edge records;
- the selected destination multiset before sparse coalescing.

Because duplicate source-destination pairs can be produced, sparse coalescing may slightly reduce the number of unique nonzero matrix entries.

The frozen public reference instance uses:

```text
release_seed = 20260919
```

The release seed is used only to reconstruct the same public reference instance.

It was not selected according to benchmark performance.

---

# Frozen release artifacts

A successful freeze run produces:

```text
bcra_v1_reference_config.json
bcra_v1_relaxed10_reference_patch.npz
BCRA_v1_ARCHITECTURE.md
BCRA_v1_FREEZE_MANIFEST.json
```

---

# Reference patch

`bcra_v1_relaxed10_reference_patch.npz` contains the information needed to reproduce the reference Relaxed10 topology transformation.

It records:

- the selected edge-record indices;
- their replacement destinations;
- the public release seed.

This means users do not have to rely only on reproducing the pseudorandom number-generator sequence.

---

# Freeze manifest

`BCRA_v1_FREEZE_MANIFEST.json` records:

- architecture version;
- architecture parameters;
- graph dimensions;
- Relaxed10 transformation metadata;
- smoke-test results;
- freeze-check results;
- SHA-256 hashes of release artifacts.

For the frozen reference run:

- native sparse nonzeros: `3,732,460`
- Relaxed10 sparse nonzeros: `3,731,409`
- actual changed destination fraction: approximately `0.0999954`

The reduced Relaxed10 sparse-nonzero count results from duplicate edges being merged during sparse coalescing.

---

# Artifact verification

The freeze manifest contains SHA-256 hashes for:

- `bcra_v1_reference_config.json`
- `bcra_v1_relaxed10_reference_patch.npz`
- `BCRA_v1_ARCHITECTURE.md`

Users can calculate the SHA-256 checksum of their local files and compare them with the manifest.

Matching hashes verify that the frozen release artifacts have not been modified.

---

# Experimental reproduction

Architecture reconstruction and experimental reproduction are separate.

The freeze notebook verifies the architecture itself.

Experiment notebooks reproduce individual research studies.

Machine-readable JSON reports in the `results/` directory contain the recorded outputs from the original experiments.

For publication-grade reproduction, use:

1. the frozen BCRA v1 specification;
2. the corresponding experiment notebook;
3. the documented experiment configuration;
4. fresh or recorded random seeds as appropriate;
5. the full FlyWire v783 graph.

---

# Randomness

BCRA experiments use explicit random seeds for:

- task generation;
- topology perturbations;
- readout initialization;
- train/test perturbations;
- control architectures.

Paired experimental designs use corresponding task seeds across compared architectures where specified.

The final BCRA v1 confirmation used 16 fresh paired seeds.

---

# Version integrity

BCRA v1.0.0 is immutable.

Do not modify its frozen graph definition, weight rule, recurrent dynamics, or topology-relaxation definition while continuing to label the result BCRA v1.0.0.

Changes belong to:

- BCRA v2;
- or a separately named experimental branch.

This rule exists so that results reported against BCRA v1 always refer to the same architecture.
