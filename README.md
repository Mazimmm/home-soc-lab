# 🛡️ Home SOC Lab — Wazuh SIEM + Detection Engineering

A fully functional Security Operations Center built on a laptop using VMware, 
Wazuh 4.9.2, Sysmon, and custom detection rules mapped to MITRE ATT&CK.

---

## 🏗️ Lab Architecture

| VM | Role | IP |
|----|------|----|
| Ubuntu Server 22.04 | SOC Manager (Wazuh SIEM) | 192.168.48.128 |
| Windows 10 | Victim Endpoint (Wazuh Agent + Sysmon) | 192.168.48.131 |
| Kali Linux | Attacker | 192.168.48.132 |

**Stack:** VMware · Wazuh 4.9.2 (Docker) · Sysmon (SwiftOnSecurity config)

---

## ✅ Phases Completed

| Phase | Description | Status |
|-------|-------------|--------|
| 1 | Lab foundation — 3 VMs, isolated network | ✅ Done |
| 2 | Wazuh SIEM deployed via Docker | ✅ Done |
| 3 | Windows agent + Sysmon telemetry | ✅ Done |
| 4 | First attacks — nmap, RDP brute force, encoded PowerShell | ✅ Done |
| 5 | Custom detection rules (T1059.001) | 🔄 In Progress |

---

## 📁 Repo Structure
