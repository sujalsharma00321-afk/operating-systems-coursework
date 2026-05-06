# Week 5 – Advanced Security and Monitoring Infrastructure

[← Week 4](week4.md) | [Back to Home](index.md) | [Next: Week 6 →](week6.md)

---

## Objective
The objective of this week was to improve Linux server security using firewall rules, intrusion prevention systems, AppArmor, and SSH hardening techniques on the Ubuntu Server virtual machine.

---

# 1. UFW Firewall Configuration

## Commands Used

```bash
sudo ufw allow from 192.168.56.1 to any port 22
sudo ufw enable
sudo ufw status verbose
```

## Description
UFW (Uncomplicated Firewall) was configured to allow SSH access only from the host machine IP address. This reduces unauthorized access attempts and improves overall server security.

## Evidence

<img width="1816" height="582" alt="week5-ufw" src="https://github.com/user-attachments/assets/290f2810-dd25-4368-83a0-7ec694b36b8b" />


---


# 2. SSH Security Hardening

## Commands Used

```bash
sudo nano /etc/ssh/sshd_config
sudo systemctl restart ssh
sudo grep -E "PasswordAuthentication|PermitRootLogin|PubkeyAuthentication|PermitEmptyPasswords|X11Forwarding" /etc/ssh/sshd_config
```

## Security Changes Applied

- Disabled root login
- Disabled empty passwords
- Disabled X11 forwarding
- Enabled public key authentication
- Disabled password authentication

## Description
The SSH configuration file was modified to strengthen remote access security and reduce the possibility of brute-force attacks and unauthorized logins.

## Evidence

<img width="1809" height="1055" alt="week5-ssh-hardening" src="https://github.com/user-attachments/assets/5537a75a-328d-43a6-a146-464742296bf1" />


---


# 3. AppArmor Status Verification

## Command Used

```bash
sudo aa-status
```

## Description
AppArmor security profiles were verified to ensure mandatory access control protection is active on the Ubuntu server.

## Evidence


<img width="1442" height="1130" alt="week5-apparmor-status" src="https://github.com/user-attachments/assets/880a0555-94f4-4de6-ac86-7ab0a79963a7" />


---


# 4. Fail2Ban Installation and Configuration

## Packages Installed

```bash
sudo apt install fail2ban apparmor-utils -y
```

## Configuration File Edited

```bash
sudo nano /etc/fail2ban/jail.local
```

## SSH Jail Configuration

```ini
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = %(sshd_log)s
maxretry = 3
bantime = 10m
findtime = 10m
```

## Service Commands

```bash
sudo systemctl restart fail2ban
sudo fail2ban-client status sshd
```

## Description
Fail2Ban was configured to monitor SSH login attempts and temporarily ban IP addresses after repeated failed login attempts. This provides protection against brute-force attacks.

## Evidence


<img width="1919" height="1126" alt="week5-fail2ban-working" src="https://github.com/user-attachments/assets/f4e1418b-41b8-4aa3-8280-33255cdf99a5" />


---


# 5. Security Summary

The Ubuntu server was successfully hardened using:

- UFW firewall restrictions
- SSH hardening techniques
- AppArmor mandatory access control
- Fail2Ban intrusion prevention

These measures significantly improved system security and reduced attack exposure.

---

# Learning Outcomes

- Learned Linux firewall configuration using UFW
- Understood SSH security best practices
- Configured Fail2Ban intrusion prevention
- Verified AppArmor mandatory access control
- Applied practical Linux server hardening techniques
- Improved Linux server administration and monitoring skills
