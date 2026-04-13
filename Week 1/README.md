# 🚨 SOC Lab – Threat Detection & Monitoring (Week 1)

This Task demonstrates a hands-on **Security Operations Center (SOC)** lab focused on threat detection, monitoring, and vulnerability assessment using multiple security tools.

---

## 📌 Overview

The objective of this lab was to simulate real-world SOC operations by building a small lab environment and performing network monitoring, endpoint analysis, log correlation, and vulnerability assessment.

This lab reflects the workflow of a **Tier 1 SOC Analyst**, including detection, investigation, and basic response.

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|--------|
| Snort | Network intrusion detection and alerting |
| Wazuh | SIEM for log monitoring and threat detection |
| Osquery | Endpoint visibility using SQL queries |
| Event Viewer | Windows log analysis |
| Nessus | Vulnerability scanning and assessment |
| Kali Linux | Attack simulation |
| Windows 11 | Target system |
| Metasploitable 2 | Vulnerable testing environment |
---

## 🧪 Key Activities

### 🔍 1. Intrusion Detection (Snort)
- Configured custom rules to detect:
  - SYN scans  
  - Port scans  
  - Malicious domains  
- Generated real-time alerts using simulated traffic  

---

### 💻 2. Endpoint Monitoring (Osquery)
- Queried running processes:
SELECT pid, name, path FROM processes;
- Detected multiple `cmd.exe` processes (MITRE ATT&CK T1059 simulation)

---

### 📊 3. SIEM Monitoring (Wazuh)
- Deployed Wazuh using Docker  
- Connected Kali and Windows agents  
- Monitored security events in real-time  

**Brute-force simulation:**
- Multiple failed login attempts detected  
- Alerts mapped to MITRE ATT&CK (T1078)  

---

### 🧾 4. Log Analysis (Event Viewer)
- Investigated **Event ID 4625 (Failed Login)**  

**Extracted:**
- Source IP (attacker)  
- Timestamp  
- Authentication method (NTLM)  

- Correlated logs with Wazuh alerts  

---

### ⚠️ 5. Vulnerability Assessment (Nessus)
- Scanned Metasploitable machine  

**Findings:**
- 90+ vulnerabilities  
- Critical issues (ShellShock, weak credentials, exposed services)  

---

## 🔄 SOC Workflow Demonstrated

1. Detection – Alerts from Snort & Wazuh  
2. Triage – Identify suspicious activity  
3. Investigation – Logs + endpoint analysis  
4. Correlation – SIEM + Event Viewer  
5. Response – Root cause understanding  

---

## 📈 Key Learnings

- Multi-layer visibility (Network + Endpoint + SIEM) is critical  
- SIEM improves detection speed  
- Log correlation validates real attacks  
- Weak credentials are easily exploitable  

---

## ⚠️ Challenges Faced

- Nessus consumed high resources → shifted to Windows VM  
- Osquery path issues → resolved manually  
- Snort configuration errors → corrected config path  

---

## 📂 Report

A detailed report with full steps, screenshots, and analysis is included in this repository.

---

## 🎯 Conclusion

This lab demonstrates how multiple security tools work together to provide complete visibility across network, endpoint, and logs.

It highlights the importance of **layered security and centralized monitoring** in a real SOC environment.
