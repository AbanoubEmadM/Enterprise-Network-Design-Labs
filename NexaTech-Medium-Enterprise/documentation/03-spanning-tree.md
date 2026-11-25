# Spanning Tree Protocol (Rapid PVST+)

## 1. Overview

The NexaTech network contains redundant Layer 2 connections between access and distribution switches.

While redundancy improves network availability, multiple Layer 2 paths can create switching loops.

Rapid PVST+ was implemented to prevent Layer 2 loops while maintaining redundant paths.

## 2. Protocol Selection

Protocol: Rapid PVST+

Rapid PVST+ maintains a separate spanning-tree instance for each VLAN and provides faster convergence than traditional 802.1D STP.

## 3. Root Bridge Design

DSW1 was selected as the primary root bridge for the departmental VLANs.

The following configuration was applied:

```cisco
spanning-tree vlan 10,20,30,40,50,60,70 root primary
```

This makes DSW1 the preferred root bridge for these VLANs.

## 4. Redundant Links

Each access switch has redundant uplinks to the distribution layer.

STP determines which paths should forward traffic and which redundant paths should remain blocked for each VLAN.

The selected port roles and states may differ between VLANs because Rapid PVST+ operates independently per VLAN.

## 5. Verification

Commands used:

```cisco
show spanning-tree
show spanning-tree vlan 10
show spanning-tree vlan 20
show spanning-tree root
show spanning-tree inconsistentports
```

## 6. Testing

The following tests were performed:

- Verified DSW1 as the root bridge.
- Verified STP port roles and states.
- Checked that redundant paths were handled by STP.
- Tested same-VLAN communication across different switches.
- Temporarily disconnected an access-switch uplink and verified that communication continued through the redundant path.

**Result:** Rapid PVST+ successfully prevented Layer 2 loops while preserving connectivity through redundant uplinks.

## 7. Future Improvements

- Configure DSW2 as the secondary root bridge.
- Evaluate STP root placement per VLAN.
- Review STP convergence after topology changes.