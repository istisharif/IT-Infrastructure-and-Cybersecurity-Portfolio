# RHCSA: Red Hat Enterprise Linux (RHEL) System Administration Lab Documentation

## 🏗️ Enterprise Linux Infrastructure Overview
This deployment validates core competencies in Red Hat Enterprise Linux (RHEL 8/9) systems engineering, kernel-level Mandatory Access Control (MAC) configuration, enterprise logical storage frameworks, distributed file structures, and cross-platform Active Directory identity integration.

---

## 🚀 Lab Configuration Stages & Verification

### 1. Centralized DNF/YUM Repository Server
* **Implementation:** Constructed an isolated local network installation and software mirror server using the Apache (HTTPD) web server. 
* **Package Management:** Utilized the `createrepo` utility to build custom runtime metadata structures, allowing completely offline client nodes to securely download and install verified application packages across the LAN.

### 2. Secure Web App Deployment & SELinux Hardening
* **Implementation:** Deployed secure web application endpoints featuring altered, non-standard file hierarchies.
* **Kernel-Level Hardening:** Maintained a strict security posture by debugging system access logs and manually re-labeling target SELinux (Security-Enhanced Linux) contexts using `semanage` and `restorecon` to enforce Mandatory Access Control boundaries without disabling enforcing mode.

### 3. Enterprise Storage Management & LVM Fabrics
* **Implementation:** Partitioned physical hardware disk blocks using standard utilities. Engineered highly flexible local file architectures by building and expanding live Logical Volume Management (LVM) allocations to scale storage volumes dynamically without service interruption.
* **Modern Pools:** Initialized persistent, structured Stratis storage pools configured with thin provisioning and integrated snapshot recovery capabilities.

### 4. Hybrid Identity Workflows & Active Directory Integration
* **Implementation:** Established a unified enterprise identity baseline across diverse platform architectures. 
* **Domain Binding:** Executed automated system enrollment sequences to securely bind and authenticate Linux client nodes directly into a Windows Active Directory Domain Services (AD DS) ecosystem utilizing the `realmd` network service discovery manager.

### 5. Distributed File Systems & Automated Storage Mounts
* **Implementation:** Implemented an enterprise distributed file sharing environment. Configured the `AutoFS` system daemon to enable dynamic, on-demand automounting of remote Network File System (NFS) exports.
* **Cross-Platform Access:** Built secure, credential-mapped Windows Common Internet File System (CIFS) mounts to seamlessly share file data assets across Linux and Windows server kernels.

---

## 🛠️ Core Linux Technologies & Engineering Toolsets
* **System Automation & Services:** Apache Web Server (`httpd`), Repository Engines (`createrepo`, `dnf`), Systemd Core Services
* **Kernel Security (MAC):** SELinux Enforcing Architectures, Context Customization (`semanage fcontext`, `restorecon`)
* **Storage Systems:** Logical Volume Management (LVM), Thin Provisioning, Stratis File Management Pools
* **Identity Interoperability:** Active Directory Integration, SSSD Core Authentication Services, `realmd` Client Enrolment
* **Network Storage:** AutoFS Automounting, Network File System (NFS), Windows Common Internet File System (CIFS/SMB)
