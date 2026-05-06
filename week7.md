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


1. Fail2Ban active service status verification 
<img width="1919" height="1124" alt="week7-fail2ban-status" src="https://github.com/user-attachments/assets/cc41b989-7200-4f1f-a201-87e97d26a388" />


2. Lynis security audit results and hardening index
<img width="1915" height="1132" alt="week7-lynis-improved-score" src="https://github.com/user-attachments/assets/4ca01bb9-0eba-4686-a17f-72e53263b4e7" />


3. Nmap network scan and open port analysis
<img width="1705" height="1123" alt="week7-nmap-scan" src="https://github.com/user-attachments/assets/73e7037c-a1ef-4709-a4ff-22ecca2db990" />


4. Running system services verification
<img width="1405" height="1125" alt="week7-running-services" src="https://github.com/user-attachments/assets/64cde811-b58b-4105-8079-add464261edd" />


5. Security controls and firewall configuration validation
<img width="1853" height="1133" alt="week7-security-controls" src="https://github.com/user-attachments/assets/eca182c7-513c-47cc-ad54-1cb807391b10" />
   
---

# Conclusion

This week focused on security auditing and monitoring of the Ubuntu server environment. Security scanning tools such as Lynis and Nmap were used to assess the system’s security posture and identify exposed services. Firewall policies, intrusion prevention mechanisms, and active services were verified successfully. The implemented hardening controls improved the overall system security and monitoring capability of the server.
