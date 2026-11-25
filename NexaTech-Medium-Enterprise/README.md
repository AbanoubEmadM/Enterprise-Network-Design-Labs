# NexaTech Solutions – Medium Enterprise Network Design

## Project Overview

This project focuses on designing and implementing a scalable enterprise network for a fictional company called **NexaTech Solutions** using Cisco Packet Tracer.

The company operates across two floors, with approximately 170 employees and a projected growth target of 250 within the next few years.

The network is designed to provide:

- Departmental network segmentation.
- Inter-VLAN communication.
- Redundant network connections.
- Loop prevention.
- Improved network availability.
- Scalability for future expansion.

The project follows a two-tier hierarchical network architecture consisting of Access and Distribution layers.

## Business Requirements

NexaTech has the following departments:

| Department | Endpoints |
|---|---:|
| Development | 65 |
| Sales | 30 |
| Finance | 20 |
| IT | 20 |
| HR | 15 |
| Management | 10 |
| Servers | 10 |

The design uses six 48-port access switches, providing 288 physical access ports to accommodate current requirements and future growth.

## Network Architecture

The network follows a two-tier hierarchical architecture.

### 1. Access Layer

The Access Layer provides network connectivity to end devices, including:

- Employee PCs
- Servers
- Other network endpoints

Six Layer 2 access switches are deployed across the two floors.

Each access switch has redundant uplinks to both distribution switches.

### 2. Distribution Layer

The Distribution Layer consists of two switches:

- DSW1
- DSW2

These switches aggregate connections from the access layer.

DSW1 performs Layer 3 switching and Inter-VLAN Routing using Switched Virtual Interfaces (SVIs).

DSW2 currently operates as a Layer 2 distribution switch. Gateway redundancy is reserved for a future implementation using HSRP.

### Network Topology

![NexaTech Network Topology](topology/01%20–%20Full%20network%20overview.png)

*Logical network topology implemented in Cisco Packet Tracer.*

## VLAN Design and IP Addressing

VLANs are used to logically separate departments and reduce unnecessary broadcast traffic between them.

The private address space `172.16.0.0` was divided using Variable Length Subnet Masking (VLSM), allocating subnets according to departmental requirements.

| VLAN ID | Department | Network | Subnet Mask | Default Gateway |
|---:|---|---|---|---|
| 10 | Development | 172.16.0.0/25 | 255.255.255.128 | 172.16.0.126 |
| 20 | Sales | 172.16.0.128/26 | 255.255.255.192 | 172.16.0.190 |
| 30 | Finance | 172.16.0.192/27 | 255.255.255.224 | 172.16.0.222 |
| 40 | IT | 172.16.0.224/27 | 255.255.255.224 | 172.16.0.254 |
| 50 | HR | 172.16.1.0/27 | 255.255.255.224 | 172.16.1.30 |
| 60 | Servers | 172.16.1.32/27 | 255.255.255.224 | 172.16.1.62 |
| 70 | Management | 172.16.1.64/27 | 255.255.255.224 | 172.16.1.94 |
| 99 | Native VLAN | - | - | - |

The last usable IP address in each departmental subnet was selected as its default gateway.

VLAN 99 was configured as the native VLAN on trunk links.

## Technologies Implemented

### VLANs and Trunking
- Created departmental VLANs across the switches.
- Configured access ports for end devices.
- Configured IEEE 802.1Q trunk links.
- Used VLAN 99 as the native VLAN.
- Restricted trunk links to the required VLANs.

### EtherChannel
- Combined two physical links between DSW1 and DSW2.
- Used Port-channel1 as the logical connection.
- Configured the EtherChannel as a trunk.

### Spanning Tree Protocol
- Implemented Rapid PVST+.
- Configured DSW1 as the primary Root Bridge for VLANs 10–70.
- Used STP to prevent Layer 2 switching loops.
- Maintained redundant paths between access and distribution switches.

### PortFast and BPDU Guard
- Enabled PortFast on end-device access ports.
- Enabled BPDU Guard to protect access ports against unexpected BPDU reception.

### Inter-VLAN Routing
- Enabled Layer 3 routing on DSW1.
- Configured seven SVIs.
- Assigned default gateway addresses to each VLAN.
- Verified connected and local routes in the routing table.
- Enabled communication between different VLANs.

## Implementation and Verification

The network was implemented and tested in Cisco Packet Tracer.

The following tests were successfully completed:

| Test | Result |
|---|---|
| VLAN creation and verification | Passed |
| Trunk configuration | Passed |
| EtherChannel operation | Passed |
| Rapid PVST+ operation | Passed |
| Root Bridge verification | Passed |
| Same-VLAN communication across switches | Passed |
| Redundant uplink failover | Passed |
| SVI operational status | Passed |
| Connected routes verification | Passed |
| Inter-VLAN communication | Passed |

All representative PCs successfully communicated with devices in other VLANs after Inter-VLAN Routing was configured.

## Project Limitations and Future Improvements

The current implementation focuses on Layer 2 switching, redundancy at the access uplink level, and Layer 3 Inter-VLAN Routing.

The following technologies are planned for future implementation as part of the learning roadmap:

- **HSRP:** Provide default gateway redundancy between distribution switches.
- **DHCP:** Implement centralized dynamic IP address allocation.
- **DNS:** Configure centralized name resolution.
- **ACLs:** Introduce traffic filtering and inter-VLAN security policies.
- **Network Monitoring:** Explore centralized monitoring and troubleshooting tools.

These features are planned enhancements and are not part of the current completed implementation.

## Repository Structure

```text
NexaTech-Medium-Enterprise/
│
├── README.md
│
├── documentation/
│   ├── 01-vlan-and-trunking.md
│   ├── 02-etherchannel.md
│   ├── 03-spanning-tree.md
│   ├── 04-inter-vlan-routing.md
│   │
│   └── images/
│       ├── full-topology.png
│       ├── distribution-layer.png
│       ├── access-layer.png
│       └── connectivity-tests.png
│
└── packet-tracer/
    └── nexatech-network.pkt
```

## Tools Used

- Cisco Packet Tracer
- Cisco IOS CLI
- Git and GitHub
- Markdown

## Learning Outcomes

Through this project, I gained practical experience in:

- Designing hierarchical enterprise network architectures.
- Planning IPv4 addressing using VLSM.
- Implementing VLAN segmentation and trunking.
- Configuring and verifying EtherChannel.
- Understanding Rapid PVST+ and redundant Layer 2 paths.
- Implementing Layer 3 switching and Inter-VLAN Routing.
- Testing network connectivity and redundancy.

---

**Project Status:** Layer 2 and Layer 3 core implementation completed. Additional network services and gateway redundancy are planned.

*Built as part of my CCNA learning journey, focusing on practical networking and enterprise network design.*