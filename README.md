# LLM Serving 研究笔记

这个仓库用于记录 multi-GPU LLM serving 方向的研究过程，重点关注 communication bottleneck 的诊断与优化。

## 研究主线

**面向 multi-GPU LLM inference 的 communication bottleneck 诊断与优化。**

允许展开的支线：

- tinygrad：理解 tensor IR、primitive composition 和 collective 语义。
- CUDA C++：理解 kernel、memory hierarchy、stream 和 profiling。
- DeepGEMM / CuTe / CUTLASS：理解计算侧粒度，以及 GEMM / MoE kernel。
- NCCL / NVSHMEM / RDMA：理解 collective communication、topology 和 transport。
- vLLM / Megatron / DeepSpeed：回到真实 serving workload 和 parallelism strategy。

每条支线最终都要回答一个问题：

> 这件事如何帮助解释或改善 multi-GPU LLM serving 中的 communication？

## 仓库结构

```text
papers/        论文笔记，按研究方向归类。
experiments/   可复现实验 slice，包括 raw log、结果表和图。
ideas/         研究问题、潜在 paper 方向和设计草图。
templates/     paper note 和 experiment record 的 Markdown 模板。
```

## 当前第一阶段

- 通过小规模复现理解 tinygrad-notes 和 tinygrad tensor puzzles。
- 在 4x RTX 4090 PCIe dual-NUMA topology 上跑通 NCCL baseline。
- 保存 commands、raw logs、topology 和第一批观察。

## 工作规则

一个实验只回答一个问题。raw data、commands、environment 和 observations 要放在一起，避免之后无法复现或解释。
