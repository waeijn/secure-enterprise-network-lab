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
