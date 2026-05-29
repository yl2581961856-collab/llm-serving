# Baseline Paper Reading List

这份列表用于启动 multi-GPU LLM serving / communication 方向的 baseline 阅读与复现。优先级不是论文价值排序，而是按当前研究主线的进入顺序排序。

## P0：先读先复现

1. vLLM / PagedAttention
   - 路径：`papers/serving/2023-vllm-pagedattention.md`
   - 作用：建立 LLM serving 和 KV cache 管理的第一条 baseline。

2. Orca
   - 路径：`papers/serving/2022-orca.md`
   - 作用：理解 iteration-level scheduling 和 continuous batching 的系统动机。

3. Sarathi-Serve
   - 路径：`papers/serving/2024-sarathi-serve.md`
   - 作用：理解 chunked prefill 和 throughput / latency tradeoff。

4. DistServe
   - 路径：`papers/serving/2024-distserve.md`
   - 作用：理解 prefill / decode disaggregation 和 SLO-aware serving。

## P1：通信与 KV cache 主线

5. Splitwise
   - 路径：`papers/serving/2024-splitwise.md`
   - 作用：理解 phase splitting 和异构资源分工。

6. Mooncake
   - 路径：`papers/kvcache/2025-mooncake.md`
   - 作用：理解 KVCache-centric serving、RDMA transfer 和存储换计算。

7. LMCache
   - 路径：`papers/kvcache/2025-lmcache.md`
   - 作用：理解 KV cache layer、offload 和跨 serving engine 的复用。

## P2：底层 collective 与通信算法

8. SCCL
   - 路径：`papers/communication/2021-sccl.md`
   - 作用：理解 topology-aware collective algorithm synthesis。

9. TACCL
   - 路径：`papers/communication/2023-taccl.md`
   - 作用：理解 communication sketch 如何指导 collective synthesis。

10. MSCCL++
    - 路径：`papers/communication/2025-mscclpp.md`
    - 作用：理解面向 AI workload 的可编程 GPU communication abstraction。

## MoE 支线

11. Tutel
    - 路径：`papers/moe/2023-tutel.md`
    - 作用：理解 MoE scale-out、routing 和 all-to-all 的系统问题。

12. MegaBlocks
    - 路径：`papers/moe/2023-megablocks.md`
    - 作用：理解 MoE 中 token imbalance、block-sparse compute 和 grouped GEMM。

## 阅读规则

每篇 paper 只先回答四件事：

1. 它解决什么 bottleneck？
2. 它的核心 mechanism 是什么？
3. 我现在能复现哪一部分？
4. 它如何回到 communication bottleneck diagnosis and optimization for multi-GPU LLM inference？
