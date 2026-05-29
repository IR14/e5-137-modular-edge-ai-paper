# Finite-Field Edge Inference with GF(137) Kernels

This repository contains a standalone paper package for the experimental
finite-field edge-inference work from the `e5-137-modular-research-sandbox`
project.

The paper reports a small Python/C++ benchmark in which model weights and
activations are represented as byte-valued residues in `Z/137Z`. The main
engineering result is a compact fused native kernel that reduces model memory
from `6.50 KB` to `1.63 KB` and, in the recorded ARM NEON throughput benchmark,
runs `1000` forward passes in `12.1 ms`.

## Contents

- `main.tex` — arXiv/Overleaf-ready LaTeX source.
- `ARTIFACTS.md` — benchmark provenance and copied result tables.
- `artifacts/cpp_kernel_benchmark.md` — GF(137) edge-inference benchmark.
- `artifacts/virtual_quantum_processor_manifest.md` — compact VQP toy benchmark.
- `artifacts/phase9_cross_phase_optimization.md` — final optimization report.

## Scope

This is an engineering benchmark package. It does not claim AGI, cryptographic
security, physical quantum simulation, or quantum advantage. The VQP component
is a deterministic finite-field gate emulator used for representation-level
experiments.

## Build

Upload `main.tex` to Overleaf, or compile locally if a TeX distribution is
installed:

```bash
pdflatex main.tex
pdflatex main.tex
```

The benchmark source code is maintained in:

https://github.com/IR14/e5-137-modular-research-sandbox

## Suggested Release Flow

1. Create a GitHub repository for this paper package.
2. Push the files from this directory.
3. Create a tagged GitHub release, for example `v0.1.0`.
4. Archive the release through Zenodo to obtain a DOI.
5. Use the DOI and GitHub URL in the arXiv metadata or paper notes as needed.
