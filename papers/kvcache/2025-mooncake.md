# Paper：Mooncake

## Citation

- Authors：Mooncake team / KTransformers 等
- Venue / Year：FAST 2025
- Title：Mooncake: Trading More Storage for Less Computation — A KVCache-centric Architecture for Serving LLM Chatbot
- Link：https://www.usenix.org/conference/fast25/presentation/qin

## 一句话总结

Mooncake 把 KVCache 作为 serving 系统的一等公民，用更多存储和更强 KV transfer 来减少重复计算。

## 问题

长上下文和多轮对话中，KV cache 很大但也很有复用价值。如果每次请求都 recompute，会浪费大量 GPU compute；如果远端读取，又会引入 network / storage latency。

## 关键想法

KVCache-centric serving：用 CPU DRAM、SSD、NIC / RDMA 等资源构建 KV cache hierarchy，并通过 scheduler 和 transfer engine 在 recomputation 与 remote KV transfer 之间做权衡。

## System / Algorithm

需要重点理解：

- KVCache 存储与检索路径。
- Transfer Engine / RDMA transfer。
- Cache hit rate 与 recomputation boundary。
- tail latency 与 network QoS。

## Experiments

- Hardware：GPU server + CPU memory / SSD / RDMA-capable network。
- Workloads：chatbot / long-context serving。
- Baselines：recompute、local cache、其他 KV cache reuse 方案。
- Metrics：throughput、latency、cache hit rate、transfer bandwidth。

## 复现计划

当前没有完整 RDMA 环境时，先做局部复现：

- 建立 KV transfer vs recomputation 的简单模型。
- 用本地 SSD / CPU memory 模拟分层 cache。
- 记录不同 context length 下 recomputation time。
- 后续有 RDMA 环境再补真实 transfer measurement。

## 与我的研究主线的关系

Mooncake 是 communication 与 KV cache 结合最直接的 baseline。它把问题从 GPU compute 推到了 data movement、storage hierarchy 和 network QoS。

## Open Questions

- 在 H200 / Blackwell 上，recomputation boundary 会如何变化？
- remote KV transfer 的 p99 latency 由哪一段主导？
- 如果 RDMA / RoCE QoS 不稳定，KVCache-centric serving 是否仍然可靠？
