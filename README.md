# SOC Lab – Attack Detection Report

## Overview

This project demonstrates simulated cyber attacks performed from Kali Linux against Ubuntu and Windows virtual machines. Wazuh was used as the SIEM platform to detect and analyze malicious activities in real time.

## Lab Environment

| Machine | Role | IP Address | OS |
|---------|------|-----------|-----|
| Kali Linux | Attacker + Wazuh Server | 192.168.56.103 | Kali Linux 2026 |
| Ubuntu | Target | 10.0.3.15 / 192.168.56.110 | Ubuntu 20.04.6 LTS |
| Windows 11 | Target | 192.168.56.105 | Windows 11 Pro 10.0.26100 |
| Metasploitable | Vulnerable Target | 192.168.56.101 | Linux (Metasploitable2) |
| DVWA / Web App | Web Target | 192.168.56.104 | Linux/Apache |

## Attacks Performed

| # | Attack | Tool | Target | MITRE Technique |
|---|--------|------|--------|----------------|
| 1 | Network Enumeration (full port scan) | Nmap | Metasploitable | T1046 |
| 2 | SMB OS Discovery | Nmap Script | Windows | T1046 + T1135 |
| 3 | Web Directory Enumeration | Gobuster | Web Server | T1083 |
| 4 | Web Vulnerability Scan | Nikto | Web Server | T1595.003 |
| 5 | SSH Brute Force | Hydra | Ubuntu | T1110.001 |
| 6 | RDP Brute Force | Hydra | Windows | T1110.001 |

## Detection

Wazuh successfully detected all attack phases:

- **Ubuntu Agent** — 795 total events | 11 authentication failures detected
- **Windows Agent** — 552 total events | Failed privileged operations detected
- Alerts triggered within 3–6 minutes of each attack starting

## Tools Used

- Kali Linux — Attacker machine
- Wazuh v4.7.5 — SIEM / XDR platform
- Nmap 7.98 — Network and port scanning
- Gobuster v3.0.2 — Web directory enumeration
- Nikto v2.6.0 — Web vulnerability scanner
- Hydra v9.6 — Brute force password attacks
- AlienVault OTX — Threat intelligence validation

## Timeline

| Time | Activity | Target | 
|------|----------|--------|
| 2026-03-26 06:44 | Wazuh agents verified active | Ubuntu + Windows | 
| 2026-03-26 06:45 | Nmap full port scan (-p-) | Metasploitable | 
| 2026-03-26 12:53 | Gobuster directory enumeration | Web Server |
| 2026-03-26 12:53 | Nikto web vulnerability scan | Web Server |
| 2026-03-26 13:00 | Nmap SMB OS discovery script | Windows | 
| 2026-03-27 06:57 | SSH Brute Force via Hydra | Ubuntu | 
| 2026-03-27 07:00 | Authentication failures detected | Ubuntu | 
| 2026-03-27 07:45 | RDP Brute Force via Hydra | Windows | 
| 2026-03-27 07:39 | Failed privileged ops detected | Windows | 

## Key Findings

### Web Server (192.168.56.104)
- phpMyAdmin publicly accessible — database compromise risk
- SVN repository exposed at /.svn/entries — source code leak
- Apache mod_status and mod_info open — server internals exposed
- 5 missing security headers
- PHP version 5.3.1 disclosed — outdated and vulnerable
- Total: 38 issues found by Nikto

### Metasploitable (192.168.56.101)
- 30+ open ports including FTP (21), Telnet (23), VNC (5900)
- vsftpd 2.3.4 — known backdoor (CVE-2011-2523)
- UnrealIRCd — known backdoor (CVE-2010-2075)
- Root bindshell on port 1524

### Brute Force Attacks
- SSH: 14,344,399 password attempts — Wazuh detected in 3 minutes
- RDP: 14,344,399 password attempts — Wazuh detected failed privileged ops

## Security Recommendations

| # | Recommendation | Priority |
|---|---------------|---------|
| 1 | Account lockout after 5 failed attempts | High |
| 2 | Deploy fail2ban on Ubuntu | High |
| 3 | Enable Wazuh Active Response (auto-block IPs) | High |
| 4 | SSH key-based auth only — disable password login | High |
| 5 | Disable RDP if not needed; enable NLA | High |
| 6 | Restrict phpMyAdmin to localhost only | Critical |
| 7 | Disable public SVN directory access | High |
| 8 | Add missing security headers to Apache | Medium |
| 9 | Upgrade PHP from 5.3.1 to supported version | Critical |
| 10 | Configure Wazuh email/Slack alerts for High events | Medium |

## Evidence

All screenshots are stored in the `/images` folder:

| File | Description |
|------|-------------|
| Wazuh-Agents.png | Wazuh agents — Ubuntu + Windows active |
| active_listening_ports.png | netstat -tulnp output |
| services_with_pid_details.png | ss -tulnp root view |
| nmap_scan.png | Nmap full port scan on Metasploitable |
| nmap_smb_os_discovery.png | SMB OS discovery on Windows |
| gobuster_discovery_scan.png | Gobuster web directory scan |
| nikto_scan(part 1).png | Nikto scan — server details |
| nikto_scan(part 2).png | Nikto scan — phpMyAdmin, SVN issues |
| ssh-bruteforce.png | Hydra SSH brute force attack |
| rdp-bruteforce.png | Hydra RDP brute force attack |
| ubuntu-alerts.png | Wazuh ubuntu-agent dashboard |
| windows-alert.png | Wazuh Windows-SOC-Lab dashboard |

## Report

Full detailed report available in: `SOC Lab – Week 2 .pdf`

