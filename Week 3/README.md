# 🛡️ SOC Lab — Advanced Detection & Incident Response

### Log Analysis · Threat Intelligence · Capstone Simulation

![SIEM](https://img.shields.io/badge/SIEM-Wazuh-0078D4?style=flat-square)
![IR](https://img.shields.io/badge/IR-TheHive-FF6B00?style=flat-square)
![Attacker](https://img.shields.io/badge/Attacker-Kali_Linux-557C94?style=flat-square)
![Exploit](https://img.shields.io/badge/Exploit-Metasploit-E34F26?style=flat-square)
![Threat Intel](https://img.shields.io/badge/Threat_Intel-OTX-4CAF50?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)

---

## 📋 Overview
This lab demonstrates an end-to-end SOC workflow including detection, investigation, escalation, and response.  
A simulated attack was launched using Metasploit, detected by Wazuh SIEM, enriched with threat intelligence, and escalated using TheHive.

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
| Kali Linux | 2026.1 | Primary Attack / Analyst VM — 192.168.56.102 |
| Windows 11 Pro | 10.0.26100 | Target Endpoint — 192.168.56.105 | 
| Metasploitable2 | Ubuntu 8.04 | Vulnerable Target — 192.168.56.107 |

---

## 🔍 Key Activities
- Advanced Log Correlation  
- Custom Anomaly Detection Rule  
- Threat Intelligence Integration  
- Alert Triage & IOC Validation  
- Threat Hunting (MITRE ATT&CK)  
- Incident Escalation (TheHive)  
- Evidence Preservation  
- Capstone Attack Simulation  
- Incident Response & Containment  

---

## 🚨 Incident Summary
**Attack:** Samba Exploit (CVE-2007-2447)  
**Source:** Kali Linux  
**Target:** Metasploitable2  
**Result:** Root shell obtained  

### Response Actions
- Alert detected in Wazuh  
- Incident escalated to TheHive  
- Attacker IP blocked  
- Target isolated  
- Evidence collected  

---

## 📁 Repository Structure
```
Week 3
├── README.md
├── SOC_Lab_Final_Report_week_3.pdf
└── images/
```

---

## 🎯 Skills Demonstrated
- SOC Monitoring  
- Threat Detection  
- Incident Investigation  
- Threat Intelligence Usage  
- MITRE ATT&CK Mapping  
- Evidence Collection  
- Incident Response Workflow  

---

## 📄 Documentation
Detailed report and screenshots are included in this repository.

---

> Security is not a product, but a process.
