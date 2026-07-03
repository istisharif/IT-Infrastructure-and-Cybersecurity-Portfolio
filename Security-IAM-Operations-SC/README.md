# SC-200, 300: Security Operations, Identity & Access Lab Documentation

## 🏗️ SecOps Ecosystem & Azure Sentinel Architecture Overview
This deployment models a cloud-native Security Operations Center (SOC) infrastructure. It focuses on centralizing security information and event management (SIEM), configuring enterprise platform defenses, orchestrating hybrid cross-platform log pipelines, and conducting proactive threat-hunting operations using Kusto Query Language (KQL).

---

## 🚀 Lab Configuration Stages & Verification

### 1. Inbound Threat Engineering & Email Presets
* **Implementation:** Deployed baseline platform protection profiles using Microsoft Defender preset security policies. 
* **Hardening Controls:** Built strict domain impersonation blocks and configured anti-malware zero-hour auto-purge parameters to intercept, isolate, and neutralize malicious script and executable attachments before delivery.

### 2. Proactive Threat Hunting & Telemetry Auditing
* **Implementation:** Spearheaded proactive incident detection routines across enterprise endpoints and messaging databases.
* **Query Design:** Structured advanced, multi-table KQL hunting queries to parse raw endpoint event metrics, tracking behavior patterns matching lateral movement indicators or suspicious file creations.

### 3. Centralized SIEM Log Collection & Analytic Ingestion
* **Implementation:** Provisioned a cloud-native Microsoft Sentinel SIEM workspace. Integrated security data streams by routing stateful firewall diagnostics and cloud-native App Service event streams into Sentinel.
* **Alert Engineering:** Synthesized raw log telemetry into actionable incidents by scripting scheduled analytic detection rules mapped to known threat indicators.

### 4. Hybrid Architecture Log Ingestion Pipelines
* **Implementation:** Engineered an enterprise-wide logging framework spanning diverse infrastructure footprints. Deployed and configured Log Analytics agents on localized Windows Active Directory Domain Controllers and Red Hat Enterprise Linux (RHEL) systems.
* **Log Streaming:** Aggregated and streamed raw Windows Security Events and Linux system logs directly into cloud SIEM data tables for analysis.

### 5. Multi-Cloud Asset Onboarding & Vulnerability Management
* **Implementation:** Onboarded external hybrid server infrastructure into the unified cloud management pane via Azure Arc.
* **Vulnerability Assessment:** Conducted system configuration vulnerability assessments across enrolled instances, generating automated Microsoft Sentinel alert triggers targeting anomalies like recurring failed RDP/SSH authentication attempts.

---

## 🛠️ Security Frameworks & Core Technologies Verified
* **SIEM / SOAR:** Microsoft Sentinel Workspace, Analytic Ingestion Policies, Custom Automation Rules
* **XDR & Endpoint Security:** Microsoft Defender for Endpoint, Email & Collaboration Protection, Domain Impersonation Defense
* **Threat Hunting:** Kusto Query Language (KQL), Log Analytics Workspace Tables (`SecurityEvent`, `Syslog`, `EmailEvents`)
* **Hybrid Security & Governance:** Azure Arc Server Enrollment, Multi-Platform Log Analytics Agents (Windows Server / RHEL)
