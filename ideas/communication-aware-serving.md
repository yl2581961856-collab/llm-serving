# Communication-Aware LLM Serving

## Thesis

Multi-GPU LLM serving performance is often limited not only by GPU compute, but by the interaction between collective communication, topology, serving schedule, and workload shape.

## Initial Hypothesis

A small empirical communication roofline can help predict when TP/PP/DP/EP will perform poorly on commodity PCIe multi-GPU systems.

## Possible Contributions

- A measurement methodology connecting NCCL microbenchmarks to vLLM traces.
- A topology-aware parallelism selection policy.
- A small tool that estimates whether a serving configuration is latency-bound, bandwidth-bound, or compute-bound.
- A case study on 4x4090 dual-NUMA PCIe topology.

## First Evidence To Collect

- `nvidia-smi topo -m`.
- NCCL all-reduce, all-gather, reduce-scatter, all-to-all curves.
- Pairwise near-GPU vs cross-NUMA performance.
- Nsight trace for one small-message and one large-message collective.
- vLLM TP traces after the NCCL baseline is stable.
