# Business Center Network (Cisco Packet Tracer)

This repository documents a Cisco Packet Tracer network project for a business center with two geographically separated branches:

- **Main office:** Almaty
- **Branch office:** Taldykorgan

Each branch has a five-level structure (four office floors + one basement). Every floor is segmented into its own VLAN to improve performance, simplify management, and enforce traffic isolation between tenant companies.

## Project Scope

The topology is designed to simulate a realistic enterprise environment with:

- Floor-based VLAN segmentation in both branches
- Redundant switched paths with rapid failover
- Dynamic routing between core network segments
- Secure site-to-site tunneling
- Centralized address assignment and shared internal services
- Access control and edge translation for traffic policy enforcement

## Topology Model

The original Packet Tracer project is built as a dual-view model:

- **Physical view:** regional map navigation (Kazakhstan) and branch drill-down
- **Logical view:** working L2/L3 links, protocols, addressing, and policies

This structure makes the lab easier to understand for both presentation and troubleshooting.

## Implemented Technologies

The following technologies are included in the topology:

- VLAN + Inter-VLAN Routing (SVIs on Layer 3 switching)
- DHCP (central server)
- FTP
- RSTP (Rapid Spanning Tree Protocol)
- LACP (EtherChannel)
- OSPF
- GRE over IPsec
- SSH
- NAT
- MPLS (included in design scope)
- ACL
- PPP (CHAP/PAP demonstration)
- AAA (access control and accounting concept)

## VLAN and IP Segmentation

Floor-to-VLAN mapping is consistent between sites (VLAN IDs 10/20/30/40/50), with separate addressing per branch.

### Main Office (Almaty)

| Floor | VLAN ID | Name | Subnet |
|---|---:|---|---|
| 1st Floor | 10 | Floor1 | 10.10.10.0/14 |
| 2nd Floor | 20 | Floor2 | 10.10.20.0/14 |
| 3rd Floor | 30 | Floor3 | 10.10.30.0/14 |
| 4th Floor | 40 | Floor4 | 10.10.40.0/14 |
| Basement | 50 | VLAN50 | 10.10.50.0/14 |

### Branch Office (Taldykorgan)

| Floor | VLAN ID | Name | Subnet |
|---|---:|---|---|
| 1st Floor | 10 | Floor1 | 10.20.10.0/14 |
| 2nd Floor | 20 | Floor2 | 10.20.20.0/14 |
| 3rd Floor | 30 | Floor3 | 10.20.30.0/14 |
| 4th Floor | 40 | Floor4 | 10.20.40.0/14 |
| Basement | 50 | VLAN50 | 10.20.50.0/14 |

## Routing and Switching Design

### Inter-VLAN Routing

Layer 3 switching with SVI interfaces is used to route traffic between floor VLANs while preserving VLAN isolation at Layer 2.

### RSTP

RSTP is enabled across switching layers to:

- prevent loops in redundant topologies
- provide faster convergence during link failures
- increase overall resilience of access/distribution connectivity

### LACP (EtherChannel)

LACP is used between distribution and core layers to bundle links, increase throughput, and add physical link redundancy.

### OSPF

OSPF runs over dedicated routing address space (`192.168.x.x/24`) instead of user VLAN ranges (`10.x.x.x`) to separate control-plane traffic from end-user data networks.

## Core Services

### DHCP

A central DHCP server provides dynamic IP assignment with per-VLAN pools.

### FTP

An internal FTP server supports file sharing between floors/tenants.

- Service IP (documented): `10.10.50.3`
- Protocol/port: FTP (`21`)

### SSH

SSH is part of the management-security scope to provide secure remote administration.

### AAA

AAA (Authentication, Authorization, Accounting) is included to represent centralized administrative access control and user action tracking on network devices.

## WAN, Security, and Edge Controls

### GRE over IPsec

The topology combines:

- **GRE** for routed tunnel flexibility and protocol encapsulation
- **IPsec** for encryption and integrity over untrusted transport

This supports secure inter-site communication while keeping routing practical over the tunnel.

### ACL

ACLs are used to allow/deny traffic by policy based on source/destination and protocol/port criteria.

### NAT

NAT is included for address translation between private internal networks and external-facing connectivity domains.

### PPP Authentication Demo

PPP is configured on a serial router-to-router link to demonstrate authentication models:

- **R1:** CHAP (stronger challenge/response model)
- **R2:** PAP (simple username/password exchange)

This contrast is used as an educational comparison of PPP authentication security levels.

## Validation Checklist

Use this checklist when reviewing or demonstrating the lab in Packet Tracer:

- [ ] Verify trunk links and allowed VLANs between access/distribution/core switches
- [ ] Confirm SVI gateway reachability for all VLANs
- [ ] Test DHCP lease assignment per VLAN
- [ ] Validate RSTP roles and failover behavior after a link shutdown
- [ ] Verify LACP EtherChannel status and load sharing
- [ ] Check OSPF neighbor adjacency and route propagation
- [ ] Confirm GRE tunnel status and routed reachability through the tunnel
- [ ] Validate IPsec SAs and encrypted tunnel traffic
- [ ] Test FTP connectivity to internal server
- [ ] Confirm ACL behavior (expected permit/deny outcomes)
- [ ] Verify PPP CHAP/PAP authentication on serial link

## Notes

- This repository currently provides the project documentation summary for GitHub.
- If needed, add the `.pkt` topology file and screenshots to this repository for reproducible review and grading.

## Authoring Context

- Project: Business Center Network with two branches
- Platform: Cisco Packet Tracer
- Location context: Almaty / Taldykorgan
- Documentation year: 2025
