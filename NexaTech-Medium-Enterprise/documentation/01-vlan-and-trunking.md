# VLANs and Trunking

## 1. Overview

NexaTech Solutions uses VLAN segmentation to separate departments into logical broadcast domains.

The network contains seven VLANs for departmental users, servers, and management.

## 2. VLAN Design

| VLAN ID | Name | Department |
|---|---|---|
| 10 | DEVELOPMENT | Development |
| 20 | SALES | Sales |
| 30 | FINANCE | Finance |
| 40 | IT | IT |
| 50 | HR | Human Resources |
| 60 | SERVERS | Servers |
| 70 | MANAGEMENT | Management |
| 99 | NATIVE | Native VLAN |

## 3. IP Addressing Plan

The network uses the private address space `172.16.0.0`.

| VLAN | Network | Subnet Mask | Usable Addresses |
|---|---|---|---|
| 10 | 172.16.0.0/25 | 255.255.255.128 | 126 |
| 20 | 172.16.0.128/26 | 255.255.255.192 | 62 |
| 30 | 172.16.0.192/27 | 255.255.255.224 | 30 |
| 40 | 172.16.0.224/27 | 255.255.255.224 | 30 |
| 50 | 172.16.1.0/27 | 255.255.255.224 | 30 |
| 60 | 172.16.1.32/27 | 255.255.255.224 | 30 |
| 70 | 172.16.1.64/27 | 255.255.255.224 | 30 |

VLSM was used to allocate subnets according to departmental requirements while preserving address space for future growth.

## 4. Trunking

802.1Q trunk links were configured to carry multiple VLANs between switches.

Native VLAN: 99

Allowed VLANs: 10, 20, 30, 40, 50, 60, 70, 99.

All access switches and distribution switches were configured with the required VLANs.

## 5. Access Port Security Configuration

End-device access ports were configured with:

- PortFast
- BPDU Guard

These settings help devices transition quickly to the forwarding state and protect access ports against unexpected BPDU reception.

## 6. Verification

The following commands were used:

```cisco
show vlan brief
show interfaces trunk
show interfaces switchport
```

## 7. Testing

- Verified VLAN creation across switches.
- Verified trunk operation.
- Verified that required VLANs were allowed across trunk links.
- Tested communication between devices belonging to the same VLAN on different switches.

**Result:** VLAN segmentation and trunking were successfully implemented and verified.