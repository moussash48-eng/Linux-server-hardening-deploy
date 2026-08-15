# 🚀 Production-Ready Linux Server Setup & Deployment

A secure, hardened, and containerized Linux server environment designed for hosting production web applications with high availability and security.

---

## 🛠️ Tech Stack & Architecture
* **OS:** Linux (Debian / Kali environment)
* **Web Server & SSL:** Nginx with TLS 1.3 encryption & automatic HTTP-to-HTTPS (301) redirection
* **Containerization:** Docker container runtime with isolated application environments
* **Security & Hardening:** UFW Firewall, ED25519 SSH Key-Only Authentication, Fail2ban Intrusion Prevention
* **Automation:** Automated daily backup Bash script managed via Cron jobs
* **Monitoring:** Real-time resource tracking via `htop` and systemd logs

---

## 🔒 Security Implementations
1. **SSH Hardening:** Disabled password logins (`PasswordAuthentication no`) and enforced public-key authentication.
2. **Firewall (UFW):** Restricted open ports to only essential services (`22/SSH`, `80/HTTP`, `443/HTTPS`).
3. **Fail2ban:** Active jail monitoring on the SSH daemon to automatically ban brute-force IP addresses.

---

## 🌐 Web Server & Reverse Proxy Architecture
* Configured Nginx Server Blocks to route domain traffic.
* Implemented Nginx as a **Reverse Proxy** passing incoming secure HTTPS traffic to internal Docker containers (`127.0.0.1:8080`).
* Forwarded client headers (`Host`, `X-Real-IP`, `X-Forwarded-For`, `X-Forwarded-Proto`).

---

## ⚙️ Automated Backup Script
A lightweight Bash script (`backup.sh`) archives critical Nginx configurations and web directories, scheduled via `crontab`:
```bash
0 2 * * * /bin/bash /home/moussa/backup.sh > /dev/null 2>&1
'''
