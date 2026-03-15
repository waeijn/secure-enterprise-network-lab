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

## Task 2: Enable SSH and Disable Telnet

### Objective

Replace insecure Telnet access with encrypted SSH for all remote
device management to protect credentials and commands from
network sniffing attacks.

### Security Problem - Telnet

Telnet transmits all data in plaintext including:

- Authentication credentials
- Configuration commands
- Sensitive network information
- Session data

Any attacker with network access can capture Telnet traffic and
extract passwords using packet sniffers like Wireshark.

### SSH Implementation

#### Configuration Applied

**Router (R1-Core):**

```
hostname R1-Core
ip domain-name enterprise.local
crypto key generate rsa modulus 2048
ip ssh version 2
ip ssh time-out 60
ip ssh authentication-retries 3

username admin privilege 15 secret Admin@2026!SSH

line vty 0 4
 transport input ssh
 login local
```

**Switch (SW1-Core):**

```
hostname SW1-Core
ip domain-name enterprise.local
crypto key generate rsa modulus 2048
ip ssh version 2
ip ssh time-out 60
ip ssh authentication-retries 3

username admin privilege 15 secret Admin@2026!SSH

line vty 0 15
 transport input ssh
 login local
```

### SSH Components Explained

**RSA Key Pair (2048-bit):**

- Public key: Shared with clients for encryption
- Private key: Kept secret on device for decryption
- 2048-bit provides strong cryptographic protection

**SSH Version 2:**

- Modern, secure protocol
- Fixes vulnerabilities in SSH v1
- Industry standard and compliance requirement

**Local Username Database:**

- Individual user accounts vs shared line password
- Privilege level 15 grants immediate privileged access
- Better accountability and audit trails

**Transport Input SSH:**

- Explicitly allows only SSH protocol
- Blocks Telnet completely
- Prevents plaintext management access

### Security Improvements

**Before (Telnet):**

- Plaintext transmission
- Credentials visible to sniffers
- No encryption
- Vulnerable to man-in-the-middle attacks

**After (SSH):**

- End-to-end encryption
- Credentials protected
- Server authentication via RSA keys
- Resistant to eavesdropping

### Session Security Settings

**Timeout: 60 seconds**

- Disconnects idle sessions automatically
- Prevents abandoned sessions from remaining open
- Reduces attack window

**Authentication Retries: 3**

- Limits brute force login attempts
- Disconnects after 3 failed attempts
- Forces attacker to reconnect (slows attacks)

### Testing Results

- SSH version 2 enabled on both devices
- 2048-bit RSA keys generated successfully
- SSH login working with username/password authentication
- Telnet access blocked (connection refused)
- VTY lines configured for SSH-only transport
- Privilege 15 access granted to admin user

## Task 3: Login Banners & Management Access Control

### Part A: Login Banners

#### Objective

Implement legal warning banners to establish authorized use policies
and provide legal protection against unauthorized access.

#### Banner Types Configured

**Message of the Day (MOTD):**

- Displays before login prompt
- Provides legal warning
- Establishes no expectation of privacy
- Warns of monitoring and prosecution

**Login Banner:**

- Displays after MOTD, before authentication
- Reinforces authorized access requirement

#### Configuration Applied

**Both Router and Switch:**

```
banner motd #
*********************************************************************
WARNING: UNAUTHORIZED ACCESS TO THIS DEVICE IS PROHIBITED

This system is for authorized use only. All activity is monitored
and logged. Unauthorized access or use may result in criminal and/or
civil prosecution to the fullest extent of the law.

Disconnect immediately if you are not an authorized user.
*********************************************************************
#

banner login #
*********************************************************************
AUTHORIZED PERSONNEL ONLY
Provide valid credentials to proceed.
*********************************************************************
#
```

#### Legal Protection Rationale

**Why Banners Matter:**

- Establishes explicit "authorized use only" policy
- Removes expectation of privacy for users
- Strengthens legal standing for prosecution
- Required by many compliance frameworks (PCI-DSS, HIPAA)

**Best Practices Followed:**

