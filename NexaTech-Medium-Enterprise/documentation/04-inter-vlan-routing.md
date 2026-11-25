# Inter-VLAN Routing Using Layer 3 Switching

## 1. Overview

Inter-VLAN routing was implemented using the Layer 3 capabilities of DSW1.

The objective was to allow devices belonging to different VLANs and IP subnets to communicate.

DSW1 acts as the default gateway for all seven VLANs.

DSW2 remains a Layer 2 distribution switch. Gateway redundancy using HSRP is reserved for a future improvement.

## 2. Layer 3 Routing

IP routing was enabled on DSW1:

```cisco
ip routing
```

This allows the switch to forward packets between directly connected IP networks.

## 3. SVI Configuration

A Switched Virtual Interface (SVI) was created for each departmental VLAN.

The last usable IP address in each subnet was selected as its default gateway.

| VLAN | Department | SVI IP Address | Subnet Mask |
|---|---|---|---|
| 10 | Development | 172.16.0.126 | 255.255.255.128 |
| 20 | Sales | 172.16.0.190 | 255.255.255.192 |
| 30 | Finance | 172.16.0.222 | 255.255.255.224 |
| 40 | IT | 172.16.0.254 | 255.255.255.224 |
| 50 | HR | 172.16.1.30 | 255.255.255.224 |
| 60 | Servers | 172.16.1.62 | 255.255.255.224 |
| 70 | Management | 172.16.1.94 | 255.255.255.224 |

## 4. Routing Table Verification

The routing table was inspected using:

```cisco
show ip route
```

DSW1 successfully installed seven connected routes (C), one for each VLAN subnet, and seven local routes (L), representing its SVI addresses.

Example:

```text
C 172.16.0.0/25 is directly connected, Vlan10
L 172.16.0.126/32 is directly connected, Vlan10
```

## 5. End-Device Configuration

Representative PCs were configured with:

- An IP address belonging to their assigned subnet.
- The correct subnet mask.
- The corresponding SVI address as their default gateway.

## 6. Connectivity Testing

The following tests were performed:

1. Same-VLAN communication across different switches.
2. Inter-VLAN communication between different departments.
3. End-to-end connectivity between representative PCs.

All representative PCs successfully communicated with one another after inter-VLAN routing was enabled.

## 7. Result

Inter-VLAN routing was successfully implemented using SVIs on DSW1.

The Layer 3 switch now routes traffic between all seven departmental networks.

## 8. Future Improvements

- Implement HSRP for default gateway redundancy.
- Configure centralized DHCP services.
- Configure DNS services.
- Introduce inter-VLAN access control policies.