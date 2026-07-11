Markdown
# 2. Secure Virtual Network Routing & Traffic Controls
## Deep-Dive Component Engineering | AZ-104 Certification Track

---

## Overview
This project establishes a perimeter-hardened network environment inside Azure by grouping virtual resources into a secured virtual network (VNet) topology. Instead of allowing virtual servers to connect directly to the public internet—which leaves them vulnerable to scanning and exploitation—this architecture forces all inbound and outbound traffic through a centralized, stateful inspection checkpoint (Azure Firewall). Traffic paths are precisely controlled using custom routing maps, while localized security rules filter traffic boundaries between independent application tiers.

---

## Architecture

Internet (Public Users / Admins)
│
▼ [Traffic Hits Public IP Endpoint]
┌─────────────────────────────────────────────────────────────┐
│                 Central Hub VNet Boundary                   │
│                                                             │
│   ┌─────────────────────────────────────────────────────┐   │
│   │             Azure Firewall (Stateful Engine)        │   │
│   │  - DNAT Rules: Intercepts inbound HTTP/RDP traffic  │   │
│   │  - Network Rules: Restricts protocols & DNS paths   │   │
│   │  - App Rules: Evaluates FQDN strings (eg. Blocks URL)│   │
│   └───────────────────────────┬─────────────────────────┘   │
└───────────────────────────────┼─────────────────────────────┘
│
│ [Custom Route Table (UDR): 0.0.0.0/0]
▼ [Forces traffic to hop to Firewall IP]
┌─────────────────────────────────────────────────────────────┐
│               Workload Spoke VNet Boundary                  │
│                                                             │
│  ┌───────────────────────────────────────────────────────┐  │
│  │ Application Subnet                                    │  │
│  │                                                       │  │
│  │   ┌───────────────────────┐   ┌───────────────────┐   │  │
│  │   │ Virtual Machine Node  │   │ Network Security  │   │  │
│  │   │ (Private IP Address)  │◄──┤ Group (NSG) ACL   │   │  │
│  │   └───────────────────────┘   └───────────────────┘   │  │
│  └───────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘


---

## What Was Built

**1. Centralized Perimeter Firewall Deployment**
- Deployed a stateful Azure Firewall inside a dedicated gateway network partition (`AzureFirewallSubnet`).
- Configured Destination Network Address Translation (DNAT) rules to map inbound public requests safely down to private, backend computing assets without exposing the machines directly to the internet.
- Enforced Application Rules using Fully Qualified Domain Names (FQDNs) to track and restrict web-browsing pathways originating from internal development nodes.

**2. Custom Traffic Path Interception (User-Defined Routes)**
- Constructed a custom Azure Route Table to override default systemic system routing logic.
- Implemented a User-Defined Route (UDR) targeting an address prefix of `0.0.0.0/0` (all internet-bound data), designating the private interface of the Azure Firewall as the next hop.
- Bound the custom route table directly to production workload subnets to ensure strict forced tunneling compliance.

**3. Layer 4 Subnet Isolation**
- Provisioned Network Security Groups (NSGs) to act as secondary packet-filtering firewalls at the subnet boundary.
- Configured inbound and outbound access control lists (ACLs) to enforce strict isolation rules, preventing unauthorized cross-talk between separate application tiers.

---

## Technologies and Services Used

| Component Category | Tool / Service Name | Specific Operational Role |
|---|---|---|
| **Network Core** | Virtual Network (VNet) | Establishes the isolated logical private network space. |
| **Stateful Inspection** | Azure Firewall | Enforces centralized inbound DNAT, network rules, and application URL filters. |
| **Path Manipulation** | Route Tables (UDR) | Overrides system paths to force traffic through security inspection points. |
| **Packet Filtering** | Network Security Groups (NSG) | Manages Layer 3 and Layer 4 access controls at the localized subnet level. |
| **Compute Node** | Virtual Machine (VM) | Hosts private application workloads inside the secure network core. |

---

## Key Concepts Demonstrated / Business Impact

* **Azure Firewall vs. NSG Defense-in-Depth:** Differentiating between localized Layer 4 packet filters (NSGs) and centralized Layer 7 application-aware engines (Azure Firewall) provides a multi-tiered defense posture that stops advanced threat vectors.
* **Mitigation of Data Exfiltration:** Using Route Tables to force all outbound traffic through the firewall ensures that compromised machines cannot dynamically upload stolen company data to unauthorized external storage servers or command-and-control websites.
* **Elimination of Public Footprints via DNAT:** Inbound access requests are terminated at the firewall's public interface, which forwards traffic using internal private IPs. This completely hides production server identities from malicious port scans.
* **FQDN URL Filtering Control:** Standard firewalls can block explicit IP numbers, but modern cloud apps shift across thousands of dynamic IP ranges daily. Using FQDN filtering ensures access blocks are consistently applied based on web address names rather than brittle IP lookups.

---

## Note to Self

* **Subnet Requirements:** Remember that Azure Firewall mandates a dedicated subnet named exactly `AzureFirewallSubnet` with at least a `/26` prefix. If you deploy a hybrid backup firewall configuration, a secondary subnet named `AzureFirewallManagementSubnet` is also required.
* **Routing Validation:** If traffic appears stuck or fails to exit the virtual network, navigate to the target Virtual Machine's Network Interface card (NIC) in the portal and select **Effective Routes**. Verify that the `0.0.0.0/0` line explicitly points to your Firewall IP as the next hop rather than the default System route.
* **Rule Processing Order:** Azure Firewall evaluates rules deterministically: **DNAT rules are processed first**, followed by Network rules, and finally Application rules. If a packet matches a network rule block, it will be handled before application-layer filtering is even evaluated.
