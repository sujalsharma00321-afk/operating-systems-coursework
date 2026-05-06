# Week 6 – Performance Evaluation and Analysis

[← Week 5](week5.md) | [Back to Home](index.md) | [Next: Week 7 →](week7.md)

---

## Objective

The objective of this week was to evaluate Ubuntu Server performance under different workload conditions. Multiple benchmarking and monitoring tools were used to analyse CPU utilisation, memory usage, disk I/O performance, network throughput, latency, and web server responsiveness.

All testing activities were performed remotely through SSH using command-line tools.

---

# 1. Baseline System Monitoring

Initial baseline monitoring was performed before applying workloads to understand normal system behaviour during idle operation.

## Commands Used

```bash
top
free -h
vmstat 1 5
```

## Description

The baseline tests provided information about:

- CPU idle percentage
- memory availability
- swap usage
- active processes
- system load
- virtual memory statistics

These measurements were important for comparing system behaviour before and after workload testing.

## Evidence



<img width="1895" height="1129" alt="week6-baseline-top" src="https://github.com/user-attachments/assets/eb3d9c80-453f-4064-9125-77d3dcd965b3" />

---



![Memory Baseline](images/week6-memory-baseline.png)

<img width="1827" height="1083" alt="week6-memory-baseline" src="https://github.com/user-attachments/assets/b450a898-0e40-4849-9947-f453720c08cf" />

---



![VMStat Baseline](images/week6-vmstat-baseline.png)

<img width="1713" height="1129" alt="week6-vmstat-baseline" src="https://github.com/user-attachments/assets/b114dd9a-ad76-4f1b-aa55-5237049fcdcf" />



---

# 2. CPU Performance Testing

CPU workload testing was performed using `stress-ng`.

## Command Used

```bash
stress-ng --cpu 2 --timeout 30s
```

## Description

The test generated artificial CPU load using two worker threads for 30 seconds. This simulated processor-intensive workloads and allowed analysis of:

- CPU scheduling
- processor saturation
- system responsiveness
- workload handling

## Evidence

![CPU Stress Test](images/week6-cpu-stress.png)

<img width="1905" height="1121" alt="week6-cpu-stress" src="https://github.com/user-attachments/assets/d7d46353-e127-4241-9968-071e290cc13d" />



---


# 3. Memory Performance Testing

Memory stress testing was conducted using the virtual memory component of `stress-ng`.

## Command Used

```bash
stress-ng --vm 1 --vm-bytes 512M --timeout 30s
```

## Description

This workload allocated 512MB of memory to evaluate:

- memory pressure handling
- RAM allocation behaviour
- system stability during memory stress
- swap utilisation

The operating system successfully managed memory allocation without crashing or becoming unresponsive.

---

# 4. Disk I/O Benchmark Testing

Disk benchmarking was performed using the Flexible I/O Tester (`fio`).

## Command Used

```bash
fio --name=test --size=256M --filename=testfile --bs=4k --rw=randrw
```

## Description

The test generated random read and write operations using a 256MB file with 4KB block sizes. This benchmark measured:

- storage throughput
- read/write performance
- disk latency
- I/O responsiveness

Disk performance is important because storage bottlenecks directly affect operating system responsiveness and application performance.

## Evidence

![FIO Benchmark](images/week6-fio-benchmark.png)

<img width="1903" height="1123" alt="week6-fio-benchmark" src="https://github.com/user-attachments/assets/af5ac663-720f-44a4-bf24-d6ae9c54c069" />



---


# 5. Network Throughput Testing

Network performance testing was performed using `iperf3`.

## Commands Used

### Server

```bash
iperf3 -s
```

### Client

```bash
iperf3 -c 192.168.56.106
```

## Description

The test measured TCP bandwidth and throughput between the Windows workstation and Ubuntu Server virtual machine.

The host-only VirtualBox adapter provided a stable isolated testing environment suitable for controlled network analysis.

## Evidence

![iPerf3 Test](images/week6-iperf3-test.png)

<img width="1687" height="1128" alt="week6-iperf3-test" src="https://github.com/user-attachments/assets/7b77fe54-ca5a-4f07-82d2-19c749730b72" />


---


# 6. Latency Analysis

Latency testing was performed using ICMP echo requests.

## Command Used

```bash
ping -c 5 192.168.56.106
```

## Description

The latency test measured:

- round-trip network delay
- packet transmission responsiveness
- network reliability

Low latency values demonstrated efficient communication between the workstation and server within the isolated VirtualBox network.

## Evidence

![Ping Latency](images/week6-ping-latency.png)

<img width="1895" height="1129" alt="week6-ping-latency" src="https://github.com/user-attachments/assets/1ec042cb-15c4-4a27-91a9-ccf7a35495a3" />


---


# 7. Nginx Web Server Response Testing

The nginx web server response was tested using `curl`.

## Command Used

```bash
curl -I http://localhost
```

## Description

The test verified:

- web server availability
- HTTP response functionality
- service responsiveness

The successful HTTP response confirmed that nginx was operating correctly on the Ubuntu Server.

---


# 8. Performance Monitoring Tools Used

| Tool | Purpose |
|---|---|
| top | Real-time CPU and process monitoring |
| free | Memory usage analysis |
| vmstat | Virtual memory statistics |
| stress-ng | CPU and memory workload generation |
| fio | Disk I/O benchmarking |
| iperf3 | Network throughput testing |
| ping | Latency testing |
| curl | Web server response verification |

---

# 9. Performance Analysis

The Ubuntu Server virtual machine demonstrated stable behaviour under all workload conditions.

Key observations:

- CPU workloads increased processor utilisation significantly during `stress-ng` testing
- memory allocation remained stable during RAM stress testing
- disk I/O operations completed successfully without major latency spikes
- VirtualBox host-only networking provided low-latency communication
- nginx remained responsive throughout testing activities

The headless Ubuntu Server configuration improved performance efficiency because no graphical desktop environment consumed unnecessary system resources.

---

# 10. Optimisation Analysis

Several optimisation strategies were identified during testing:

- headless server deployment reduced memory usage
- minimal running services reduced CPU overhead
- SSH-only administration improved resource efficiency
- UFW firewall reduced unnecessary network exposure
- lightweight nginx configuration improved responsiveness

These optimisations improved both security and system performance.

---

# 11. Reflection

This week improved understanding of Linux performance monitoring and workload analysis techniques. The use of command-line benchmarking tools demonstrated how operating systems respond to different computational demands.

Testing also highlighted the relationship between security, performance, and resource efficiency within Linux server environments. The lightweight Ubuntu Server installation provided strong performance whilst maintaining secure remote administration capabilities.

---

# Learning Outcomes Achieved

- Conducted Linux performance benchmarking
- Analysed CPU, memory, storage, and network behaviour
- Used professional Linux monitoring tools
- Evaluated system performance under workload stress
- Investigated network latency and throughput
- Applied performance optimisation strategies
- Improved command-line monitoring skills
