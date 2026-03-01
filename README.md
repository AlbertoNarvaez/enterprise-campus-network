# Enterprise Campus Network Architecture – v1.0
**OSPF Ring Backbone · ASA Perimeter · DMZ · Azure VPN (Simulated)**

---

## Project Overview

This project models the design and implementation of a segmented enterprise campus network architecture including:

- Internet connectivity through an ISP router  
- Perimeter firewall (Cisco ASA)  
- Redundant OSPF backbone (Routers A, B and C in ring topology)  
- Hierarchical distribution layer  
- Department-based VLAN segmentation  
- Dedicated DMZ for public services (WEB / DNS)  
- Logical Azure cloud integration (Site-to-Site model)

The architecture was initially designed conceptually using Draw.io following enterprise design principles and later implemented in Cisco Packet Tracer.

Due to simulator limitations, certain physical adaptations were required.  
These changes affect only interface distribution — the logical design, routing model, and security segmentation remain consistent with enterprise standards.

---

## Architectural Intent

The conceptual design follows a classical hierarchical enterprise model:

- **Core Layer** – Transit backbone and OSPF Area 0 routing
- **Distribution Layer** – Inter-VLAN routing and segmentation
- **Access Layer** – Endpoint connectivity
- **Perimeter Security** – ASA firewall separating Outside / Inside / DMZ
- **Cloud Integration** – Azure network connected through a Site-to-Site VPN model

The backbone is implemented as a ring topology (Routers A, B and C) running OSPF Area 0 to provide redundancy and dynamic convergence.

---

## Packet Tracer Constraints & Technical Adaptations

### ASA 5505 Limitations

The ASA model available in Packet Tracer:

- Supports limited active `nameif` interfaces  
- Restricts VLAN capabilities  
- Does not fully support IPsec VPN simulation  

**Adaptation:**  
The DMZ was implemented at the distribution layer using a dedicated VLAN while preserving logical isolation and security separation.

---

### Router 2911 Interface Density

The conceptual design required four routed interfaces at the core level.

Packet Tracer’s 2911:

- Provides only three routed Gigabit interfaces  
- HWIC modules operate strictly as Layer 2  
- No SVI creation supported in router IOS  

**Adaptation:**  
Physical link distribution was rearranged while maintaining:

- OSPF Area 0 backbone  
- Redundant ring topology  
- Full route propagation  
- Network convergence behavior  

The logical architecture remains unchanged.

---

### Inter-VLAN Routing Implementation

Because the router HWIC module does not support SVIs:

- Inter-VLAN routing was implemented on Catalyst 3560 switches  
- `ip routing` and `interface vlan X` were used at the distribution layer  

This aligns with real-world hierarchical enterprise design principles.

---

## Cloud Integration – Azure (Simulated)

The design includes logical Azure integration:

- Azure Network: `172.16.100.0/24`
- Intended architecture: Site-to-Site IPsec VPN tunnel

Packet Tracer does not support full IPsec implementation on ASA.

**Simulation Approach:**

Azure connectivity is modeled using static routing through the ISP router to emulate tunnel behavior and preserve routing logic.

This maintains:

- Logical separation  
- Cloud routing intent  
- Future scalability  
- Architectural consistency  

---

## Security Model

The network is divided into three primary domains:

- **Outside** – Internet connectivity  
- **Inside** – Corporate LAN segmented by VLAN  
- **DMZ** – Public-facing services (WEB / DNS)  

### Intended Traffic Flows

- Internal VLANs → Internet via ASA  
- Internet → DMZ services  
- Controlled inter-department routing  
- OSPF backbone traffic within Area 0  

Advanced ACL policies and inspection mechanisms are planned for further hardening.

---

## Validation & Testing

The implementation has been validated through:

- Successful OSPF adjacency formation  
- Correct route propagation across the backbone  
- Verified inter-VLAN routing  
- End-to-end connectivity between departments  
- DMZ isolation confirmation  
- Simulated Azure reachability  

Routing tables and adjacency states were verified during testing.

---

## Technical Summary

This project demonstrates:

- Enterprise-level network segmentation  
- Hierarchical architecture implementation  
- OSPF backbone design  
- Perimeter firewall integration  
- DMZ isolation  
- Cloud connectivity modeling  
- Adaptation to platform constraints  

In a production environment, the original conceptual design would leverage:

- Higher interface-density routers  
- Advanced firewall licensing  
- Full IPsec VPN configuration  
- Enterprise-grade switching platforms  

The logical architecture is scalable, resilient, and aligned with industry best practices.

---

## Roadmap

This project represents the first stable architectural version.

Next evolution phase will focus on:

- Granular traffic control through extended ACL design
- NAT policies and service publication on ASA
- Layer 2 security hardening (Port-Security, BPDU Guard)
- Default route redistribution strategy in OSPF
- Infrastructure services integration (DHCP, NTP, Syslog)

The objective is to progressively evolve this lab toward a more production-like enterprise environment.

---

## Configuration Files

All device configurations are available in the `/configs` directory.

Validation outputs are provided in `/validation` to demonstrate routing, segmentation and OSPF adjacency status.

---

## License

This project is licensed under the MIT License – see the LICENSE file for details.



