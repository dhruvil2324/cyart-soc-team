# 🛡️ SOC Lab — Week 3
### Advanced Log Analysis · Threat Intelligence · Capstone Simulation

![Wazuh](https://img.shields.io/badge/SIEM-Wazuh_4.7.5-0078D4?style=flat-square&logo=elasticsearch&logoColor=white)
![TheHive](https://img.shields.io/badge/IR_Platform-TheHive_5.2-FF6B00?style=flat-square)
![Kali](https://img.shields.io/badge/Attacker_VM-Kali_Linux_2026.1-557C94?style=flat-square&logo=kalilinux&logoColor=white)
![Metasploit](https://img.shields.io/badge/Exploit-Metasploit_6.4-E34F26?style=flat-square)
![OTX](https://img.shields.io/badge/Threat_Intel-AlienVault_OTX-4CAF50?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)

---

## 📋 Overview

This project documents the **Week 3 SOC Analyst Lab** covering advanced detection, threat intelligence integration, incident escalation, and a full end-to-end capstone attack simulation.

All activities were performed in a controlled virtual lab environment using Kali Linux as the attacker/analyst machine, Windows 11 as an endpoint agent, and Metasploitable2 as the vulnerable target — with **Wazuh SIEM deployed via Docker**.

---

## 🖥️ Lab Environment

| Tool | Version | Role |
|------|---------|------|
| Wazuh SIEM | 4.7.5 | Security Information & Event Management |
| TheHive | 5.2.16-1 | Incident Response & Case Management |
| AlienVault OTX | API v1 | Threat Intelligence Feed |
| VirusTotal | Web API | IOC Validation |
| Metasploit | 6.4.116-dev | Attack Simulation |
| Velociraptor | 0.7.0 | Digital Forensics & Evidence Collection |
| Kali Linux | 2026.1 | Primary Attack / Analyst VM — `192.168.56.102` |
| Windows 11 Pro | 10.0.26100 | Target Endpoint — `192.168.56.105` |
| Metasploitable2 | Ubuntu 8.04 | Vulnerable Target — `192.168.56.107` |


---

## 🔍 Key Findings

### Log Correlation — T1078 Attack Chain Detected

| Timestamp | Event ID | Source IP | Destination IP | Notes |
|-----------|----------|-----------|----------------|-------|
| 2026-04-05 08:44:00 | 4625 | 192.168.56.105 | 192.168.56.102 | Failed login — wrong password |
| 2026-04-05 08:45:00 | 4625 | 192.168.56.105 | 192.168.56.102 | Repeated auth failure — T1078 |
| 2026-04-06 01:33:58 | 4673 | 192.168.56.105 | 192.168.56.102 | Privileged operation attempt |
| 2026-04-06 01:34:00 | 4624 | 192.168.56.105 | 192.168.56.102 | Windows logon success — T1078 |

### Custom Anomaly Detection Rule

- **Rule ID:** 100300
- **Description:** High volume data transfer detected — Anomaly
- **Pattern:** `bytes_out` monitoring via `if_sid 530`
- **Groups:** `local, anomaly` | **MITRE Mapping:** T1041 (Exfiltration Over C2 Channel)

### Capstone — Samba Exploit (CVE-2007-2447)

```
Exploit:  exploit/multi/samba/usermap_script
Target:   Metasploitable2 — 192.168.56.107
Attacker: Kali Linux — 192.168.56.102
Result:   Root shell obtained (uid=0, gid=0)
Session:  192.168.56.102:4444 → 192.168.56.107:39243
```

### Evidence Chain of Custody

| Item | Collected By | Date | SHA256 Hash |
|------|-------------|------|-------------|
| netstat_final.csv | SOC Analyst Dhruv | 2026-04-06 | `1c6d82cd2dd52c787885acc920ec3932...` |
| memory_dump.bin | SOC Analyst Dhruv | 2026-04-06 | `c036cbb7553a909f8b8877d446192430...` |
| evidence.txt | SOC Analyst Dhruv | 2026-04-06 | `83f632bece4e03b45b428ac7e566673...` |

---

## 🚨 Incident Report Summary

**Title:** Samba Exploit — Metasploitable2 Compromise
**Severity:** 🔴 Critical | **MITRE:** T1210 (Exploitation of Remote Services), T1078

**Timeline:**
- `10:12` — Wazuh SIEM detected Samba exploit attempt from `192.168.56.102`
- `10:12` — Root shell session established on Metasploitable2
- `10:15` — Incident escalated via TheHive (Case #2)
- `10:17` — Attacker IP blocked using iptables on target VM
- `10:20` — Evidence collected and hashed for chain-of-custody

**Response Actions:** IP blocked via iptables · VM network isolated · TheHive Tier 2 task assigned · Forensic evidence preserved

---

## 📁 Repository Structure

```
📦 Week 3
 ┣ 📄 README.md
 ┣ 📄 SOC_Lab_Final_Report_week_3.pdf
 ┗ 📁 images/
    ┣ wazuh_dashboard.png
    ┣ failed_login_4625.png
    ┣ custom_rule_100300.png
    ┣ thehive_case.png
    ┣ metasploit_shell.png
    ┗ evidence_hash.png
```

---

## 📚 References

- [Wazuh Official Documentation](https://documentation.wazuh.com)
- [TheHive Project Docs](https://docs.strangebee.com/thehive/)
- [AlienVault OTX API](https://otx.alienvault.com/api)
- [MITRE ATT&CK Framework](https://attack.mitre.org)
- [CVE-2007-2447 — Samba usermap_script](https://nvd.nist.gov/vuln/detail/CVE-2007-2447)
- [NIST SP 800-61 — Incident Handling Guide](https://csrc.nist.gov/)
- [Metasploit Unleashed](https://www.offensive-security.com/metasploit-unleashed/)


---

> *"Security is not a product, but a process." — Bruce Schneier*
