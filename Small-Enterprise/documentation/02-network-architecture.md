# Network Architecture – TechNova Solutions

## 1. Architecture Overview

The TechNova Solutions network follows a simplified hierarchical network design using an Access Layer architecture.

Because the company operates from a single building and has a relatively small number of employees, a dedicated Distribution Layer and Core Layer are not necessary for the initial implementation.

The network uses two Layer 2 access switches and one router to provide endpoint connectivity and inter-VLAN routing.

## 2. Selected Architecture

**Architecture: Access Layer Only**

The infrastructure consists of:

| Device | Role |
|---|---|
| Router | Inter-VLAN routing and external connectivity |
| Access Switch 1 | Connects end devices and provides connectivity to the router |
| Access Switch 2 | Connects additional end devices |
| Firewall | Provides network security at the external network boundary |

The two access switches are interconnected using EtherChannel.

## 3. Why This Architecture Was Selected

The architecture was selected based on the company's size, budget, and infrastructure requirements.

Reasons include:

- A single building does not require a complex multi-layer campus architecture.
- Two access switches provide sufficient connectivity for the initial device requirements.
- Layer 2 switches reduce hardware costs.
- Router-on-a-Stick provides inter-VLAN routing without requiring a Layer 3 switch.
- EtherChannel provides link redundancy between the access switches.
- The design is relatively simple to manage and expand.

## 4. Network Topology

The logical topology follows this structure:

```text
                 Internet
                    |
                 Firewall
                    |
                  Router
                    |
               802.1Q Trunk
                    |
              Access Switch 1
                    |
              EtherChannel
                    |
              Access Switch 2
```

End devices and servers connect to the appropriate access switch ports according to their VLAN assignments.

## 5. VLAN Architecture

The network is divided into five logical segments:

| Department | VLAN |
|---|---:|
| Development | 10 |
| HR | 20 |
| IT | 30 |
| Management | 40 |

Each VLAN has a dedicated IP subnet.

Refer to `03-vlan-and-ip-addressing.md` for the detailed addressing plan.

## 6. Routing Architecture

Router-on-a-Stick is used to provide communication between VLANs.

The router connects to Access Switch 1 through an 802.1Q trunk.

Multiple router subinterfaces handle traffic for the different VLANs.

Refer to `04-inter-vlan-routing.md` for the implementation details.

## 7. Switch Interconnection

Access Switch 1 and Access Switch 2 are connected using EtherChannel.

Multiple physical links are combined into one logical Port-channel interface.

This provides aggregate bandwidth and redundancy against individual physical link failures.

Refer to `05-etherchannel.md` for the configuration details.

## 8. Security Considerations

VLAN segmentation separates departmental broadcast domains, but it does not automatically prevent communication between departments.

Future security improvements include:

- Implementing ACLs to restrict communication between selected VLANs.
- Preventing direct access from HR to Development resources.
- Defining appropriate management access policies.
- Reviewing firewall policies for external connectivity.

## 9. Scalability and Limitations

The current architecture is appropriate for a small enterprise.

However, the design has limitations:

- The router is a single point of failure for inter-VLAN routing.
- Each access switch is a single point of failure for devices connected to it.
- The single router interface used by Router-on-a-Stick can become a bandwidth bottleneck.
- A dedicated Distribution Layer may become necessary as the company grows.

## 10. Implementation Status

- [x] Architecture selected.
- [x] Two Layer 2 access switches implemented.
- [x] Router-on-a-Stick configured.
- [x] EtherChannel configured.
- [x] Inter-VLAN connectivity verified.
- [ ] Departmental ACL policies.
- [ ] Additional redundancy and scalability improvements.