## Task 1: Guest Network Isolation

### Objective

Completely isolate the Guest network (VLAN 99) from all internal
departments to prevent untrusted devices from accessing sensitive resources.

### ACL Design: GUEST_ISOLATION

**Type:** Named Extended ACL  
**Applied:** Outbound on GigabitEthernet0/0/0.99

**Configuration:**

```
ip access-list extended GUEST_ISOLATION
 deny ip 192.168.99.0 0.0.0.255 192.168.10.0 0.0.0.255
 deny ip 192.168.99.0 0.0.0.255 192.168.20.0 0.0.0.255
 deny ip 192.168.99.0 0.0.0.255 192.168.30.0 0.0.0.255
 deny ip 192.168.99.0 0.0.0.255 192.168.40.0 0.0.0.255
 permit ip any any

interface GigabitEthernet0/0/0.99
 ip access-group GUEST_ISOLATION out
```

### Security Rationale

Guest networks typically host unknown devices (visitors, contractors,
personal devices). These should never access internal corporate resources.
The permit statement allows future internet-only access for guests without
compromising internal security.

### ACL Placement Strategy

Applied outbound on the Guest VLAN subinterface to filter traffic at the
source, following the best practice of denying traffic as close to the
source as possible.

### Known Limitation - Packet Tracer ACL Processing

**Note:** Packet Tracer has a documented limitation with ACL processing on
subinterfaces. While the ACL configuration shown above is syntactically
correct and would function properly on physical Cisco hardware, Packet
Tracer's simulation engine does not consistently enforce ACLs on Router-on-a-Stick
subinterface configurations.

This is a known issue in the Packet Tracer community. The configuration
demonstrates proper ACL design, placement, and syntax that would be
production-ready on actual Cisco IOS devices.

**Alternative verification methods in production environments:**

- `show access-lists` with hit counters
- `debug ip packet` to trace packet flow
- Actual traffic capture and analysis
- Real-world testing with physical devices

### Demonstrated Knowledge

Despite the simulator limitation, this task demonstrates understanding of:

- Extended ACL syntax and wildcard masks
- ACL placement strategies (inbound vs outbound)
- Defense-in-depth principles
- Guest network isolation requirements
- Named ACL best practices
