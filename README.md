# SOC Lab – Attack Detection Report

## Overview

This project demonstrates simulated cyber attacks performed from Kali Linux against Ubuntu and Windows virtual machines. Wazuh was used as the SIEM platform to detect and analyze malicious activities.

## Lab Environment

* Kali Linux (Attacker + Wazuh Manager)
* Ubuntu (Target)
* Windows 11 (Target)
* Metasploitable (Target)
* DVWA (Target)
* VirtualBox Host-only Network

## Attacks Performed

* Network Enumeration (Nmap)
* SSH Brute Force Attack (Ubuntu)
* RDP Brute Force Attack (Windows)

## Detection

Wazuh successfully detected:

* Authentication failures
* Suspicious login attempts
* Privileged operation failures

## Tools Used

* Kali Linux
* Wazuh SIEM
* Hydra
* Nmap
* VirtualBox

## Timeline

| Time  | Activity                         | Target  |
| ----- | -------------------------------- | ------- |
| 06:45 | Nmap Scan                        | Ubuntu  |
| 06:57 | SSH Brute Force                  | Ubuntu  |
| 07:00 | Authentication Failures Detected | Ubuntu  |
| 07:39 | RDP Brute Force                  | Windows |
| 07:45 | Wazuh Alert                      | Windows |

## Report

Full report available in:
`SOC Lab - Week 2.pdf`

