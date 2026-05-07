# Week 4 – Initial System Configuration and Security Implementation

[← Week 3](week3.md) | [Back to Home](index.md) | [Next: Week 5 →](week5.md)

---

## Overview

This week focused on implementing foundational security controls on the Ubuntu Server virtual machine. All administration tasks were performed remotely through SSH from the Windows workstation using Git Bash. The objective was to configure secure remote access, implement firewall protection, manage user privileges, and demonstrate secure system administration practices.

---

# SSH Key-Based Authentication

## SSH Connection from Workstation

The server was accessed remotely from the Windows host machine using SSH through Git Bash.

### SSH Connection Command

```bash
ssh studentadmin@192.168.56.106
```

### SSH Connection Evidence

<img width="1611" height="1089" alt="week4-ssh-key-created" src="https://github.com/user-attachments/assets/3901f0c0-2d6e-444c-8079-6fa46874d495" />


---



# SSH Hardening Configuration

The SSH daemon configuration file was modified to improve system security and reduce attack surface exposure.

## SSH Configuration File

```bash
sudo nano /etc/ssh/sshd_config
```

The following security settings were configured:

```text
PubkeyAuthentication yes
PasswordAuthentication no
PermitRootLogin no
PermitEmptyPasswords no
X11Forwarding no
```

These changes:
- disabled password-based authentication
- prevented root login through SSH
- enforced key-based authentication
- disabled unnecessary X11 forwarding
- reduced brute-force attack risk

---

# SSH Configuration Verification

The configuration was verified using:

```bash
sudo sshd -t
```

SSH service was restarted using:

```bash
sudo systemctl restart ssh
```

Configuration verification command:

```bash
sudo grep -E "PasswordAuthentication|PermitRootLogin|PubkeyAuthentication|PermitEmptyPasswords|X11Forwarding" /etc/ssh/sshd_config
```

### Hardened SSH Configuration Evidence

<img width="1430" height="1098" alt="week4-before-ssh-config" src="https://github.com/user-attachments/assets/e3467c75-16cc-4461-8b40-b6c886ab71fd" />

---

# Firewall Configuration Using UFW

The Uncomplicated Firewall (UFW) was configured to restrict remote access to the workstation system only.

## Firewall Rules Applied

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow from 192.168.56.1 to any port 22 proto tcp
sudo ufw enable
```

This configuration:
- blocked all unauthorised incoming traffic
- allowed only SSH traffic from the trusted workstation
- improved network security isolation
- reduced exposure to external attacks

## Firewall Status Verification

```bash
sudo ufw status numbered
```

### Firewall Ruleset Evidence

<img width="1430" height="1098" alt="week4-before-ssh-config" src="https://github.com/user-attachments/assets/8716263a-1715-4699-9ec7-175b87fb830b" />


---



# User Privilege Management

The system was configured using a non-root administrative account called `studentadmin`.

## Privilege Verification Commands

```bash
whoami
groups
sudo -l
```

These commands verified:
- current logged-in user
- group membership
- sudo administrative privileges

### User Privilege Evidence

<img width="1919" height="1098" alt="week4-user-privilege-check" src="https://github.com/user-attachments/assets/506ab8d0-735f-421b-8b9c-f9468fab957d" />


---


# Remote Administration Evidence

All administration tasks were completed remotely through SSH.

## Remote Administration Commands

```bash
hostnamectl
uptime
sudo systemctl status ssh --no-pager
sudo ufw status verbose
```

### Remote Administration Evidence


<img width="1847" height="1127" alt="week4-remote-admin-evidence" src="https://github.com/user-attachments/assets/02253a64-4488-4502-ace8-3142a4ba6697" />

---



# Security Analysis and Reflection

Implementing SSH hardening significantly improved the security posture of the server by eliminating password-based authentication and restricting root access. Using key-based authentication reduced the likelihood of brute-force attacks while improving authentication security.

Restricting firewall access to a single trusted workstation demonstrated the principle of least privilege and minimised unnecessary network exposure. The use of a headless Ubuntu Server environment also improved resource efficiency because no graphical desktop environment consumed additional memory or CPU resources.

One challenge encountered during this phase involved safely modifying SSH configuration settings without accidentally locking remote access. This was mitigated by maintaining an active SSH session while testing new SSH connections in a separate terminal window.

This week demonstrated how Linux operating systems can be securely administered remotely using command-line tools and layered security controls.

---

# Skills Developed

- SSH remote administration
- Linux system hardening
- Firewall configuration with UFW
- User privilege management
- Secure authentication implementation
- Remote server administration
- Command-line system management
- Security configuration validation
