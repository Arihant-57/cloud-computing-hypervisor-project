# Performance Analysis of Type-1 and Type-2 Hypervisors

[![Course](https://img.shields.io/badge/Course-Cloud%20Computing-blue.svg)](#)
[![Hypervisors](https://img.shields.io/badge/Hypervisors-Proxmox%20VE%20%7C%20VMware%20Workstation-orange.svg)](#)
[![Benchmark](https://img.shields.io/badge/Benchmark-Sysbench%20CPU%2020k%20Primes-green.svg)](#)
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen.svg)](#)

---

## Executive Summary

This repository contains the experimental setup, screenshots, benchmark results, performance comparison, and analysis for comparing a **Type-1 hypervisor (Proxmox VE)** with a **Type-2 hypervisor (VMware Workstation)**.

Ubuntu virtual machines were used in both environments with the same main resource allocation of **2 vCPU, 2 GB RAM, and 20 GB virtual disk**. The CPU benchmark used was:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The recorded results from the experiment are:

| Performance Metric | Proxmox VE (Type-1) | VMware Workstation (Type-2) |
|---|---:|---:|
| Total Execution Time | 10.0030 s | 10.0002 s |
| Total Events | 14,548 | 10,381 |
| Events per Second | 1,453.98 | 1,037.93 |
| Average Latency | 0.69 ms | 0.96 ms |

These values are from the actual benchmark runs performed for this project. They should be interpreted as results for these experimental VM configurations and benchmark runs, not as universal performance values for every installation.

---

## Table of Contents

1. [Project Objectives](#1-project-objectives)
2. [Hypervisor Architectural Comparison](#2-hypervisor-architectural-comparison)
3. [Virtual Machine Specifications](#3-virtual-machine-specifications)
4. [Experimental Procedure](#4-experimental-procedure)
5. [Empirical Results and Screenshots](#5-empirical-results-and-screenshots)
6. [Performance Comparison](#6-performance-comparison)
7. [Metric Explanations](#7-metric-explanations)
8. [Analysis and Observation](#8-analysis-and-observation)
9. [Conclusion](#9-conclusion)
10. [Repository Structure and Reproduction](#10-repository-structure-and-reproduction)

---

## 1. Project Objectives

The objectives of this Cloud Computing experiment are:

1. Deploy an Ubuntu virtual machine using a **Type-1 hypervisor (Proxmox VE)**.
2. Deploy an Ubuntu virtual machine using a **Type-2 hypervisor (VMware Workstation)**.
3. Configure comparable virtual hardware resources in both environments.
4. Verify CPU, memory, and disk configuration inside the Ubuntu virtual machines.
5. Run the same Sysbench CPU benchmark in both environments.
6. Record:
   - Total execution time
   - Total events
   - Events per second
   - Average latency
7. Compare the measured results and document the observations.

---

## 2. Hypervisor Architectural Comparison

### Type-1 Hypervisor — Proxmox VE

Proxmox VE is a virtualization platform that runs directly on the physical server hardware. It uses Linux and KVM for hardware-assisted virtualization.

Basic architecture:

```text
+---------------------------------------+
|       Ubuntu Virtual Machine          |
|       Sysbench CPU Benchmark          |
+---------------------------------------+
|          Proxmox VE / KVM             |
+---------------------------------------+
|          Physical Hardware            |
|       CPU | RAM | Storage | NIC       |
+---------------------------------------+
```

The experiment used Proxmox VE to create and run the Type-1 Ubuntu virtual machine.

### Type-2 Hypervisor — VMware Workstation

VMware Workstation is a hosted virtualization application that runs on a host operating system. The Ubuntu virtual machine runs through VMware Workstation while the host operating system manages the underlying physical hardware.

Basic architecture:

```text
+---------------------------------------+
|       Ubuntu Virtual Machine          |
|       Sysbench CPU Benchmark          |
+---------------------------------------+
|         VMware Workstation            |
+---------------------------------------+
|          Host Operating System        |
+---------------------------------------+
|          Physical Hardware            |
|       CPU | RAM | Storage | NIC       |
+---------------------------------------+
```

The experiment used VMware Workstation to create and run the Type-2 Ubuntu virtual machine.

---

## 3. Virtual Machine Specifications

The main VM resources used for the experiment were kept comparable:

| Resource | Proxmox VE (Type-1) | VMware Workstation (Type-2) |
|---|---|---|
| Guest OS | Ubuntu | Ubuntu |
| CPU | 2 vCPU | 2 vCPU |
| RAM | 2 GB | 2 GB |
| Virtual Disk | 20 GB | 20 GB |
| Benchmark | Sysbench CPU | Sysbench CPU |
| Prime Limit | 20,000 | 20,000 |

System configuration was verified using commands such as:

```bash
lscpu
free -h
df -h
```

---

## 4. Experimental Procedure

### Step 1: Create the Type-1 VM

1. Open the Proxmox VE web interface.
2. Create an Ubuntu virtual machine.
3. Configure the VM with the required CPU, memory, and disk resources.
4. Install Ubuntu.
5. Start the VM and open the Ubuntu console.

Screenshots of the Proxmox setup are available in:

```text
screenshots/type1-proxmox/
```

### Step 2: Create the Type-2 VM

1. Open VMware Workstation on the host system.
2. Create a new Ubuntu virtual machine.
3. Configure the VM with comparable CPU, memory, and disk resources.
4. Install Ubuntu.
5. Start the VM.

Screenshots of the VMware setup are available in:

```text
screenshots/type2-vmware/
```

### Step 3: Verify System Configuration

The following commands were used inside the Ubuntu VMs:

```bash
lscpu
free -h
df -h
```

These commands were used to verify CPU, memory, and disk information before running the benchmark.

### Step 4: Run Sysbench

The same benchmark was executed in both environments:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The benchmark was allowed to run for approximately 10 seconds and the output was recorded.

---

## 5. Empirical Results and Screenshots

### Type-1 — Proxmox VE

The Proxmox VE Sysbench result recorded:

```text
events per second: 1453.98
total time: 10.0030s
total number of events: 14548
Latency avg: 0.69 ms
```

The complete Type-1 screenshots are available in:

[`screenshots/type1-proxmox/`](screenshots/type1-proxmox/)

The main benchmark screenshot is:

[`06-proxmox-sysbench-result.png`](screenshots/type1-proxmox/06-proxmox-sysbench-result.png)

### Type-2 — VMware Workstation

The VMware Workstation Sysbench result recorded:

```text
events per second: 1037.93
total time: 10.0002s
total number of events: 10381
Latency avg: 0.96 ms
```

The complete Type-2 screenshots are available in:

[`screenshots/type2-vmware/`](screenshots/type2-vmware/)

The main benchmark screenshot is:

[`06-vmware-sysbench-cpu.png`](screenshots/type2-vmware/06-vmware-sysbench-cpu.png)

---

## 6. Performance Comparison

The following table contains the measured values from the two benchmark runs:

| Performance Metric | Proxmox VE (Type-1) | VMware Workstation (Type-2) |
|---|---:|---:|
| **Total Execution Time** | **10.0030 s** | **10.0002 s** |
| **Total Events** | **14,548** | **10,381** |
| **Events per Second** | **1,453.98** | **1,037.93** |
| **Average Latency** | **0.69 ms** | **0.96 ms** |

A visual comparison of these measurements is available here:

[`01-hypervisor-performance-comparison.png`](screenshots/comparison/01-hypervisor-performance-comparison.png)

The detailed written analysis is available in:

[`results/performance-analysis.md`](results/performance-analysis.md)

---

## 7. Metric Explanations

### Total Execution Time

The total time taken by the Sysbench benchmark run.

### Total Events

The total number of benchmark events completed during the test.

### Events Per Second

The number of benchmark events completed per second. It represents the throughput measured by Sysbench.

### Average Latency

The average time required to complete an individual benchmark event.

For this experiment, the recorded average latencies were:

- Proxmox VE: **0.69 ms**
- VMware Workstation: **0.96 ms**

---

## 8. Analysis and Observation

The two benchmark runs produced similar total execution times because Sysbench runs the CPU test for approximately the same duration in both environments.

The measured number of events and events per second were different:

- Proxmox VE: **14,548 total events** and **1,453.98 events/sec**
- VMware Workstation: **10,381 total events** and **1,037.93 events/sec**

The measured average latency was:

- Proxmox VE: **0.69 ms**
- VMware Workstation: **0.96 ms**

Therefore, in this particular experiment, the Proxmox VE VM completed more benchmark events per second and recorded a lower average latency.

These observations are specific to the configurations, host conditions, and benchmark runs used in this experiment. They should not be treated as a general performance ranking of all Proxmox VE and VMware Workstation installations.

---

## 9. Conclusion

This experiment successfully compared CPU performance in Ubuntu virtual machines running on:

- **Type-1:** Proxmox VE
- **Type-2:** VMware Workstation

The same Sysbench CPU benchmark was executed in both environments using a prime-number limit of **20,000**.

The experiment recorded:

- Proxmox VE: **1,453.98 events/sec**, **14,548 events**, and **0.69 ms average latency**
- VMware Workstation: **1,037.93 events/sec**, **10,381 events**, and **0.96 ms average latency**

The results provide an experimental basis for understanding the performance differences observed between the two virtualization environments.

---

## 10. Repository Structure and Reproduction

### Folder Layout

```text
cloud-computing-hypervisor-project/
│
├── README.md
│
├── screenshots/
│   ├── comparison/
│   │   └── 01-hypervisor-performance-comparison.png
│   │
│   ├── type1-proxmox/
│   │   ├── 01-proxmox-dashboard.png
│   │   ├── 02-proxmox-vm-configuration.png
│   │   ├── 03-proxmox-vm-running.png
│   │   ├── 04-proxmox-ubuntu-console.png
│   │   ├── 05-01-proxmox-system-configuration.png
│   │   ├── 05-02-proxmox-system-configuration.png
│   │   ├── 06-proxmox-sysbench-result.png
│   │   └── 07-01proxmox-resource-monitoring.png
│   │
│   └── type2-vmware/
│       ├── 01-vmware-vm-configuration.png
│       ├── 02-vmware-vm-running.png
│       ├── 03-vmware-lscpu--01--.png
│       ├── 03-vmware-lscpu--02--.png
│       ├── 04-vmware-memory.png
│       ├── 05-vmware-disk.png
│       └── 06-vmware-sysbench-cpu.png
│
├── results/
│   └── performance-analysis.md
│
└── scripts/
    ├── benchmark.sh
    ├── generate_plots.py
    └── parse_sysbench.py
```

### Benchmark Command

Install Sysbench on Ubuntu:

```bash
sudo apt update
sudo apt install sysbench -y
```

Verify the installation:

```bash
sysbench --version
```

Run the CPU benchmark:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The benchmark output can then be recorded and compared between the Type-1 and Type-2 environments.

### Included Scripts

The `scripts/` directory contains supporting files for the experiment:

- `benchmark.sh` — benchmark automation script
- `generate_plots.py` — performance visualization script
- `parse_sysbench.py` — Sysbench analysis script

---

## Project Files

- **Screenshots:** `screenshots/`
- **Performance analysis:** `results/performance-analysis.md`
- **Supporting scripts:** `scripts/`
- **Performance comparison image:** `screenshots/comparison/`

---

*Laboratory experiment conducted for the Cloud Computing course.*
