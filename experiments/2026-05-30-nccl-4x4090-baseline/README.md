# Experiment: NCCL 4x4090 Baseline

## Question

How do NCCL collective baselines differ between near-GPU pairs, cross-NUMA pairs, and all 4 GPUs on a PCIe-only 4x4090 dual-NUMA machine?

## Known Topology

```text
        GPU0    GPU1    GPU2    GPU3    CPU Affinity    NUMA Affinity
GPU0     X      NODE    SYS     SYS     0-27,56-83      0
GPU1    NODE     X      SYS     SYS     0-27,56-83      0
GPU2    SYS     SYS      X      NODE    28-55,84-111    1
GPU3    SYS     SYS     NODE     X      28-55,84-111    1
```

Interpretation:

- GPU0/GPU1 are near each other within NUMA node 0.
- GPU2/GPU3 are near each other within NUMA node 1.
- Cross pairs traverse `SYS` and should be slower or less stable.
- There is no NVLink in this topology.

## Collectives

Run at least:

- all_reduce
- all_gather
- reduce_scatter
- alltoall

## Device Cases

```text
0,1       near pair on NUMA 0
2,3       near pair on NUMA 1
0,2       cross-NUMA pair
1,3       cross-NUMA pair
0,1,2,3   full 4-GPU run
```

## Commands

```bash
# Fill exact commands here.
```

## Results

| Collective | Devices | Size Range | Peak AlgBW | Peak BusBW | Notes |
|---|---|---:|---:|---:|---|

## Observations

1. 
2. 
3. 

## Next

- Add `NCCL_DEBUG=INFO NCCL_DEBUG_SUBSYS=INIT,GRAPH` for selected runs.
- Add Nsight Systems trace for one small-message and one large-message case.
- Compare with `NCCL_P2P_DISABLE=1`.
