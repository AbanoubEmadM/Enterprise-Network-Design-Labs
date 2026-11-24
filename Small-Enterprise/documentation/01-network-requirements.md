# Network Requirements – TechNova Solutions

## 1. Business Scenario

TechNova Solutions is a small company operating from a single building with approximately 35 employees.

The company requires a reliable and organized network infrastructure that supports communication between departments while allowing future expansion.

The network is expected to accommodate approximately 50 employees within the next two years.

## 2. Departmental Requirements

The company consists of the following departments:

| Department | Number of Employees / Devices |
|---|---:|
| Development | 15 |
| HR | 5 |
| IT | 5 |
| Management | 5 |

## 3. Network Requirements

The proposed network must satisfy the following requirements:

### Connectivity
- Provide network connectivity to all departments.
- Enable communication between different departmental networks.
- Provide connectivity to the Internet through a single Internet connection.

### Network Segmentation
- Separate departments using VLANs.
- Assign a dedicated IP subnet to each VLAN.
- Prevent unnecessary mixing of departmental broadcast traffic.

### Infrastructure
- Use Layer 2 access switches for endpoint connectivity.
- Provide inter-VLAN routing through a router.
- Establish connectivity between access switches.
- Implement EtherChannel for inter-switch link redundancy and bandwidth aggregation.

### Administration and Security
- Allow IT administrators to manage network devices.
- Establish a foundation for future access-control policies.
- Support future network security improvements.

### Scalability
- Support the company's expected growth.
- Allow additional devices and network segments to be introduced when needed.

## 4. Hardware Constraints

The available equipment includes:

- Cisco Catalyst 24-port or 48-port switches.
- One router.
- One network rack.
- Ethernet cabling.

The design should make reasonable use of the available hardware while avoiding unnecessary infrastructure complexity.

## 5. Design Constraints and Considerations

- The company operates from a single building.
- The network has a limited hardware budget.
- A dedicated distribution layer is not currently required.
- The initial design uses a single router and a single firewall.
- ACL-based departmental restrictions are planned as a future security improvement.

## 6. Expected Outcome

A functional small enterprise network that provides:

- Departmental VLAN segmentation.
- Inter-VLAN communication.
- Redundant inter-switch links through EtherChannel.
- Centralized routing.
- A foundation for future expansion and security improvements.
