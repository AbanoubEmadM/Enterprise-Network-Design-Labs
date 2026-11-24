# VLAN Design and IP Addressing

## 1. Overview

The TechNova Solutions network uses VLAN segmentation to separate departments into different logical networks.

Each department is assigned a dedicated VLAN and IP subnet. This design helps organize network traffic, reduce broadcast domains, and provide a foundation for implementing access-control policies.

## 2. VLAN Allocation

The following VLANs were created for the network:

| Department | VLAN ID |
|---|---:|
| Development | 10 |
| HR | 20 |
| IT | 30 |
| Management | 40 |
| Servers | 50 |

Each VLAN represents a separate logical broadcast domain.

## 3. IP Addressing Strategy

The network uses the private address space `192.168.1.0/24`.

Variable Length Subnet Masking (VLSM) was used to divide the address space into smaller subnets according to the host requirements of each department.

Larger subnets were allocated to departments with more devices, while smaller subnets were allocated to departments with fewer devices.

## 4. Subnet Allocation

| Department | VLAN | Network Address | Prefix | Subnet Mask |
|---|---:|---|---|---|
| Development | 10 | `192.168.1.0` | /27 | `255.255.255.224` |
| HR | 20 | `192.168.1.32` | /29 | `255.255.255.248` |
| IT | 30 | `192.168.1.40` | /29 | `255.255.255.248` |
| Management | 40 | `192.168.1.48` | /29 | `255.255.255.248` |
| Servers | 50 | Pending | Pending | Pending |

## 5. Detailed Subnet Calculations

### Development – VLAN 10

- Required devices: 15 PCs
- Network address: `192.168.1.0/27`
- Subnet mask: `255.255.255.224`
- Total addresses: 32
- Usable host addresses: 30
- First usable address: `192.168.1.1`
- Last usable address: `192.168.1.30`
- Broadcast address: `192.168.1.31`

### HR – VLAN 20

- Required devices: 5 PCs
- Network address: `192.168.1.32/29`
- Subnet mask: `255.255.255.248`
- Total addresses: 8
- Usable host addresses: 6
- First usable address: `192.168.1.33`
- Last usable address: `192.168.1.38`
- Broadcast address: `192.168.1.39`

### IT – VLAN 30

- Required devices: 5 PCs
- Network address: `192.168.1.40/29`
- Subnet mask: `255.255.255.248`
- Total addresses: 8
- Usable host addresses: 6
- First usable address: `192.168.1.41`
- Last usable address: `192.168.1.46`
- Broadcast address: `192.168.1.47`

### Management – VLAN 40

- Required devices: 5 PCs
- Network address: `192.168.1.48/29`
- Subnet mask: `255.255.255.248`
- Total addresses: 8
- Usable host addresses: 6
- First usable address: `192.168.1.49`
- Last usable address: `192.168.1.54`
- Broadcast address: `192.168.1.55`

## 6. VLSM Design Considerations

VLSM allows efficient allocation of IP addresses by assigning different subnet sizes based on host requirements.

In this design:

- Development received a `/27` subnet to accommodate its larger number of devices.
- HR, IT, and Management received `/29` subnets.

The current subnet allocations are non-overlapping.

## 7. Implementation Status

- [x] VLAN allocation planned.
- [x] VLANs configured.
- [x] IP subnet calculations completed for four departments.
- [x] VLAN segmentation implemented.
- [x] Document gateway addresses and final device IP assignments.

Implementation Status: Completed and Operational