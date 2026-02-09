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
