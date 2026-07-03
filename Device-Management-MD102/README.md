# MD-102: Endpoint & Device Management Administrator Lab Documentation

## 🏗️ Enterprise Endpoint Infrastructure Overview
This deployment validates advanced engineering competencies across cloud-native and on-premises unified endpoint management (UEM) systems. Configurations span Microsoft Intune compliance frameworks, cloud onboarding pipelines, legacy software packaging, and the construction of a multi-site Microsoft Endpoint Configuration Manager (MECM/SCCM) hierarchy.

---

## 🚀 Lab Configuration Stages & Verification

### 1. Cloud Device Compliance & Cryptographic Enforcement
* **Implementation:** Engineered cloud-based endpoint compliance policies within Microsoft Intune to mandate cryptographic standards across corporate computing nodes.
* **Security Baselines:** Enforced hardware-level protections by requiring active Trusted Platform Module (TPM 2.0) verification, secure boot sequences, and full-disk BitLocker encryption policies prior to granting tenant access resources.

### 2. Fleet Hardening & Patch Management
* **Implementation:** Hardened distributed Windows endpoints by deploying Microsoft Security Baselines to restrict local system attack surfaces.
* **Update Orchestration:** Configured Intune Windows Update Rings to automate patch deployments, balancing risk mitigation with deployment stability through targeted quality/feature deferrals and strict compliance deadlines.

### 3. Automated Zero-Touch Provisioning (Windows Autopilot)
* **Implementation:** Architected a zero-touch operating system deployment pipeline to automate corporate endpoint provisioning.
* **Script Automation:** Executed administrative PowerShell scripts to harvest unique hardware hashes from bare-metal devices, uploaded hardware identifiers to the tenant, and mapped custom Windows Autopilot deployment profiles to execute user-driven cloud enrollment sequences.

### 4. Application Packaging & Modern Ingestion Pipelines
* **Implementation:** Engineered distribution mechanics for legacy enterprise client applications into cloud-native channels.
* **Compilation:** Utilized the Microsoft Win32 Content Prep Tool to transform unmanaged installer strings into secure, encrypted `.intunewin` software packages, defining silent command-line parameters and custom application detection rules for enterprise deployment.

### 5. Multi-Tier MECM (SCCM) Topology & Network OS Imaging
* **Implementation:** Designed and deployed a multi-tier Microsoft Endpoint Configuration Manager (MECM) infrastructure featuring a Central Administration Site (CAS), Primary Site, and integrated Active Directory Domain Services (AD DS).pdf].
* **Deployment & Distribution:** Configured site distribution points with network PXE-responder services and boot package data access configurations to execute high-capacity, automated bare-metal operating system imaging over the LAN.pdf].
* **Application Injection:** Developed complex Task Sequences to seamlessly couple network OS installations with the silent installation of enterprise `.exe` and `.msi` application bundles during the system provisioning phase.

---

## 🛠️ Endpoint Engineering Toolsets & Core Technologies
* **Cloud UEM Platforms:** Microsoft Intune (Endpoint Manager), Microsoft Entra Identity, Windows Autopilot
* **On-Premises Infrastructure:** Microsoft Endpoint Configuration Manager (MECM/SCCM), Central Administration Site (CAS), Primary Site Topology.pdf]
* **Security & Compliance:** BitLocker Encryption, Trusted Platform Module (TPM 2.0), Windows Security Baselines, Update Rings
* **Packaging & Provisioning:** Microsoft Win32 Content Prep Tool (`.intunewin`), Task Sequence Architecture, PXE Boot Operations, `.msi` & `.exe` Packaging
