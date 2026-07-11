Markdown
# 4. High-Availability Systems & Secure Data Access
## Deep-Dive Component Engineering | AZ-104 Certification Track

---

## Overview
This project focuses on the engineering of highly resilient compute frameworks and secure data access layers that eliminate single points of failure and minimize external attack surfaces. The architecture implements an Azure Load Balancer to distribute client traffic across redundant compute nodes, ensuring high availability during high-demand phases or hardware maintenance. Administrative access is hardened by deploying Azure Bastion as an isolated proxy gateway, while sensitive platform services (PaaS) are secured from external exploitation via Private Endpoints that remove public endpoints entirely.

---

## Architecture

Internet (Public Traffic / Administrators)
│
├── [Administrative Access via Port 443] ──► [ Azure Bastion Proxy ]
│                                                    │
│                                                    ▼ [Private SSH/RDP]
└── [Standard User Web Access]                       │
│                                         │
▼                                         │
┌───────────────────────────────────────────────────────┼─────┐
│                 Spoke VNet Boundary                   │     │
│                                                       │     │
│   ┌───────────────────────────────────────────────┐   │     │
│   │  Azure Load Balancer (Public Interface)       │   │     │
│   └───────────────────────┬───────────────────────┘   │     │
│                           │                           │     │
│                           ▼ [Distributed Traffic]     │     │
│   ┌───────────────────────────────────────────────┐   │     │
│   │  Backend Compute Subnet                       │   │     │
│   │                                               │   │     │
│   │   ┌───────────────────┐   ┌───────────────────┐   │     │
│   │   │  Virtual Machine  │   │  Virtual Machine  │◄──┘     │
│   │   │      Node 01      │   │      Node 02      │         │
│   │   └─────────┬─────────┘   └─────────┬─────────┘         │
│   └─────────────┼───────────────────────┼───────────────────┘
│                       │
└───────────┬───────────┘
│
▼ [Internal VNet Routing]
┌───────────────────────────────────────────────────────┐
│  Data Storage Subnet Boundary                         │
│                                                       │
│   ┌───────────────────┐   ┌───────────────────┐       │
│   │ Private Endpoint  │──►│ Azure Storage     │       │
│   │ (Private IP Map)  │   │ (Blob Container)  │       │
│   └───────────────────┘   └───────────────────┘       │
└───────────────────────────────────────────────────────┘


---

## What Was Built

**1. Layer 4 Public Load Balancer Distribution**
- Provisioned a Standard SKU Azure Load Balancer to act as a highly available front-end traffic ingress point.
- Created a Backend Pool grouping redundant virtual machine nodes to distribute workload weight.
- Configured custom **Health Probes** targeting TCP Port 80 to continuously check application responsiveness, forcing the load balancer to automatically stop routing traffic to any unresponsive backend node within 10 seconds.
- Implemented load-balancing rules to map inbound front-end traffic streams to the healthy backend pool instances.

**2. Zero-Public Endpoint Management (Azure Bastion)**
- Provisioned Azure Bastion inside a dedicated subnet partition to manage secure administrative access.
- Removed public IP address boundaries from all backend workload virtual machines, restricting their connection parameters strictly to private internal IP addresses.
- Established secure administrative proxy gateways allowing RDP/SSH sessions to run over encrypted TLS Port 443 directly within the web portal browser shell.

**3. PaaS Network Inversion (Private Endpoints)**
- Deployed a **Private Endpoint** linked straight to an Azure Storage account blob container.
- Disabled the default public network access path on the target storage account firewall settings.
- Mapped a private IP address directly from the internal subnet architecture to the storage resource, routing backend application data requests across secure private networks.
- Configured an Azure **Private DNS Zone** (`privatelink.blob.core.windows.net`) to ensure internal resource name resolution cleanly routes traffic to the private endpoint interface.

---

## Technologies and Services Used

| Component Category | Tool / Service Name | Specific Operational Role |
|---|---|---|
| **Traffic Distribution**| Azure Load Balancer | Evaluates health checks and balances Layer 4 traffic across backend targets. |
| **Secure Management** | Azure Bastion | Proxies secure administrative RDP and SSH terminals inside a TLS browser stream. |
| **Private Data Ingress**| Private Endpoints | Assigns a private network interface IP map to public cloud platform services. |
| **Data Repository** | Azure Storage Account | Serves as the back-end file/object storage repository for application data. |
| **Name Resolution** | Private DNS Zones | Overrides public DNS records to resolve platform services to internal IP maps. |

---

## Key Concepts Demonstrated / Business Impact

* **High-Availability Fault Inversion:** Utilizing health probes alongside a standard load balancer ensures that if an individual virtual machine node crashes or undergoes maintenance, traffic is rerouted instantly, preventing costly business application downtime.
* **Reduction of Perimeter Attack Surface:** Eliminating public IP addresses from virtual machines neutralizes automated brute-force scripts and remote port scanners, protecting management boundaries.
* **Data Exfiltration Mitigation via PaaS Isolation:** Private Endpoints isolate cloud storage accounts from public internet data routes. Even if credentials are leaked, data access is blocked from outside the company's private network boundary.
* **Preservation of Resource Performance:** Standard SKU load balancers run with sub-millisecond switching speeds, optimizing user response times while scaling workload distributions across elastic target pools.

---

## Note to Self

* **Bastion Subnet Constraints:** Azure Bastion requires a dedicated subnet named exactly **`AzureBastionSubnet`**. It must be provisioned with a minimum network mask of `/26` or larger, and it cannot host any other enterprise workloads or custom gateways.
* **Load Balancer SKU Cohesion:** Remember that Azure Load Balancer SKUs must match your compute assets. If you choose a Standard SKU Load Balancer, all virtual machines added to the backend pool **must** utilize Standard SKU public IPs (if public IPs are assigned) or have no public IPs, and they must reside within an Availability Zone or Availability Set.
* **Private DNS Zone Ingestion:** When implementing Private Endpoints, if application connection strings start throwing name resolution faults, check the Private DNS Zone virtual network links. The DNS zone must be explicitly linked to the target workload VNet to correctly resolve the resource name to its private IP map.
