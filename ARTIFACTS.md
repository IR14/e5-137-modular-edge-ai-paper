# Artifact Provenance

The benchmark numbers in `main.tex` were copied from the local release package:

`/Users/i.mikhailov/Desktop/work/cosmo/e5-137-modular-research-sandbox`

The source reports bundled in this paper package are:

- `artifacts/cpp_kernel_benchmark.md`
- `artifacts/virtual_quantum_processor_manifest.md`
- `artifacts/phase9_cross_phase_optimization.md`

## GF(137) Edge-Inference Benchmark

The benchmark task uses 500 prime and 500 composite integers from the range
1000 to 5000. Features are the first 50 fractional base-e digits. Prior audits
found no robust prime/composite separability in these digits, so the benchmark
is interpreted as a systems test rather than a classification result.

| Backend | Memory KB | Time for 1000 forwards | Notes |
|---|---:|---:|---|
| float32 NumPy MLP | 6.50391 | 58.7784 ms | Baseline |
| GF(137) compact uint8 | 1.62793 | 582.904 ms | Python overhead dominates |
| GF(137) C++ fused uint8 | 1.62793 | 40.1530 ms | Python-call latency path |
| GF(137) C++ NEON native loop | 1.62793 | 12.1055 ms | Native throughput path |
| JAX JIT CPU | 6.50391 | 42.4758 ms | Float compute cache |

The native-loop throughput row gives:

- Memory reduction: approximately `4.0x`
- Speedup over the float32 NumPy baseline: approximately `4.86x`

## Compact VQP Toy Benchmark

The VQP path stores `26n` byte-valued phase lanes for `n` virtual qubits. The
comparison baseline stores a full NumPy `complex128` state vector with `2^n`
amplitudes. This is a representation-level comparison, not a physical quantum
simulation benchmark.

| Qubits | Repeats | VQP ms | Float ms | Speedup | Memory Ratio |
|---:|---:|---:|---:|---:|---:|
| 8 | 5000 | 0.072708 | 45.932166 | 631.73x | 19.69x |
| 10 | 3000 | 0.006709 | 49.136333 | 7323.96x | 63.02x |
| 12 | 1000 | 0.012459 | 37.761125 | 3030.83x | 210.05x |
| 16 | 300 | 0.019291 | 94.975167 | 4923.29x | 2520.62x |

The optimized VQP path exploits idempotence in the toy target-oracle projection.
It should be described as compact deterministic finite-field emulation, not as
quantum advantage.

## Reproducibility Notes

The current source repository uses an active compressed test matrix:

```text
5 passed
```

The paper intentionally cites the benchmark reports as artifacts rather than
claiming broader model validity.
