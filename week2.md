# Week 2 – Security Planning and Testing Methodology

[← Week 1](week1.md) | [Back to Home](index.md) | [Next: Week 3 →](week3.md)

---

# Introduction

This week focused on designing the security baseline and performance testing methodology for the Ubuntu Server infrastructure. The objective was to analyse the default system security posture, identify potential vulnerabilities, and plan future hardening activities that will be implemented throughout later coursework phases.

The system was assessed using command-line security analysis tools through remote SSH administration from the Windows workstation.

---

# Security Baseline Planning

The initial Ubuntu Server deployment was analysed to identify existing security mechanisms and areas requiring further hardening.

The following security controls were selected for implementation during future coursework phases:

* SSH key-based authentication
* Firewall hardening using UFW
* Mandatory access control using AppArmor
* Automatic security updates
* User privilege management
* Intrusion prevention using fail2ban
* Service exposure reduction
* Security auditing and monitoring

These controls were selected to improve system confidentiality, integrity, and availability.

---

# SSH Service Analysis

The SSH service was inspected to verify that remote administration services were operational.

The analysis confirmed:

* OpenSSH service running successfully
* SSH daemon listening on port 22
* Active remote administration capability
* Successful workstation-to-server connectivity

(Insert SSH service status screenshot below this section)

The use of SSH enables secure encrypted remote administration whilst reducing the need for direct console interaction with the server.

---

# SSH Configuration Analysis

The `/etc/ssh/sshd_config` file was analysed to review current SSH security settings.

Key observations included:

* Password authentication enabled by default
* Empty password logins disabled
* PAM authentication enabled
* Default SSH port configuration active

(Insert SSH configuration screenshot below this section)

The default SSH configuration provides basic functionality but requires further hardening. Future improvements will include:

* SSH key-based authentication
* Disabling password authentication
* Restricting root access
* Firewall access restrictions

---

# Firewall Baseline Analysis

The Ubuntu UFW firewall status was inspected.

(Insert firewall status screenshot below this section)

The firewall was initially inactive, meaning incoming network traffic was not currently restricted. Whilst acceptable during initial deployment, this represents a potential security risk that will be mitigated in Week 4 through firewall rule implementation and SSH access restrictions.

---

# Mandatory Access Control Analysis

AppArmor status was analysed using the `aa-status` command.

(Insert AppArmor screenshot below this section)

The analysis confirmed that several system services were already protected using AppArmor security profiles operating in enforce mode. This demonstrates Ubuntu Server’s use of mandatory access control mechanisms to reduce the impact of service compromise.

AppArmor was selected instead of SELinux due to:

* Ubuntu native integration
* Simpler profile management
* Better compatibility with Ubuntu Server environments
* Reduced configuration complexity

---

# Open Service and Port Analysis

The `ss -tuln` command was used to inspect active listening services and network ports.

(Insert open services screenshot below this section)

The analysis identified currently exposed services and network sockets. Monitoring active listening ports is important because unnecessary services increase the attack surface of the operating system.

Future hardening activities will aim to minimise exposed services and restrict network access.

---

# Monitoring Tool Verification

Monitoring and performance analysis tools were verified using command-line inspection.

(Insert monitoring tools screenshot below this section)

The following tools were confirmed available:

* `top`
* `vmstat`
* `ss`
* `ping`

These tools will later support:

* CPU performance monitoring
* memory analysis
* network analysis
* system load monitoring
* latency testing
* troubleshooting activities

---

# Performance Testing Methodology

A structured testing methodology was designed for future workload evaluation.

The testing process will include:

## Baseline Performance Testing

Baseline measurements will be collected before workload execution to establish standard system behaviour under idle conditions.

Metrics collected:

* CPU usage
* memory utilisation
* disk usage
* network activity
* system load
* response latency

---

## Application Load Testing

Different workload types will later be deployed to analyse operating system behaviour under varying computational stress.

Planned workload categories:

* CPU-intensive applications
* memory-intensive applications
* disk I/O-intensive applications
* network-intensive applications
* server-based services

---

## Performance Monitoring Approach

Performance data will be collected remotely through SSH using command-line monitoring tools.

Tools selected:

* `top`
* `vmstat`
* `ss`
* `ping`
* `df`
* `free`

This approach supports lightweight monitoring without unnecessary graphical overhead.

---

# Threat Model

Several security threats were identified during baseline analysis.

| Threat                      | Risk                       | Mitigation Strategy                                          |
| --------------------------- | -------------------------- | ------------------------------------------------------------ |
| Brute-force SSH attacks     | Unauthorised remote access | SSH key authentication, fail2ban, firewall restrictions      |
| Exposed network services    | Increased attack surface   | Restrict open ports and disable unnecessary services         |
| Weak authentication methods | Credential compromise      | Enforce strong passwords and disable password authentication |
| Unpatched vulnerabilities   | System exploitation        | Configure automatic security updates                         |
| Privilege escalation        | Administrative compromise  | Implement least privilege access controls                    |

---

# Reflection

This week improved understanding of Linux security baselines and the importance of proactive security planning before system deployment into production environments.

Analysing default Ubuntu Server configurations demonstrated that many operating systems prioritise usability and compatibility during installation rather than maximum security. This highlighted the importance of security hardening within professional system administration workflows.

The use of command-line monitoring and analysis tools reinforced the importance of lightweight administration techniques within headless Linux server environments.

---
