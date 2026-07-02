# CCNA: Network Infrastructure Lab Documentation

## 🏗️ Enterprise Network Topology Overview
This deployment models a high-availability corporate LAN/WAN topology validating routing architectures, switching fabrics, protocol analysis, and per-subnet perimeter security boundaries using Cisco IOS standards.

---

## 🚀 Lab Configuration Stages & Verification

### 1. Inter-VLAN Routing & Logical Segmentation
* **Implementation:** Segmented broadcast domains by provisioning custom enterprise Virtual Local Area Networks (VLANs) across switching matrices.
* **Routing Architecture:** Engineered inter-VLAN communications by establishing IEEE 802.1Q trunking encapsulation across uplink interfaces and mapping individual router subinterfaces via a Router-on-a-Stick (RoAS) framework.

### 2. Network Layer Security Boundaries
* **Implementation:** Hardened network traffic vectors by developing and applying Standard Access Control Lists (ACLs) to strategic interface inbound/outbound paths.
* **Traffic Control:** Enforced security boundaries by explicitly filtering and restricting cross-subnet traffic patterns, preventing unauthorized end-user nodes from accessing restricted management segments.

### 3. Default Gateway Redundancy & High Availability
* **Implementation:** Implemented the Hot Standby Router Protocol (HSRP) to safeguard against single points of physical layer gateway failures.
* **Priority Metrics:** Configured custom active/standby device priority weight thresholds paired with automated interface tracking to guarantee zero-downtime default gateway failovers.

### 4. Scalable Dynamic Routing Topologies
* **Implementation:** Scaled the routing core across multi-router backbones by deploying the Single-Area OSPFv2 link-state routing protocol.
* **Optimization:** Fine-tuned loop prevention and convergence times by modifying default OSPF hello/dead intervals, setting specific router IDs, and managing wildcards to minimize routing table overhead.

### 5. Protocol-Level Traffic Troubleshooting
* **Implementation:** Intercepted and decoded live system traffic flows using packet analyzer utilities.
* **Frame Analysis:** Diagnosed and verified stateful address allocations by deep-diving into individual Wireshark traces, isolating the step-by-step DHCP DORA sequence (Discover, Offer, Request, Acknowledge) and evaluating Layer 2/Layer 3 frame metadata headers.

---

## 🛠️ Protocols & Core Technologies Verified
* **Switching & Layer 2:** 802.1Q Encapsulation, Trunking Links, Virtual Local Area Networks (VLANs), Broadcast Domain Isolation
* **Routing & Layer 3:** Single-Area OSPFv2, Router-on-a-Stick (RoAS), Router Subinterfaces, Static Routes
* **High Availability & Security:** Hot Standby Router Protocol (HSRP), Standard Access Control Lists (ACLs), Subnet Filtering Boundaries
* **Diagnostics & Analysis:** Wireshark Packet Captures, DHCP DORA Decoding, Protocol Frame Header Inspections
