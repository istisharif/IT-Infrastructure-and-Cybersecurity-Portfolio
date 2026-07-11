Markdown
# 1. Hybrid Identity Infrastructure
## Deep-Dive Component Engineering | AZ-104 Certification Track

---

## Overview
This project connects a company's on-premises office directory (Active Directory Domain Services) with the Microsoft Azure cloud directory (Microsoft Entra ID). The goal is to create a single, unified identity system so employees can use one username and password to log into both local office equipment and cloud-based business applications[cite: 1]. It includes security safeguards like Multi-Factor Authentication (MFA) to prevent unauthorized access and Self-Service Password Reset (SSPR) to allow users to securely manage their own credentials[cite: 1].

---

## Architecture

+───────────────────────────────+
|  On-Premises Windows Server   |
|  Active Directory (AD DS)     |
+───────────────┬───────────────+
│
│  [Outbound HTTPS Port 443]
│  Password Hash Sync (PHS)
▼
+───────────────────────────────+
|  Azure AD Connect Sync Engine |
+───────────────┬───────────────+
│
│  [Bi-Directional Encrypted Tunnel]
│  Real-Time Password Writeback
▼
+───────────────────────────────+
|       Microsoft Entra ID      |
|  Cloud Identity Control Plane |
+───────────────────────────────+
│
▼
- Multi-Factor Authentication (MFA)
- Self-Service Password Reset (SSPR)


---

## What Was Built

**1. Directory Synchronization Pipeline**
- Deployed and configured the Azure AD Connect synchronization agent on a local Windows Server instance to bridge the gap between on-premises and cloud registries[cite: 1].
- Enforced Password Hash Synchronization (PHS) to automatically copy encrypted user credential states up to the cloud directory[cite: 1].
- Scheduled a 30-minute delta replication cycle to capture automated identity additions, changes, and deletions across platforms.

**2. Self-Service Password Management**
- Activated Self-Service Password Reset (SSPR) within Microsoft Entra ID to allow users to unblock their accounts without IT intervention[cite: 1].
- Enforced Password Writeback parameters to dynamically sync cloud-initiated password resets back down to the on-premises domain controllers[cite: 1].

**3. Perimeter Identity Hardening**
- Configured tenant security controls to mandate Multi-Factor Authentication (MFA) registration for all synchronized users[cite: 1].
- Implemented verification parameters requiring the Microsoft Authenticator App (TOTP) to secure user sessions against credential exploitation.

---

## Technologies and Services Used

| Component Category | Tool / Service Name | Specific Operational Role |
|---|---|---|
| **Local Identity Store** | Active Directory (AD DS) | Acts as the local source of truth for user accounts[cite: 1]. |
| **Sync Engine** | Azure AD Connect | Coordinates the replication pipeline between local and cloud directories[cite: 1]. |
| **Cloud Control Plane** | Microsoft Entra ID | Manages cloud authentication, access tokens, and security perimeters[cite: 1]. |
| **Credential Security** | Self-Service Password Reset (SSPR) | Allows users to authenticate and change expired or forgotten passwords[cite: 1]. |
| **Sync Feature** | Password Writeback | Writes cloud password updates back to local servers in real time[cite: 1]. |
| **Access Verification** | Multi-Factor Authentication (MFA) | Mandates a second form of identity verification during login[cite: 1]. |

---

## Key Concepts Demonstrated / Business Impact

* **Elimination of Split Identities:** Synchronizing local accounts to the cloud ensures employees maintain a single identity across the organization, preventing credential confusion and poor password hygiene.
* **Help Desk Ticket Reduction:** Automating password updates via SSPR eliminates manual password reset tickets, which historically make up a large portion of internal IT help desk workloads.
* **Secure Hybrid Lifecycle Management:** Enabling Password Writeback guarantees that security configurations and complex password policies remain aligned between cloud and on-premises directories instantly[cite: 1].
* **Mitigation of Credential Theft:** Enforcing mandatory MFA blocks automated brute-force attacks and credential stuffing, protecting enterprise endpoints from unauthorized infiltration.

---

## Note to Self

* **Firewall Configuration:** Do not open inbound ports on the perimeter firewall. Azure AD Connect relies strictly on an outbound web-socket connection over Port 443 to pull change requests down from the cloud.
* **Troubleshooting Steps:** If a cloud password reset fails to sync to local workstations, log into the Azure AD Connect server and audit the Windows Application Event Logs (filter for Source: `DirectorySynchronization`). 
* **APIPA Check:** Remember that if local computers drop off the domain entirely, verify their IP addressing state. A `169.254.x.x` address means they can't see the DHCP server or default gateway network paths.
