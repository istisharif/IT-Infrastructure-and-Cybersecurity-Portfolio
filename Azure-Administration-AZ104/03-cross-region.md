Markdown
# 3. Cross-Region Connectivity
## Deep-Dive Component Engineering | AZ-104 Certification Track

---

## Overview
This project establishes high-speed, secure communication channels across separate geographic boundaries and hybrid cloud environments. It implements a multi-region cloud backbone using VNet Peering to link disparate virtual networks with sub-millisecond latency. To extend this architecture back to physical corporate infrastructure, a secure hybrid network pipeline is established using Azure Virtual Network Gateways to manage an encrypted Site-to-Site VPN connection over the public internet, ensuring secure cross-premises data mobility.

---

## Architecture

┌───────────────────────────────────────┐         ┌───────────────────────────────────────┐
│       Primary Azure Region VNet       │         │      Secondary Azure Region VNet      │
│          (e.g., East US)              │         │            (e.g., West US)            │
│     Subnet range: 10.1.0.0/16         │         │       Subnet range: 10.2.0.0/16       │
│                                       │         │                                       │
│   ┌───────────────────────────────┐   │         │   ┌───────────────────────────────┐   │
│   │     Production App Subnet     │   │         │   │     Disaster Recovery Subnet  │   │
│   └───────────────┬───────────────┘   │         │   └───────────────┬───────────────┘   │
│                   │                   │         │                   │                   │
│         [ GatewaySubnet ]             │         │                   │                   │
│     (Virtual Network Gateway)         │         │                   │                   │
└───────────────────▲───────────────────┘         └───────────────────▼───────────────────┘
│                                                 ▲
│                                                 │
│ [Site-to-Site VPN]                              │ [Global VNet Peering]
│ Encrypted IPsec Tunnel over Internet            │ High-Speed Private Backbone
│                                                 │
▼                                                 │
┌───────────────────────────────────────┐                             │
│     On-Premises Corporate Network     │                             │
│       Subnet range: 192.168.1.0/24    │                             │
│                                       │                             │
│   ┌───────────────────────────────┐   │                             │
│   │ Local Gateway / VPN Edge Appliance│◄─────────────────────────────┘
│   └───────────────────────────────┘   │
└───────────────────────────────────────┘


---

## What Was Built

**1. Multi-Region Network Interconnection (Global VNet Peering)**
- Configured bi-directional VNet Peering connections between the primary and secondary regional virtual networks.
- Enabled explicit virtual network access parameters (`Allow forwarded traffic` and `Allow virtual network access`) to enable seamless inter-region communication.
- Verified low-latency, high-bandwidth data transfers traveling entirely across Microsoft’s private fiber-optic global backbone network without exposing data to the public internet.

**2. Hybrid Gateway Infrastructure Provisioning**
- Deployed a dedicated, highly available **Virtual Network Gateway (VpnGw1)** inside a specialized gateway network partition (`GatewaySubnet`).
- Constructed an Azure **Local Network Gateway** resource to register the public IP architecture and local IPv4 address prefixes (`192.168.1.0/24`) of the on-premises corporate office.

**3. Encrypted Site-to-Site VPN Tunnel Establishment**
- Created an Azure Connection resource to bind the Virtual Network Gateway to the Local Network Gateway.
- Configured a secure **Site-to-Site (S2S) VPN tunnel** using Internet Protocol Security (IPsec) and Internet Key Exchange (IKEv2) encapsulation parameters.
- Generated and mapped a complex cryptographically random Pre-Shared Key (PSK) across both the Azure gateway engine and the local router edge endpoint to authenticate the encrypted connection.

---

## Technologies and Services Used

| Component Category | Tool / Service Name | Specific Operational Role |
|---|---|---|
| **Backbone Routing** | VNet Peering | Links multiple regional VNets directly together over the private Microsoft backbone. |
| **Cloud VPN Endpoint** | Virtual Network Gateway | Manages the encryption, decryption, and routing of cross-premises tunnels. |
| **On-Premises Mapping**| Local Network Gateway | Defines the public IP and address ranges of the physical remote data center. |
| **Tunnel Configuration**| Connection Resource | Enforces the IPsec/IKE policy parameters and holds the pre-shared key. |
| **Network Core** | GatewaySubnet | Dedicated subnet infrastructure block required to host Azure gateway resources. |

---

## Key Concepts Demonstrated / Business Impact

* **Peering vs. VPN Gateway Optimization:** Utilizing VNet Peering for cloud-to-cloud connections avoids the cost and compute limitations of a VPN gateway, leveraging Microsoft's global backbone for fast inter-region data transfers.
* **Cost-Effective Hybrid Connectivity:** Implementing an IPsec Site-to-Site VPN provides a secure, encrypted hybrid connection to local corporate networks over standard public internet paths, avoiding the higher upfront costs of dedicated private circuits like ExpressRoute.
* **Disaster Recovery Network Alignment:** Linking multiple regions together via Global VNet Peering allows companies to replicate database engines and application configurations asynchronously, preparing the infrastructure for multi-region failovers.
* **Secure Cross-Premises Mobility:** Encrypted encapsulation protocols ensure that local files and enterprise configurations can migrate to cloud assets without exposure to sniffing or man-in-the-middle attacks on the internet.

---

## Note to Self

* **Address Space Rule:** Virtual Networks cannot be peered if their configured IP address spaces overlap. Always coordinate enterprise IP tracking (IPAM) beforehand to prevent subnet overlap errors (e.g., trying to peer two networks that both use `10.0.0.0/16`).
* **Gateway Subnet Constraints:** The `GatewaySubnet` must be named exactly that, and it should be provisioned with a minimum network size of `/27` or `/26` to allow room for future scaling. **Never** attach Network Security Groups (NSGs) or User-Defined Routes (UDRs) to the GatewaySubnet; doing so will disrupt gateway management control signals.
* **Gateway Transit Parameters:** If a spoke VNet needs to utilize a gateway hosted inside a central Hub VNet to talk back to the local office, you must check **`Use the remote virtual network's gateway`** on the spoke peering profile, and **`Use this virtual network's gateway`** on the hub peering profile.
