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

## Task 3: Switch Port Hardening

### Overview

Hardened the switch by disabling all unused ports and assigning
them to a blackhole VLAN to prevent rogue device attacks.

### Security Problem

Unused switch ports default to VLAN 1 and remain active,
allowing any device plugged into them to gain network access.

### Controls Applied

#### Blackhole VLAN (VLAN 999)

Created a dedicated VLAN with no routed interface. All unused
ports are assigned here so even if the shutdown is bypassed,
traffic goes nowhere.

#### Port Shutdown

Administratively disabled all unused ports (Fa0/6-24, Gi0/2)
using the shutdown command. These ports will show as
"disabled" in interface status.

### Defense-in-Depth

Both controls are applied together following the
defense-in-depth principle: never rely on a single
security control.

### Ports Hardened

- FastEthernet0/6 through FastEthernet0/24 (19 ports)
- GigabitEthernet0/2 (1 port)
- Total: 20 ports disabled and assigned to VLAN 999

### Testing

Verified active ports (Fa0/1-5, Gi0/1) still function
correctly after hardening via successful ping tests.

## Week 1 Summary

### Accomplishments

Successfully transformed a flat, insecure network into a properly
segmented enterprise network with VLAN isolation and hardened
switch configurations.

### Key Security Improvements

**Before (Baseline):**

- Single flat network (192.168.1.0/24)
- No segmentation between departments
- Unrestricted lateral movement
- Unused ports active and vulnerable

**After (Segmented & Hardened):**

- 5 separate VLANs with dedicated subnets
- Department isolation via VLAN segmentation
- Inter-VLAN routing controlled through R1-Core
- 20 unused ports disabled and assigned to blackhole VLAN
- Foundation established for ACL enforcement (Week 2)

### Files Delivered

- `week1_baseline.pkt` - Initial flat network
- `week1_segmented.pkt` - Segmented and hardened network
- 9 verification screenshots
- Complete documentation

### Next Steps

Week 2 will implement Access Control Lists (ACLs) to enforce
least-privilege access policies between departments.
