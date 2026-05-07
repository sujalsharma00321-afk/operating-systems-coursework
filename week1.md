# Week 1 – System Planning and Distribution Selection

[Back to Home](index.md) | [Next: Week 2 →](week2.md)

---


# Introduction

This week focused on planning and deploying the operating system infrastructure for the CMPN202 Operating Systems coursework. The objective was to create a professional Linux server environment using a headless Ubuntu Server virtual machine administered remotely via SSH from a Windows workstation using Git Bash.

The deployment was designed to reflect real-world server administration practices used in cloud and enterprise environments. A dual-network VirtualBox configuration using NAT and Host-Only adapters was implemented to provide internet access whilst maintaining an isolated testing environment for security experimentation and remote administration.

The use of a headless Linux server reduces unnecessary graphical resource consumption and aligns with sustainable computing principles by improving resource efficiency.

---

# System Architecture

The environment consists of:

* Windows Host Machine (Workstation)
* Git Bash SSH Client
* Oracle VirtualBox
* Ubuntu Server 24.04 LTS Virtual Machine
* NAT Network Adapter
* Host-Only Network Adapter

The workstation remotely administers the Linux server entirely through SSH command-line access.

---

<img width="1146" height="639" alt="week1-architecture-diagram (1)" src="https://github.com/user-attachments/assets/3bbba370-04f9-44f3-8fc5-42b2d4ddba0f" />

---


# Distribution Selection Justification

Ubuntu Server 24.04 LTS was selected as the server operating system for the following reasons:

* Long-Term Support (LTS) provides stability and extended security updates.
* Strong community support and extensive documentation simplify troubleshooting.
* Native AppArmor support provides mandatory access control capabilities required later in the coursework.
* Excellent package management through APT.
* Widely used in enterprise cloud and DevOps environments.

## Comparison with Debian

Debian is extremely stable and lightweight but generally provides older package versions and slower update cycles. Ubuntu Server offers a more beginner-friendly experience whilst still maintaining enterprise reliability.

## Comparison with CentOS Stream

CentOS Stream provides strong enterprise compatibility but has a steeper learning curve and uses SELinux by default, which may increase configuration complexity for this coursework. Ubuntu Server was selected for its balance between usability, security, and documentation availability.

---

# Workstation Configuration Decision

The Windows host operating system combined with Git Bash was selected as the workstation environment.

Advantages include:

* Lightweight administration workflow
* Reduced resource usage compared to running a second Linux desktop VM
* Native SSH support through Git Bash
* Simplified screenshot capture and documentation management
* Efficient remote server administration

This approach mirrors professional remote administration practices commonly used in cloud infrastructure management.

---

# Network Configuration

Two VirtualBox network adapters were configured:

## NAT Adapter

The NAT adapter provides internet connectivity for the Ubuntu Server virtual machine. This allows package installation, updates, and external connectivity testing.

## Host-Only Adapter

The Host-Only adapter creates an isolated internal network between the Windows workstation and the Ubuntu Server VM. This allows secure SSH administration whilst isolating testing activity from external networks.

The server received the Host-Only IP address:

`192.168.56.106`

This network design improves security by separating internet-facing traffic from the internal administration network.

---

# SSH Remote Administration

SSH remote administration was successfully configured during installation by enabling the OpenSSH Server package.

Remote administration was performed from the Windows workstation using Git Bash.

## SSH Connection Evidence

<img width="1270" height="915" alt="week1-ssh-success" src="https://github.com/user-attachments/assets/5ca15fb8-eff4-400b-bff5-ce3d5a8a9830" />


---


# Command-Line Evidence

## uname -a

The `uname -a` command displays Linux kernel information, system architecture, hostname, and operating system details.


<img width="1466" height="988" alt="week1-uname-output" src="https://github.com/user-attachments/assets/541fe310-72aa-4beb-b7aa-6862c7917b8b" />


---


## free -h

The `free -h` command displays memory usage statistics including total RAM, used memory, available memory, and swap usage using human-readable formatting.


<img width="1377" height="780" alt="week1-free-h" src="https://github.com/user-attachments/assets/537ff7d3-4fea-4c17-8ab0-fe7702b06fbf" />


---


## df -h

The `df -h` command displays filesystem storage usage and mounted partitions in human-readable format.


<img width="1374" height="1090" alt="week1-disk-usage" src="https://github.com/user-attachments/assets/9f13330a-0fa9-43a9-a48f-dbfeb1aca14f" />


---


## ip addr

The `ip addr` command displays network interface configuration and IP addressing information.

The output confirmed:

* NAT adapter configuration
* Host-Only adapter configuration
* Internal SSH management IP address



<img width="1531" height="496" alt="week1-network-config" src="https://github.com/user-attachments/assets/0a293c9d-fe9b-4b35-9c93-ad750e4f04a6" />


---


## lsb_release -a

The `lsb_release -a` command displays Linux distribution information including Ubuntu version, codename, and release details.


<img width="973" height="153" alt="week1-distribution-info" src="https://github.com/user-attachments/assets/ff09a182-119f-4705-ab88-423f603a3838" />


---


# Advanced System Analysis

## hostnamectl

The `hostnamectl` command provided additional operating system metadata including hostname configuration, virtualization details, and kernel information.


<img width="1678" height="1123" alt="week1-hostnamectl" src="https://github.com/user-attachments/assets/2b33304d-2162-435f-8fd6-1257e54c6c22" />


---


## lscpu

The `lscpu` command displayed processor architecture, CPU virtualization support, core allocation, and processor capabilities.


<img width="1898" height="1097" alt="week1-cpu-info" src="https://github.com/user-attachments/assets/2a1f2a3b-4fd5-4148-b364-9a0ac641e775" />


---


## lsblk

The `lsblk` command displayed block storage devices and partition structures configured within the virtual machine.


<img width="1915" height="1100" alt="week1-block-devices" src="https://github.com/user-attachments/assets/d4c0e464-d75c-4219-be67-d463fb152d71" />


---


## ping -c 4 google.com

The ping connectivity test verified external network communication and internet access from the Ubuntu Server virtual machine.


<img width="1697" height="1125" alt="week1-ping-test" src="https://github.com/user-attachments/assets/4077a0d5-9770-4c2d-9266-1fa4b35963ba" />


---



# Reflection

This week provided practical experience in deploying and remotely administering a Linux server environment. Configuring the dual-network architecture improved understanding of network isolation and secure remote administration practices.

One challenge encountered during deployment was understanding the difference between NAT and Host-Only adapters within VirtualBox. Through experimentation and troubleshooting, it became clear that NAT provides external internet access whilst Host-Only networking enables secure isolated communication between the workstation and server.

The use of a headless Ubuntu Server installation demonstrated how server environments can reduce unnecessary graphical overhead and improve resource efficiency. This supports sustainability objectives by lowering memory and processing requirements compared to graphical desktop systems.

Remote administration through SSH highlighted the importance of command-line proficiency in professional Linux system management.

---

