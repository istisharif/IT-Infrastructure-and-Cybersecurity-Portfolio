# AZ-104: Microsoft Azure Administrator Lab Documentation

## 🏗️ Hybrid Cloud Architecture Overview
This deployment validates core competencies in enterprise cloud architecture, hybrid identity synchronization, secure network topology management, and high-availability system orchestration inside Microsoft Azure.

---

## 🚀 Lab Deployment Stages & Verification

### [1. Hybrid Identity Infrastructure](./01-hybrid-identity.md)
* **Implementation:** Configured and deployed an on-premises Active Directory Domain Services (AD DS) simulation environment and synchronized objects to cloud-native Entra ID using Azure AD Connect.
* **Security Controls:** Enforced Multi-Factor Authentication (MFA) registration requirements and enabled Self-Service Password Reset (SSPR) writeback capabilities.
* **Verification Token:** Managed user state sync status verified via the Microsoft Entra Admin Center synchronization health dashboard.

### [2. Secure Virtual Network Routing & Traffic Controls](./02-secure-routing.md)
* **Implementation:** Provisioned isolated Virtual Networks (VNets) paired with granular network layer separation. Route tables were explicitly mapped to bypass default routing hops.
* **Traffic Control:** Configured an Azure Firewall instance alongside strict Network Security Groups (NSGs) to enforce ingress/egress stateful filtering patterns.
* **Security Rules:** Blocked all direct public RDP/SSH exposure, limiting management paths exclusively through private, encrypted gateways.

### [3. Cross-Region Connectivity](./03-cross-region.md)
* **Implementation:** Interconnected distinct geographic cloud locations by provisioning high-speed VNet Peering links. 
* **Hybrid Tunneling:** Implemented a secure Site-to-Site VPN tunnel utilizing Azure Virtual Network Gateways to connect remote local office endpoints to central cloud assets.

### [4. High-Availability Systems & Secure Data Access](./04-high-availability.md)
* **Implementation:** Deployed an Azure Load Balancer to distribute incoming application traffic across redundant computational backends. 
* **Secure Access:** Configured an Azure Bastion host to allow secure TLS-based browser management of virtual machines without public IP addresses. Implemented Private Endpoints to isolate critical database storage accounts behind private cloud network addresses.

### [5. Automated Scale-Out Compute Environments](./05-compute-elasticity.md)
* **Implementation:** Engineered automated compute capacity tiers by deploying Virtual Machine Scale Sets (VMSS) tied to dynamic CPU utilization thresholds.
* **Image Management:** Utilized generalized Golden Images inside Availability Sets to prevent single points of hardware failure.

### [6. Business Continuity & Platform Monitoring Frameworks](./06-monitoring-backup.md)
* **Implementation:** Established a centralized Recovery Services Vault mapping automated Azure Backups to virtual assets.
* **Diagnostics:** Deployed Network Watcher to run automated packet captures and connection troubleshooting checks to verify systemic network path health.

---

## 🛠️ Infrastructure Components Validated
* **Compute:** Virtual Machine Scale Sets (VMSS), Availability Sets, Custom Golden Images
* **Networking:** Azure Firewall, Route Tables, Network Security Groups (NSGs), VNet Peering, Virtual Network Gateways (Site-to-Site VPN)
* **Identity & Management:** Entra ID, Azure AD Connect, SSPR, Azure Bastion, Private Endpoints, Azure Load Balancer
* **Governance & Monitoring:** Recovery Services Vault, Azure Backups, Network Watcher