- No welcoming language (avoids implied permission)
- Clear warning about monitoring
- Statement of legal consequences
- Instruction to disconnect if unauthorized

### Part B: Management Access Control

#### Objective

Restrict SSH management access to devices to only the IT VLAN,
preventing unauthorized management attempts from other departments
or Guest network.

#### Access Policy

- IT VLAN (192.168.10.0/24): ALLOWED
- All other VLANs: DENIED

#### Configuration Applied

**Router (R1-Core):**

```
banner motd #
[warning text]
#

banner login #
[login text]
#
```

**Switch (SW1-Core):**

```
banner motd #
[warning text]
#
```

**Note:** The 2960 switch in Packet Tracer does not support the `banner login`
command. Only MOTD banner is configured, which is the primary legal warning
and appears before authentication.

#### Access-Class Explained

**Standard ACL on VTY Lines:**

- Filters incoming SSH connections by source IP
- Applied with `access-class` command (not `ip access-group`)
- `in` direction filters connections TO the device
- Only permitted IPs can establish SSH sessions

**Why Standard ACL?**

- Only need to filter by source IP (not destination, port, etc.)
- Simpler and more efficient than extended ACL
- Industry best practice for VTY access control

#### Security Rationale

**Defense Against:**

- Unauthorized management access from Guest network
- Lateral movement attempts after department compromise
- Insider threats from non-IT personnel
- Accidental configuration changes by unauthorized users

**Layered Security:**
This combines with existing controls:

- Layer 1: Network segmentation (VLANs)
- Layer 2: Access control (ACLs between VLANs)
- Layer 3: SSH authentication (username/password)
- Layer 4: Management access restriction (this task)

#### Testing Results

- MOTD and login banners display on SSH connection
- IT VLAN successfully connects via SSH
- HR VLAN SSH connection refused
- Guest VLAN SSH connection refused
- Management plane secured to IT department only

## Task 4: Disable Unused Services & Final Hardening

### Objective

Reduce attack surface by disabling unnecessary services and implementing
session timeout controls on network devices.

### Attack Surface Reduction

#### Services Disabled

**CDP (Cisco Discovery Protocol):**

- Disabled globally on router
- Disabled on Guest access port (Fa0/5) on switch
- Prevents information disclosure to untrusted networks

**Session Timeout:**

- 5-minute exec timeout on console and VTY lines
- Automatically disconnects idle sessions
- Prevents abandoned sessions from remaining open

### Configuration Applied

#### Router (R1-Core)

```
no cdp run

interface GigabitEthernet0/0/0.10
 no ip proxy-arp

interface GigabitEthernet0/0/0.20
 no ip proxy-arp

interface GigabitEthernet0/0/0.30
 no ip proxy-arp

interface GigabitEthernet0/0/0.40
 no ip proxy-arp

interface GigabitEthernet0/0/0.99
 no ip proxy-arp

line console 0
 exec-timeout 5 0

line vty 0 4
 exec-timeout 5 0
```

#### Switch (SW1-Core)

```
interface FastEthernet0/5
 no cdp enable

line console 0
 exec-timeout 5 0

line vty 0 15
 exec-timeout 5 0
```

### Packet Tracer Limitations

The 4331 router model in Packet Tracer has limited support for some advanced
hardening commands. The following commands are not available but would be
implemented in production Cisco IOS environments:

- `no ip http server` - Disable HTTP web interface
- `no ip http secure-server` - Disable HTTPS web interface
- `no ip source-route` - Disable IP source routing

These are industry-standard hardening practices and would be included in
real-world deployments.

### Security Controls Explained

**CDP Disable:**

- CDP broadcasts device information (hostname, IOS version, IP addresses)
- Valuable reconnaissance data for attackers
- Disabled globally on router for maximum security
- Disabled on untrusted Guest port on switch

**Exec Timeout:**

- Auto-logout after 5 minutes of inactivity
- Prevents abandoned sessions from staying open
- Reduces session hijacking risk
- Forces re-authentication for continued access

### Testing Results

- CDP disabled on router (global)
- CDP disabled on switch Guest port
- Exec timeout configured on all management lines
- All configurations saved to NVRAM
