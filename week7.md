# Week 7 – Security Audit and Monitoring

[← Week 6](week6.md) | [Back to Home](index.md)

---

## Objective
The objective of this week was to perform security auditing and monitoring on the Ubuntu server environment. This included vulnerability scanning, firewall verification, intrusion prevention monitoring, running service auditing, and system hardening assessment using Lynis.

---

# Tasks Performed

## 1. Updated System Packages

The package repositories were updated before performing security scans and auditing.

### Command Used
```bash
sudo apt update
```

---

## 2. Installed Lynis Security Auditing Tool

Lynis was installed to perform a complete security audit and hardening assessment of the system.

### Command Used
```bash
sudo apt install lynis -y
```

---

## 3. Performed System Security Audit

A full system audit was performed using Lynis.

### Command Used
```bash
sudo lynis audit system
```

### Result
The audit successfully scanned the server and generated a hardening index score along with security recommendations.

---

## 4. Verified Lynis Hardening Results

The final Lynis audit results were checked to verify the hardening index and system security status.

### Command Used
```bash
sudo grep "Hardening index" /var/log/lynis.log
```

### Result
The system achieved a hardening index score of 62 after implementing firewall configuration, SSH hardening, Fail2Ban intrusion prevention, AppArmor enforcement, and service auditing.

---

## 5. Performed Network Port Scan Using Nmap

Nmap was used to identify open network ports and verify running services.

### Command Used
```bash
nmap 192.168.56.106
```

### Result
The scan confirmed that only the required services such as SSH and HTTP were open.

---

## 6. Verified Fail2Ban Protection

Fail2Ban status was checked to confirm that SSH intrusion prevention was active.

### Command Used
```bash
sudo fail2ban-client status sshd
```

### Result
The SSH jail was active and monitoring failed login attempts.

---

## 7. Verified Firewall Rules

The UFW firewall configuration was checked to confirm secure firewall policies.

### Command Used
```bash
sudo ufw status verbose
```

### Result
The firewall was active and configured to allow only required incoming connections.

---

## 8. Audited Running Services

Active running services were reviewed to verify important security-related services.

### Command Used
```bash
systemctl list-units --type=service --state=running
```

### Result
Critical services such as SSH, Nginx, Fail2Ban, rsyslog, and unattended upgrades were confirmed to be running.

---

## 9. Verified Fail2Ban Service Status

The Fail2Ban service status was checked to ensure the intrusion prevention service was operational.

### Command Used
```bash
sudo systemctl status fail2ban
```

---

## 10. Verified Nginx Service Status

The Nginx web server service was checked to confirm that the web service was active.

### Command Used
```bash
sudo systemctl status nginx
```

---

# Security Improvements Implemented

- Firewall configuration using UFW
- SSH hardening configuration
- Fail2Ban intrusion prevention
- AppArmor enforcement
- Network service auditing
- Vulnerability scanning using Nmap
- System security auditing using Lynis
- Running service monitoring

---

# Evidence / Screenshots


1. `week7-lynis-scan.png`       


2. `week7-lynis-improved-score.png`


3. `week7-nmap-scan.png`


4. `week7-firewall-status.png`


5. `week7-fail2ban-jail.png`


6. `week7-running-services.png`


7. `week7-fail2ban-status.png`


8. `week7-nginx-status.png`

---

# Conclusion

This week focused on security auditing and monitoring of the Ubuntu server environment. Security scanning tools such as Lynis and Nmap were used to assess the system’s security posture and identify exposed services. Firewall policies, intrusion prevention mechanisms, and active services were verified successfully. The implemented hardening controls improved the overall system security and monitoring capability of the server.
