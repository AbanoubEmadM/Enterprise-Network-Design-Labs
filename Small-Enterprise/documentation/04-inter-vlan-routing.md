# Inter-VLAN Routing – Router-on-a-Stick

## 1. Overview

The TechNova Solutions network contains multiple VLANs, each representing a separate department.

Since VLANs create separate Layer 2 broadcast domains, communication between devices in different VLANs requires a Layer 3 routing mechanism.

Router-on-a-Stick (ROAS) was implemented to enable communication between the VLANs using a single physical router interface.

## 2. Network Design

The router connects to the first access switch through a trunk link.

The router's physical interface is divided into multiple logical subinterfaces. Each subinterface is assigned to a specific VLAN using IEEE 802.1Q encapsulation.

Each subinterface acts as the default gateway for its corresponding VLAN.

### VLAN-to-Subnet Mapping

| Department | VLAN | Network |
|---|---:|---|
| Development | 10 | `192.168.1.0/27` |
| HR | 20 | `192.168.1.32/29` |
| IT | 30 | `192.168.1.40/29` |
| Management | 40 | `192.168.1.48/29` |
| Servers | 50 | Pending |

## 3. How Router-on-a-Stick Works

1. A device sends traffic to another device in a different VLAN.
2. The source device forwards the packet to its default gateway.
3. The access switch forwards the tagged frame to the router over the trunk link.
4. The router receives the frame through the corresponding subinterface.
5. The router performs the Layer 3 routing operation.
6. The packet is forwarded through the appropriate subinterface toward the destination VLAN.

This allows devices in different VLANs to communicate without requiring a dedicated physical router interface for every VLAN.

## 4. Configuration

The router was configured with multiple subinterfaces, each associated with its respective VLAN.

Example configuration structure:

```cisco
interface GigabitEthernet0/0
 no shutdown

interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address <VLAN10-GATEWAY> <SUBNET-MASK>

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address <VLAN20-GATEWAY> <SUBNET-MASK>

interface GigabitEthernet0/0.30
 encapsulation dot1Q 30
 ip address <VLAN30-GATEWAY> <SUBNET-MASK>

interface GigabitEthernet0/0.40
 encapsulation dot1Q 40
 ip address <VLAN40-GATEWAY> <SUBNET-MASK>
```

**Note:** Replace the interface name and gateway placeholders with the actual values used in the Packet Tracer implementation. Add the server subinterface when its subnet is allocated.

## 5. Switch Configuration Requirements

The switch port connected to the router must operate as an 802.1Q trunk.

The trunk must allow the VLANs that need to communicate with the router.

This ensures that traffic from different VLANs can reach the correct router subinterfaces.

## 6. Verification and Testing

The configuration was verified using the following commands:

```cisco
show ip interface brief
show running-config
show interfaces trunk
```

Connectivity tests were performed between devices belonging to different VLANs.

**Result:** Inter-VLAN routing was successfully implemented, and devices across the configured VLANs can communicate with each other.

## 7. Advantages of Router-on-a-Stick

- Requires only one physical router interface for multiple VLANs.
- Provides centralized inter-VLAN routing.
- Reduces hardware requirements.
- Suitable for small enterprise networks.

## 8. Limitations

- All inter-VLAN traffic passes through one physical router link.
- The router interface can become a bandwidth bottleneck.
- The router represents a potential single point of failure.

## 9. Implementation Status

- [x] Router physical interface configured.
- [x] Router subinterfaces configured.
- [x] 802.1Q encapsulation implemented.
- [x] Switch-to-router trunk configured.
- [x] Inter-VLAN routing tested successfully.

**Implementation Status: Completed and Operational**