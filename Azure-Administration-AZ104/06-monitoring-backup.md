Markdown
# 6. Business Continuity & Platform Monitoring Frameworks
## Deep-Dive Component Engineering | AZ-104 Certification Track

---

## Overview
This project establishes enterprise-grade data resilience, system monitoring, and real-time threat/performance diagnostics across an Azure cloud ecosystem. The architecture implements a Recovery Services Vault to orchestrate automated, secure machine state backups, ensuring data can be completely recovered in the event of ransomware attacks or system corruption. To maintain deep visibility into the infrastructure fabric, Azure Network Watcher is deployed alongside Log Analytics arrays to analyze packet flows, verify connection paths, and actively run remote packet captures to accelerate troubleshooting and ensure system uptime.

---

## Architecture

┌────────────────────────────────────────────────────────────────────────┐
│                        Azure Workload Subnet                           │
│                                                                        │
│   ┌───────────────────────┐            ┌──────────────────────────┐    │
│   │  Virtual Machine Node │            │ Network Watcher Agent    │    │
│   │  (Production App VM)  │◄───────────┤ (Live Flow / Captures)   │    │
│   └───────────┬───────────┘            └──────────────┬───────────┘    │
└───────────────┼───────────────────────────────────────┼────────────────┘
│                                       │
│ [Automated Backup Snaps]              │ [Diagnostic Streaming]
▼                                       ▼
┌───────────────────────────────────────┐┌───────────────────────────────┐
│        Recovery Services Vault        ││   Log Analytics Workspace     │
│                                       ││                               │
│  - Vault Backup Policy (Daily GFS)    ││  - Traffic Analytics Dash     │
│  - Soft Delete Protection Layer       ││  - NSG Flow Log Repositories  │
│  - Multi-Region LRS/GRS Storage Base  ││  - Network Diagnostics Center │
└───────────────────────────────────────┘└───────────────────────────────┘


---

## What Was Built

**1. Enterprise Backup Orchestration (Recovery Services Vault)**
- Provisioned a centralized **Recovery Services Vault** configured with Geo-Redundant Storage (GRS) parameters to protect backup data from regional data center disasters.
- Authored a custom **Backup Policy** implementing a grandfather-father-son (GFS) rotation scheme:
  - **Daily Recovery Point:** Captured at 11:00 PM with a strict 14-day retention rule.
  - **Weekly Recovery Point:** Captured every Sunday with an 8-week retention window.
- Registered and protected workload virtual machines, configuring native extension injections to stream application-consistent snapshots to the vault without interrupting active user operations.

**2. Network Path Diagnostics Automation**
- Activated **Azure Network Watcher** across active subscription regions to monitor networking health.
- Utilized the **Connection Troubleshoot** API to dynamically audit structural network communication paths between application compute tiers and remote backend storage resources, isolating latency issues and configuration blocks.

**3. Remote Packet Interception and Traffic Analytics**
- Deployed Network Watcher packet capture pipelines directly onto active production servers.
- Configured targeted capture filters to generate standardized `.cap` files during active performance alerts, saving trace assets directly into secure storage accounts for root-cause troubleshooting.
- Implemented **NSG Flow Logs** mapped to a centralized Log Analytics Workspace, enabling Traffic Analytics to visualize application protocols, active connection states, and rogue geolocation access attempts.

---

## Technologies and Services Used

| Component Category | Tool / Service Name | Specific Operational Role |
|---|---|---|
| **Backup Storage** | Recovery Services Vault | Centralizes, encrypts, and retains system images and system snapshots. |
| **Data Protection** | Azure Backup | Executes policy-driven infrastructure snapshots across hybrid systems. |
| **Diagnostics Hub** | Azure Network Watcher | Inspects packet pathways, tests port access, and captures live traffic. |
| **Log Centralization**| Log Analytics Workspace | Collects and aggregates infrastructure logs and platform metrics. |
| **Visualization** | Traffic Analytics | Provides charts and visual maps parsing NSG flow logs for security analysis. |

---

## Key Concepts Demonstrated / Business Impact

* **RPO and RTO Minimization:** Implementing automated backup policies ensures low Recovery Point Objectives (RPO - how much data you lose) and rapid Recovery Time Objectives (RTO - how fast you recover), allowing an enterprise to quickly restore business operations from data corruption.
* **Proactive Security Auditing via Flow Logs:** NSG Flow Logs track the source IP, destination IP, port number, and protocol of every packet hitting a subnet. This gives security teams the exact telemetry needed to spot network scanning, brute-force attempts, or unauthorized cross-subnet traffic.
* **Accelerated MTTR (Mean Time to Resolution):** Instead of logging into a server and installing custom tools to diagnose an application drop, Network Watcher tools can run remote packet captures and port checks instantly from the cloud console, slashing the time it takes to find and fix bugs.
* **Defense Against Ransomware:** Storing system state copies inside an isolated Recovery Services Vault ensures that even if a server's local operating system is encrypted by ransomware, clean snapshots are protected in a separate cloud tier to enable safe, uncorrupted rollbacks.

---

## Note to Self

* **Soft Delete Safeguard:** By default, Recovery Services Vaults have **Soft Delete** turned on. If a compromised administrator account or an attacker tries to delete a system backup, the data is retained securely for an extra 14 days, allowing you to stop the deletion and restore your infrastructure.
* **VHD Expansion Limits:** Remember that if you alter or expand the size of a virtual machine's underlying Managed Disk OS partition, the Azure Backup agent might fail out on its next scheduled snapshot cycle. You must run a manual backup check or trigger a re-registration flow to re-align the storage profiles.
* **VM Extension Requirement:** To run Network Watcher features like Packet Capture or Next Hop checks, the target virtual machine **must** have the `NetworkWatcherAgentWindows` or `NetworkWatcherAgentLinux` VM extension installed and running, and outbound Port 443 must be completely open to the Network Watcher service endpoints.
