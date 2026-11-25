# TechNova Solutions – Enterprise Network Design Labs

## Project Overview

This repository documents a series of practical enterprise network design and implementation labs using Cisco Packet Tracer.

The project explores how to design, configure, and verify networks of different sizes, starting with a small enterprise and progressing toward medium and large enterprise environments.

The first lab focuses on **TechNova Solutions**, a small company requiring a segmented, reliable, and expandable network infrastructure.

## Lab 1: Small Enterprise Network

### 1. Business Requirements

TechNova Solutions operates in one building with approximately 35 employees and expects to grow to around 50 employees within two years.

The network includes the following departments:

| Department | End Devices |
|---|---:|
| Development | 15 PCs |
| HR | 5 PCs |
| IT | 5 PCs |
| Management | 5 PCs |
| Servers | 3 servers |

The network must provide:
- Separate network segments for each department.
- Inter-VLAN communication through a central routing device.
- Connectivity between switches.
- Link redundancy between access switches.
- A foundation for future network expansion.

### 2. Network Architecture

**Selected Architecture: Access Layer Network Design**

The network uses a simplified architecture suitable for a small enterprise.

Infrastructure:
- 2 Layer 2 Access Switches.
- 1 Router.
- 1 Firewall.
- End-user devices and servers.
- EtherChannel between the two switches.

A dedicated distribution layer is unnecessary for this network's current size.

### 3. VLAN Design

The network is segmented into five VLANs:

| Department | VLAN ID |
|---|---:|
| Development | 10 |
| HR | 20 |
| IT | 30 |
| Management | 40 |
| Servers | 50 |

VLAN segmentation separates departmental broadcast domains and provides a foundation for applying security policies.

### 4. IP Addressing and Subnetting

The `192.168.1.0/24` address space was divided using VLSM according to departmental host requirements.

| Department | Network | Subnet Mask | Usable IP Range | Broadcast |
|---|---|---|---|---|
| Development | `192.168.1.0/27` | `255.255.255.224` | `192.168.1.1 – 192.168.1.30` | `192.168.1.31` |
| HR | `192.168.1.32/29` | `255.255.255.248` | `192.168.1.33 – 192.168.1.38` | `192.168.1.39` |
| IT | `192.168.1.40/29` | `255.255.255.248` | `192.168.1.41 – 192.168.1.46` | `192.168.1.47` |
| Management | `192.168.1.48/29` | `255.255.255.248` | `192.168.1.49 – 192.168.1.54` | `192.168.1.55` |
| Servers | Pending | Pending | Pending | Pending |

VLSM allows different subnet sizes to be allocated according to the number of hosts required by each department.

### 5. Inter-VLAN Routing – Router-on-a-Stick

Router-on-a-Stick was implemented to enable communication between VLANs.

The router uses a single physical interface configured with multiple logical subinterfaces.

Each subinterface:
- Uses 802.1Q encapsulation.
- Is associated with a specific VLAN.
- Provides the Layer 3 gateway for that VLAN.

This approach enables inter-VLAN routing without requiring a Layer 3 switch.

**Implementation status:** Configured and tested successfully.

### 6. EtherChannel

EtherChannel was configured between the two access switches.

It combines multiple physical Ethernet links into one logical link.

Benefits:
- Increased aggregate bandwidth.
- Link redundancy if an individual member link fails.
- Simplified logical link management.

**Implementation status:** Configured and operational.

### 7. Verification and Testing

The implemented network was tested in Cisco Packet Tracer.

Verification included:
- VLAN configuration.
- Trunk connectivity.
- EtherChannel operation.
- Router subinterface configuration.
- Inter-VLAN routing.
- Connectivity between devices in different VLANs.

**Result:** All configured VLANs successfully communicate through the router.

### 8. Technologies Used

- Cisco Packet Tracer
- VLANs
- VLSM and subnetting
- 802.1Q trunking
- Router-on-a-Stick
- EtherChannel
- Inter-VLAN routing

### 9. Project Status

**Current Stage: Small Enterprise Network – Implementation Completed**

Completed:
- Business requirements analysis.
- Network architecture selection.
- VLAN design and segmentation.
- VLSM subnet calculations for four departments.
- VLAN and trunk configuration.
- Router-on-a-Stick configuration.
- EtherChannel configuration.
- Inter-VLAN connectivity testing.

Future improvements:
- Complete the server subnet allocation.
- Implement ACLs to enforce departmental access restrictions, including HR and Development isolation.
- Document and test additional security policies.
- Expand the design for medium and large enterprise environments.

---

## Project Roadmap

| Lab | Description | Status |
|---|---|---|
| Lab 1 | Small Enterprise Network | Implementation completed |
| Lab 2 | Medium Enterprise Network | Planned |
| Lab 3 | Large Enterprise Network | Planned |

## Repository Structure

```text
Enterprise-Network-Design-Labs/
├── README.md
├── Small-Enterprise/
│   ├── README.md
│   ├── topology/
│   ├── packet-tracer/
│   └── documentation/
├── Medium-Enterprise/
│   └── README.md
└── Large-Enterprise/
    └── README.md
```

This project is part of my practical learning journey in enterprise networking and CCNA.
