# Week 3: Device & Network Hardening

## Overview

Week 3 focuses on securing the network infrastructure devices themselves
(routers and switches) through authentication hardening, encrypted
management access, and attack surface reduction.

## Security Problems Addressed

### Current Vulnerabilities

- **Weak Authentication**: Default or no passwords on devices
- **Plaintext Management**: Telnet sends credentials unencrypted
- **No Legal Warning**: Missing login banners for unauthorized access
- **Password Exposure**: Passwords visible in plaintext in configs
- **Open Management Access**: Devices accessible from any VLAN
- **Unnecessary Services**: CDP, HTTP server, and other services running
- **Unused Interfaces**: Additional attack surface

### Attack Scenarios

- Attacker on Guest network could Telnet to router/switch
- Sniffed Telnet session reveals admin password
- Compromised device grants full network control
- No legal recourse for unauthorized access attempts

## Security Objectives

1. **Authentication Hardening**
   - Strong enable secret passwords
   - Strong line passwords (console, VTY)
   - Password encryption

2. **Encrypted Management**
   - SSH v2 enabled
   - Telnet disabled
   - RSA key generation

3. **Legal Protection**
   - Login banners
   - MOTD (Message of the Day)

4. **Management Access Control**
   - VTY access restricted to IT VLAN only
   - Console access secured

5. **Service Hardening**
   - Disable CDP where not needed
   - Disable HTTP server
   - Disable unused interfaces

## Devices to Harden

- R1-Core (4331 Router)
- SW1-Core (2960 Switch)

## Task 1: Password Hardening & Encryption

### Objective

Implement strong password policies and encryption on all network devices
to prevent unauthorized access and credential theft.

### Password Policy Implemented

**Requirements:**

- Minimum 12 characters
- Mix of uppercase, lowercase, numbers, special characters
- No dictionary words
- Different passwords for different access methods

**Passwords Configured:**

- Enable secret: Cisco@2026!Secure
- Console password: Console@2026!
- VTY password: VTY@2026!Remote

### Configuration Applied

#### Router (R1-Core)

```
enable secret Cisco@2026!Secure
service password-encryption

line console 0
 password Console@2026!
 login

line vty 0 4
 password VTY@2026!Remote
 login
```

#### Switch (SW1-Core)

```
enable secret Cisco@2026!Secure
service password-encryption

line console 0
 password Console@2026!
 login

line vty 0 15
 password VTY@2026!Remote
 login

interface vlan 10
 ip address 192.168.10.254 255.255.255.0

ip default-gateway 192.168.10.1
```

### Password Encryption Types

**Enable Secret (Type 5 - MD5):**

- One-way hash function
- Cannot be reversed to plaintext
- Industry standard for privileged access

**Service Password-Encryption (Type 7):**

- Weak Cisco proprietary encryption
- Easily reversible but better than plaintext
- Protects against casual viewing of configs

### Security Rationale

**Why Strong Passwords Matter:**

- Default or weak passwords are the primary attack vector
- Compromised device grants full network control
- Enables lateral movement to all VLANs
- Allows modification of ACLs, routing, and data theft

**Defense in Depth:**
Even with network segmentation and ACLs, physical or remote access
to devices must be protected. Multiple password layers (console, VTY,
enable) create authentication barriers.

### Testing Results

- Enable secret required for privileged EXEC mode
- Console password required for physical access
- VTY password required for remote Telnet/SSH access
- All passwords encrypted in running-config
- No plaintext credentials visible

### Management Access Configuration

Switch management IP configured in IT VLAN (192.168.10.254) to enable
remote administration from the IT department while maintaining network
segmentation.
