# Performance Analysis

## 1. Objective

The objective of this experiment is to compare the CPU performance of a Type-1 hypervisor (Proxmox VE) and a Type-2 hypervisor (VMware Workstation) using the same Sysbench CPU benchmark.

The benchmark used was:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

## 2. Benchmark Results

| Parameter | Type-1 Proxmox VE | Type-2 VMware Workstation |
|---|---:|---:|
| Total Execution Time | 10.0030 s | 10.0002 s |
| Total Events | 14,548 | 10,381 |
| Events per Second | 1,453.98 | 1037.93 |
| Average Latency | 0.69 ms | 0.96 ms |

## 3. Analysis

### Total Execution Time

Proxmox VE recorded a total execution time of 10.0030 seconds, while VMware Workstation recorded 10.0002 seconds. The measured times are very close, showing only a small difference for this benchmark run.

### Total Events

Proxmox VE completed 14,548 events, whereas VMware Workstation completed 10,381 events during the benchmark.

### Events Per Second

Proxmox VE achieved 1,453.98 events per second. VMware Workstation achieved 1037.93 events per second. Events per second represents the number of benchmark operations completed each second.

### Average Latency

The average latency measured for Proxmox VE was 0.69 ms, while VMware Workstation recorded 0.96 ms. Lower latency indicates less time per individual benchmark event.

## 4. Observation

The benchmark results are relatively close for both hypervisors. Proxmox VE recorded more events per second and a lower average latency in this particular run, while the total execution times were almost identical.

These results are specific to the experimental VM configurations and the particular benchmark runs performed. They should not be treated as a general performance result for all Proxmox VE or VMware Workstation installations.

## 5. Conclusion

The experiment successfully measured CPU performance for both Type-1 Proxmox VE and Type-2 VMware Workstation using Sysbench with a prime-number limit of 20000.

The collected measurements provide a basis for comparing execution time, event throughput, and latency between the two experimental environments.
