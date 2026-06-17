# Windows Baselining Lab

> *Know normal. Find evil.*

An Azure lab environment for understanding default Windows behaviour through telemetry collection and KQL analysis. Inspired by [Baselining Windows To Blend In](https://blog.zsec.uk/baselining-windows/) by Andy Gill (ZephrFish).

---

## Purpose

Before you can write reliable detections, you need to understand what Windows *actually* does. What happens at rest, at startup, and under normal user activity before being compromised.

This lab provides a controlled environment to:

- Collect Windows telemetry from clean, known-good machines
- Build frequency tables and process lineage maps of default OS behaviour
- Identify what's normal so deviations become meaningful signals
- Practice KQL across Azure Data Explorer and Log Analytics
- Develop and validate detection content grounded in observed reality

APTs blend into normal Windows noise. You can only spot what doesn't belong if you know what belongs.

---

## Architecture

```
Windows VMs (Azure)
    │
    ├── Sysmon
    ├── Windows Event Logs
    └── PowerShell Script Block Logging
         │
         ▼
    Azure Monitor Agent
    Data Collection Rules
         │
         ▼
    Log Analytics Workspace
         │
         ├── Microsoft Sentinel (hunting + analytics rules)
         └── Continuous Export
              │
              ▼
         Azure Data Explorer (ADX)
         (long-term retention, free-form KQL analysis)
```

---

## Lab Components

### Infrastructure

| Component | Purpose |
|---|---|
| Windows 11 VM | Workstation baseline |
| Windows Server 2022 VM | Server baseline |
| Log Analytics Workspace | Telemetry collection and query hub |
| Microsoft Sentinel | Detection engineering, hunting workbooks |
| Azure Data Explorer | Cheap long-term storage, raw schema exploration |

### Telemetry Sources

| Source | Key Signal | Event IDs of Interest |
|---|---|---|
| Windows Security Log | Logon events, process creation, privilege use | todo |
| Sysmon | Process tree, network connections, file/registry writes | todo |
| PowerShell | Script block content, module loads, remoting | todo |
| System Log | Service installs, driver loads, crashes | todo |

---

## What We're Baselining

The goal is to build a documented picture of default Windows behaviour across these areas:

- **Process lineage** - what spawns what, under which conditions (`services.exe → svchost.exe` is expected; `Word.exe → powershell.exe` is not)
- **Scheduled tasks** - What are the default ones? What could an attacker change
- **Running services** - default vs domain-joined vs user-installed
- **Network beaconing** - Windows Update, telemetry endpoints, DNS, NTP - what calls out, how often?
- **LOLBin activity** - How do typical LOLBAS executables ( `certutil.exe`, `mshta.exe`, or `wscript.exe`) work on a clean machine?
- **PowerShell usage** - what modules load at startup, what commands run, what encoding patterns appear

---

## Repository Structure

```
todo
```

---

## Getting Started

### Prerequisites

- Azure subscription (Free tier or Pay-as-you-go)
- KQL familiarity
- todo

---

## Learning Objectives

Working through this lab should leave you able to:

- [ ] Understand what each Sysmon event ID captures and why it matters
- [ ] Understand which apps make network connections, how and why
- [ ] Describe the normal parent-child process tree for a Windows workstation
- [ ] Identify which LOLBins fire on a clean Windows install and what they do
- [ ] Write KQL frequency queries

---

## References

- [Baselining Windows To Blend In - ZephrFish / ZSec](https://blog.zsec.uk/baselining-windows/)
- [MITRE ATT&CK - Defense Evasion: LOLBins](https://attack.mitre.org/tactics/TA0005/)
---

## Notes