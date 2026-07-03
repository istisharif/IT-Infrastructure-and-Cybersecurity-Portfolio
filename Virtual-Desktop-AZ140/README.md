# AZ-140: Configuring and Operating Microsoft Azure Virtual Desktop Lab Documentation

## 🏗️ Enterprise Virtual Desktop Infrastructure Overview
This deployment validates advanced engineering competencies in cloud-based Virtual Desktop Infrastructure (VDI), managed directory infrastructure integrations, highly resilient network storage engineering, and seamless user profile virtualization using FSLogix systems.

---

## 🚀 Lab Configuration Stages & Verification

### 1. Dedicated Cloud Domain Interoperability
* **Implementation:** Deployed and configured a managed directory environment using Microsoft Entra Domain Services (Entra AD DS). 
* **Network Integration:** Provisioned custom Domain Name System (DNS) properties inside central virtual network settings to establish seamless, low-latency name resolution between virtual assets and the cloud identity forest.

### 2. Multi-Session Pooled Desktop Orchestration
* **Implementation:** Provisioned high-capacity, multi-session pooled Azure Virtual Desktop (AVD) host pools designed to optimize resource compute footprints.
* **Optimization Control:** Enforced a **depth-first load balancing** methodology to saturate active compute nodes sequentially, maximizing efficiency. Automated domain enrollment parameters to seamlessly join host instances to the identity forest while mapping custom workspace application groups to isolate software distribution streams.

### 3. Encrypted Profile Storage Architectures
* **Implementation:** Engineered a resilient storage subsystem using Geo-Redundant Storage (GRS) Azure File Shares to prevent data loss across regional outages.
* **Access Hardening:** Integrated storage clusters into the Entra ID identity perimeter, enforcing strict Server Message Block (SMB) share-level and NTFS file system security permissions using Role-Based Access Control (RBAC).

### 4. Dynamic Profile Virtualization via FSLogix Containers
* **Implementation:** Implemented cross-session user state preservation by deploying an enterprise **FSLogix Profile Container** framework across multi-session computing nodes.
* **Storage Interception:** Engineered system registry configurations and custom network SMB paths to dynamically route and isolate user profile write vectors directly into dedicated remote file shares, enabling instant logon speeds and decoupled session states.

---

## 🛠️ VDI Architecture & Platform Toolsets Verified
* **VDI Infrastructure:** Azure Virtual Desktop (AVD), Multi-Session Host Pools, Workspace Application Groups, Depth-First Load Balancing Logic
* **Identity & Core Networking:** Microsoft Entra Domain Services (Entra AD DS), Custom VNet DNS Scopes, AD Join Automation
* **Virtual Storage Matrices:** Geo-Redundant Storage (GRS), Azure File Shares, Share-Level RBAC Permissions, NTFS ACL Inheritances
* **Profile Virtualization Engineering:** FSLogix Container Software, Registry Policy Deployments, Dynamic VHDX Stream Allocations
