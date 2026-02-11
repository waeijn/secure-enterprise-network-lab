# Week 1: Secure Network Architecture & Segmentation

## Task 1: Baseline Network (Flat Network)

### Overview

Created a flat network topology to demonstrate the security problem of unrestricted lateral movement.

### Topology

- 1 Router (R1-Core)
- 1 Switch (SW1-Core)
- 5 PCs (IT, HR, Finance, Operations, Guest)

### IP Addressing Scheme

- Network: 192.168.1.0/24
- PC-IT: 192.168.1.10
- PC-HR: 192.168.1.20
- PC-Finance: 192.168.1.30
- PC-Operations: 192.168.1.40
- PC-Guest: 192.168.1.50
- Gateway: 192.168.1.1 (Router)

### Security Problem Identified

All devices are in the same subnet with no segmentation. Any compromised device can communicate with all other devices, including sensitive departments like Finance and HR.

### Testing

Successfully pinged between all PCs, confirming the flat network security issue.

## Task 2: VLAN Segmentation

### Overview

Transformed the flat network into a segmented network using VLANs and
Router-on-a-Stick inter-VLAN routing.

### VLAN Design

| VLAN | Department | Subnet          |
| ---- | ---------- | --------------- |
| 10   | IT         | 192.168.10.0/24 |
| 20   | HR         | 192.168.20.0/24 |
| 30   | Finance    | 192.168.30.0/24 |
| 40   | Operations | 192.168.40.0/24 |
| 99   | Guest      | 192.168.99.0/24 |

### Security Improvement

Each department is now isolated in its own VLAN and subnet.
Lateral movement between departments now requires passing through
the router, enabling future access control enforcement via ACLs.

### Router-on-a-Stick

Configured subinterfaces on R1-Core GigabitEthernet0/0 to handle
inter-VLAN routing for all 5 VLANs using 802.1Q encapsulation.

### Testing

Successfully verified inter-VLAN routing with ping tests between
all department PCs.
