# Week 3 — Application Selection for Performance Testing

[Back to Home](index.md)

---

# Introduction

This week focused on selecting appropriate applications and services for performance evaluation and operating system behaviour analysis. The goal was to deploy different workload categories capable of generating measurable CPU, memory, storage, and network activity within the Ubuntu Server environment.

Applications were selected based on:

* lightweight server compatibility
* ease of command-line deployment
* measurable resource utilisation
* suitability for benchmarking
* professional industry relevance

All applications were installed remotely through SSH administration from the Windows workstation.

---

# Application Selection Matrix

| Workload Type      | Application    | Purpose                    | Justification                                                                      |
| ------------------ | -------------- | -------------------------- | ---------------------------------------------------------------------------------- |
| CPU-intensive      | stress-ng      | CPU stress testing         | Lightweight benchmarking tool capable of generating controlled processor workloads |
| Memory-intensive   | stress-ng --vm | RAM stress testing         | Allows controlled memory allocation for resource analysis                          |
| Disk I/O-intensive | fio            | Storage benchmarking       | Industry-standard disk testing utility widely used in server environments          |
| Network-intensive  | iperf3         | Network throughput testing | Professional network bandwidth and latency testing tool                            |
| Server application | nginx          | Web server deployment      | Lightweight and widely used web server suitable for response-time analysis         |

---

# Package Installation

The required testing applications and monitoring tools were installed using the Ubuntu package manager through the command-line interface.

Installed packages:

* stress-ng
* fio
* iperf3
* nginx
* sysstat

(Insert package installation screenshot below this section)

The installation process demonstrated Linux package management functionality and server-side software deployment through remote administration workflows.

---

# CPU Workload Testing

The `stress-ng` utility was selected for CPU benchmarking and workload simulation.

Command used:

```bash
stress-ng --cpu 2 --timeout 30s
```

(Insert CPU stress test screenshot below this section)

This workload generated artificial processor utilisation using two CPU workers for 30 seconds. CPU stress testing is important because it helps identify:

* scheduling behaviour
* processor saturation
* system responsiveness under load
* thermal and performance limitations

---

# Memory Workload Testing

Memory stress testing was performed using the virtual memory functionality of `stress-ng`.

Command used:

```bash
stress-ng --vm 1 --vm-bytes 512M --timeout 30s
```

This workload allocated 512MB of memory to simulate memory-intensive application behaviour. Monitoring memory pressure is important because insufficient RAM availability can lead to:

* swapping
* increased latency
* application instability
* reduced system responsiveness

---

# Disk I/O Performance Testing

Disk benchmarking was performed using the `fio` testing utility.

Command used:

```bash
fio --name=test --size=256M --filename=testfile --bs=4k --rw=randrw
```

(Insert fio screenshot below this section)

The test generated random read/write operations using a 256MB file and 4KB block sizes. Disk I/O analysis is important because storage bottlenecks significantly affect:

* application responsiveness
* database workloads
* file operations
* server scalability

The use of `fio` reflects industry-standard benchmarking practices within Linux server environments.

---

# Network Performance Testing

Network throughput testing was performed using `iperf3`.

Server command:

```bash
iperf3 -s
```

Client command:

```bash
iperf3 -c 192.168.56.106
```

(Insert iperf3 screenshot below this section)

The test measured TCP bandwidth and network throughput between the workstation and Ubuntu Server virtual machine. Network analysis is important because:

* latency affects service responsiveness
* throughput limitations reduce scalability
* network congestion impacts application performance

The host-only VirtualBox network configuration provided an isolated environment for controlled testing activities.

---

# Nginx Web Server Deployment

The nginx web server was deployed to provide a lightweight server application suitable for response-time analysis and service monitoring.

(Insert nginx screenshot below this section)

Nginx was selected because:

* it is lightweight
* highly efficient
* widely used in production Linux environments
* suitable for load and response testing

Deploying nginx also supports future security analysis activities such as service auditing and firewall configuration.

---

# Expected Resource Profiles

| Application        | Expected Resource Usage               |
| ------------------ | ------------------------------------- |
| stress-ng CPU test | High CPU usage, low disk activity     |
| stress-ng VM test  | High memory allocation                |
| fio                | High disk read/write operations       |
| iperf3             | High network throughput               |
| nginx              | Low CPU usage, moderate network usage |

Understanding expected resource behaviour is important because it supports accurate performance analysis and bottleneck identification during future testing phases.

---

# Monitoring Strategy

The following monitoring tools were selected for future performance analysis:

| Tool   | Purpose                              |
| ------ | ------------------------------------ |
| top    | Real-time CPU and process monitoring |
| vmstat | System performance statistics        |
| free   | Memory usage analysis                |
| df     | Disk usage monitoring                |
| ss     | Network socket analysis              |
| ping   | Latency testing                      |

The command-line monitoring approach supports lightweight administration without graphical overhead, improving system efficiency and resource utilisation.

---

# Reflection

This week improved understanding of workload generation and operating system performance analysis techniques. Different workload categories demonstrated how operating systems manage:

* processor scheduling
* memory allocation
* storage operations
* network communication

The use of lightweight command-line benchmarking tools reinforced the importance of efficient resource monitoring within headless Linux server environments.

The practical deployment process also demonstrated how server administrators prepare systems for performance testing and infrastructure optimisation activities.

---

# References

[1] stress-ng Documentation. Available: https://manpages.ubuntu.com/manpages/jammy/man1/stress-ng.1.html [Accessed: 6 May 2026].

[2] fio Documentation. Available: https://fio.readthedocs.io [Accessed: 6 May 2026].

[3] iPerf3 Documentation. Available: https://iperf.fr [Accessed: 6 May 2026].

[4] Nginx Documentation. Available: https://nginx.org/en/docs/ [Accessed: 6 May 2026].
