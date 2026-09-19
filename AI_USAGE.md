# AI Usage Disclosure

Generative AI systems were used extensively during the development of BCRA.

This disclosure is provided to make the research and development process transparent.

## Scope of AI assistance

AI systems assisted with several parts of the BCRA research workflow, including:

- experimental design;
- development of experimental protocols;
- Python and PyTorch implementation;
- Google Colab notebook generation;
- debugging;
- statistical-analysis implementation;
- interpretation of experimental results;
- identification of experimental limitations and confounds;
- documentation;
- preparation and editing of repository material;
- planning of follow-up experiments.

AI assistance was therefore not limited to grammar correction or code autocomplete.

## Human responsibility

The project author executed the experiments and retained the generated experimental reports and release artifacts.

Experimental outputs were reviewed before architectural decisions were made.

The human author takes responsibility for:

- the decision to publish BCRA;
- the frozen BCRA v1.0.0 specification;
- the experiments included in this repository;
- the claims presented in the repository documentation;
- the decision to accept or reject AI-generated suggestions;
- future corrections if errors are discovered.

AI systems are not listed as authors.

## Verification

BCRA development used repeated controls, paired experimental designs, fresh-seed confirmation experiments, machine-readable JSON reports, and a final architecture-freeze procedure.

The final BCRA v1.0.0 freeze notebook verifies architecture invariants and produces a manifest containing hashes for the frozen release artifacts.

This does not mean that every AI-generated suggestion was correct. AI-generated code and interpretations were treated as material requiring testing and review.

## Research philosophy

AI assistance is considered a development tool in this project rather than a source of experimental evidence.

Claims about BCRA are based on executed experiments and their recorded outputs, not on statements produced by an AI system.

## Disclosure in future publications

Any academic manuscript based on BCRA will disclose generative-AI use in accordance with the policies of the relevant journal, conference, or preprint service.
