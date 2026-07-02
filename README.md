# Enterprise IT Infrastructure & Cybersecurity Portfolio

## 🧑‍💻 Professional Profile
Transitioning 12+ years of client-facing IT experience, SLA ownership, and stakeholder management into hands-on infrastructure and security roles. Technical foundation spans Azure, hybrid environments, networking, IAM, and cybersecurity. Proficient in PowerShell, Python, and ITIL to bridge business priorities with technical execution.

---

## 🛠️ Portfolio Architecture & Mapped Projects
This repository serves as a centralized, production-grade lab environment validating technical competencies across cloud architecture, enterprise networking, systems administration, and security operations. 

*Click on a domain header below to explore the detailed lab guides, configuration scripts, and verification logs for each deployment lifecycle.*

### ☁️ [1. Azure Administration (AZ-104)](./Azure-Administration-AZ104/)
* Deployed a hybrid identity infrastructure by synchronizing on-premises Active Directory (AD DS) with Entra ID using AD Connect, SSPR, and MFA.
* Configured secure virtual network routing and traffic access controls using Azure Firewall, Route Tables, and Network Security Groups (NSGs).
* Established cross-region connectivity by implementing VNET Peering and Site-to-Site VPN connections via Azure Virtual Network Gateways.
* Architected high-availability systems and secure data access by deploying an Azure Load Balancer, Azure Bastion, and Private Endpoints.
* Automated scalable compute environments by configuring Virtual Machine Scale Sets (VMSS), Availability Sets, and Golden Images.
* Implemented business continuity, infrastructure monitoring frameworks using Recovery Services Vaults, Azure Backups, and Network Watcher.

### 🌐 [2. Network Infrastructure (CCNA)](./Network-Infrastructure-CCNA/)
* Configured inter-VLAN routing by establishing 802.1Q trunking links and deploying router subinterfaces using Router-on-a-Stick architecture.
* Implemented network layer security boundaries by developing Standard Access Control Lists (ACLs) to filter traffic patterns between subnets.
* Engineered default gateway redundancy and high availability by implementing HSRP with custom active/standby router priority settings.
* Deployed scalable dynamic routing architectures across multi-router topologies by configuring Single-Area OSPFv2 routing protocols.
* Conducted protocol-level troubleshooting operations using Wireshark to isolate DHCP DORA sequences and analyze network frame structures.

### 🛡️ [3. Security Operations, Identity & Access (SC-200)](./Security-Operations-SC200/)
* Configured Defender preset policies, domain impersonation blocks, and custom KQL hunting queries for malicious executable attachments.
* Executed advanced KQL hunting queries against Microsoft Defender for Endpoint telemetry and email event log databases.
* Engineered network monitoring by routing Firewall diagnostics and App Service logs into Sentinel to build scheduled analytics detection rules.
* Built a log ingestion pipeline by deploying Log Analytics agent on Windows DC and RHEL to stream Security Events and Syslog data into Sentinel.
* Enrolled hybrid servers via Azure Arc, assessed vulnerabilities, and configured Sentinel alerts for failed RDP attempts.

### 🐧 [4. Linux System Administration (RHCSA)](./Linux-System-Administration-RHCSA/)
* Constructed a centralized local network installation server by utilizing Apache (HTTPD) & createrepo to deliver software to offline client nodes.
* Deployed secure web application endpoints with altered file hierarchies while debugging and configuring target SELinux security label contexts.
* Maintained storage by partitioning hardware blocks, modifying live LVM allocations, configuring persistent Stratis storage pools.
* Established hybrid-identity management workflows by executing domain enrollment sequences to bind Linux nodes into Windows AD via realmd.
* Implemented distributed file infrastructure using AutoFS automounting for NFS exports and secure Windows CIFS mounts.

### 📧 [5. M365 Certified Expert (MS-102)](./M365-Administration-MS102/)
* Engineered identity governance frameworks by provisioning Entra ID groups using dynamic membership with RBAC delegated assignments.
* Designed secure messaging ecosystems by building Mail Flow Rules paired with cloud-based anti-phishing and anti-malware threat policies.
* Implemented data governance standards inside Purview by deploying DLP filters configured to capture and remediate corporate financial leaks.
* Configured tenant access by designing conditional, medium and above Sign in Risk Policies to intercept & block compromised authentications.

### 💻 [6. Device Management & Endpoint Engineering (MD-102)](./Device-Management-MD102/)
* Engineered device compliance frameworks by deploying policies that mandate BitLocker encryption, Secure Boot protocols & TPM verification.
* Hardened endpoint by deploying Windows Security Baselines alongside Update Rings to manage patch deferrals and compliance deadlines.
* Automated zero-touch onboarding pipelines using PowerShell to harvest hardware identifiers for Windows Autopilot deployment profiles.
* Packaged and distributed legacy software by utilizing the Microsoft Win32 Content Prep Tool to compile and deploy .intunewin application payloads.
* Deployed a MECM hierarchy featuring a CAS, Primary Site, and ADDS to automate network OS imaging and validate .exe & .msi app deployments.

### 🤖 [7. Linux Automation & Infrastructure as Code (RHCE)](./Linux-Automation-RHCE/)
* Secured credentials by engineering an encrypted Ansible Vault data volume to feed passwords during automated multi-host deployment.
* Engineered content & transfer engines by combining Jinja2 configuration with automated firewall rule changes & SELinux boolean modifications.
* Designed reusable IaC Ansible roles with structured directory layouts, README documentation, variables, and metadata configurations.
* Constructed dual-play system storage automation playbooks to execute live disk partitioning, initialize active swap allocations & build LVM fabrics.

### 🗄️ [8. Database Administration (DP-300)](./Database-Administration-DP300/)
* Deployed Azure SQL infrastructure across operational models including Hyperscale, Serverless, shared Elastic Pool compute architectures.
* Implemented point-in-time database recovery strategies by executing granular Point-in-Time Restores (PITR) using the Azure CLI.
* Enforced data governance and compliance mandates by implementing Dynamic Data Masking for columns with role-based access restrictions.
* Engineered business continuity topologies by configuring SQL Geo-Replication & validating disaster recovery through forced failover testing.

### 🖥️ [9. Virtual Desktop Specialty (AZ-140)](./Virtual-Desktop-AZ140/)
* Deployed and configured Azure ADDS with custom VNET DNS settings and integrated a Windows Server domain management environment.
* Provisioned multi-session pooled AVD host pools utilizing depth-first load balancing, automated domain joins, and workspace application groups.
* Engineered cloud storage architecture by deploying GRS Azure File Shares integrated with Entra ID and custom SMB share-level RBAC assignments.
* Implemented profile virtualization using FSLogix containers across multi session hosts utilizing registry configurations & network SMB path routing.

---

## 🛠️ Technical Skill Summary
* **Cloud & Virtualization:** Microsoft Azure, Microsoft Intune, MECM (SCCM), VMware, Azure Virtual Desktop (AVD), FSLogix
* **Networking & Security:** Cisco IOS, TCP/IP, Inter-VLAN Routing, Access Control Lists (ACLs), HSRP, OSPFv2, Wireshark, Microsoft Sentinel SIEM, Microsoft 365 Defender
* **Operating Systems & Automation:** Red Hat Enterprise Linux (RHEL 8/9), Windows Server, Active Directory (AD DS), Ansible Core, PowerShell scripting, Python, Bash
* **Methodologies & Frameworks:** Agile/Scrum Frameworks (CSM, CSPO principles), ITIL Operational Frameworks, Customer Success Management (CCSM Frameworks)
