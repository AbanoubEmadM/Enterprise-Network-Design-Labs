# EtherChannel Configuration

## 1. Overview

EtherChannel was implemented between the two distribution switches, DSW1 and DSW2.

The purpose is to combine multiple physical links into one logical connection, increasing available bandwidth and providing link-level redundancy.

## 2. Topology

- DSW1: Distribution Switch 1
- DSW2: Distribution Switch 2
- Physical member interfaces: Fa0/3 and Fa0/4
- Logical interface: Port-channel1

Both physical interfaces were bundled into the same EtherChannel.

## 3. Configuration Objectives

- Establish an EtherChannel between DSW1 and DSW2.
- Configure the logical connection as an 802.1Q trunk.
- Carry the required VLANs across the bundle.
- Use VLAN 99 as the native VLAN.

## 4. Trunk Configuration

Port-channel1 carries:

- VLAN 10 – Development
- VLAN 20 – Sales
- VLAN 30 – Finance
- VLAN 40 – IT
- VLAN 50 – HR
- VLAN 60 – Servers
- VLAN 70 – Management
- VLAN 99 – Native VLAN

## 5. Verification

Commands used:

```cisco
show etherchannel summary
show interfaces port-channel 1
show interfaces trunk
```

## 6. Testing

- Verified that the physical interfaces joined Port-channel1.
- Verified that the logical interface was operational.
- Verified trunk operation and VLAN propagation.

**Result:** EtherChannel was successfully established between the distribution switches.