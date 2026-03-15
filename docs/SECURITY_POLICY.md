# Network Security Policy

## Enterprise Network Infrastructure

**Document Version:** 1.0  
**Effective Date:** March 2026  
**Last Updated:** March 15, 2026  
**Document Owner:** John Wayne Landong  
**Classification:** Internal Use Only

---

## 1. Purpose

This Network Security Policy establishes the security requirements,
standards, and procedures for the enterprise network infrastructure
to protect organizational assets, ensure data confidentiality and
integrity, and maintain network availability.

### 1.1 Objectives

- Protect sensitive data through network segmentation
- Prevent unauthorized access to network resources
- Ensure secure management of network devices
- Maintain audit trails for security events
- Comply with industry security standards

---

## 2. Scope

### 2.1 Applicability

This policy applies to:

- All network infrastructure devices (routers, switches)
- All network segments and VLANs
- All personnel with network access privileges
- All systems connected to the enterprise network
- Remote access connections

### 2.2 Covered Departments

- IT / Network Administration (VLAN 10)
- Human Resources (VLAN 20)
- Finance (VLAN 30)
- Operations (VLAN 40)
- Guest Network (VLAN 99)

---

## 3. Policy Principles

### 3.1 Defense in Depth

Multiple layers of security controls shall be implemented:

- Network segmentation (Layer 2)
- Access control lists (Layer 3)
- Device authentication (Management plane)
- Encrypted communications (Data plane)
- Service hardening (Attack surface reduction)

### 3.2 Least Privilege

Users and systems shall have only the minimum access required
to perform authorized job functions. Default deny policies
shall be applied with explicit permit exceptions.

### 3.3 Separation of Duties

Network administration functions shall be restricted to authorized
IT personnel. End users shall not have access to network
infrastructure management interfaces.

---

## 4. Network Segmentation Policy

### 4.1 VLAN Requirements

**Requirement:** All departments shall be isolated into separate VLANs.

**Technical Implementation:**

- IT Department: VLAN 10 (192.168.10.0/24)
- Human Resources: VLAN 20 (192.168.20.0/24)
- Finance: VLAN 30 (192.168.30.0/24)
- Operations: VLAN 40 (192.168.40.0/24)
- Guest Network: VLAN 99 (192.168.99.0/24)

**Rationale:** Prevents lateral movement and limits blast radius
of security incidents.

### 4.2 Inter-VLAN Routing

**Requirement:** Traffic between VLANs shall be routed and subject
to access control enforcement.

**Technical Implementation:**

- Router-on-a-Stick configuration
- Subinterfaces for each VLAN
- All inter-VLAN traffic passes through router

**Rationale:** Creates enforcement point for access control policies.

### 4.3 Unused Ports

**Requirement:** All unused switch ports shall be disabled and
assigned to a blackhole VLAN.

**Technical Implementation:**

- Unused ports: administratively shutdown
- Assignment: VLAN 999 (blackhole)
- Total secured: 20 unused ports

**Rationale:** Prevents rogue device connections and unauthorized
network access.

---

## 5. Access Control Policy

### 5.1 Guest Network Isolation

**Requirement:** Guest network shall have no access to internal
corporate resources.

**Technical Implementation:**

- ACL: GUEST_ISOLATION
- Denies: All traffic from VLAN 99 to VLANs 10, 20, 30, 40
- Applied: Outbound on Guest subinterface

**Rationale:** Untrusted devices (visitors, contractors) must not
access sensitive corporate data or systems.

### 5.2 Sensitive Department Protection

**Requirement:** HR and Finance departments shall be accessible
only by IT for support purposes.

**Technical Implementation:**

- ACL: PROTECT_HR (protects VLAN 20)
- ACL: PROTECT_FINANCE (protects VLAN 30)
- Permits: IT VLAN (192.168.10.0/24)
- Denies: All other networks
- Applied: Inbound on HR and Finance subinterfaces

**Rationale:** HR contains PII and payroll data. Finance contains
financial records and payment systems. Both require strict access
control for compliance and data protection.

### 5.3 Default Deny

**Requirement:** All ACLs shall implement default deny with
explicit permit rules.

**Technical Implementation:**

- Explicit deny rules for blocked traffic
- Explicit permit rule at end for allowed traffic
- Implicit deny at end of all ACLs

**Rationale:** Prevents accidental exposure through misconfiguration.

---

## 6. Device Authentication Policy

### 6.1 Password Requirements

**Requirement:** All network devices shall use strong passwords
meeting complexity requirements.

**Standards:**

- Minimum length: 12 characters
- Complexity: Uppercase, lowercase, numbers, special characters
- No dictionary words or common patterns
- Different passwords for different access methods

**Technical Implementation:**

- Enable secret: Cisco@2026!Secure (Type 5 MD5)
- Console password: Console@2026! (Type 7)
- VTY password: VTY@2026!Remote (Type 7)
- Service password-encryption: Enabled

**Rationale:** Weak passwords are the primary attack vector for
device compromise. Strong passwords prevent brute force and
dictionary attacks.

### 6.2 Password Encryption

**Requirement:** All passwords shall be encrypted in device
configurations.

**Technical Implementation:**

- Enable secret: Type 5 (MD5 hash)
- Line passwords: Type 7 (Cisco encryption)
- Service password-encryption: Enabled globally

**Rationale:** Prevents credential theft through configuration
file access or shoulder surfing.

### 6.3 User Accounts

**Requirement:** Individual user accounts shall be created for
administrative access with appropriate privilege levels.

**Technical Implementation:**

- Username: admin
- Privilege level: 15 (full access)
- Password: Admin@2026!SSH (Type 5)

**Rationale:** Individual accounts provide accountability and
audit trails for administrative actions.

---

## 7. Encrypted Management Policy

### 7.1 SSH Requirement

**Requirement:** All remote management access shall use SSH
version 2 with strong encryption.

**Technical Implementation:**

- Protocol: SSH version 2
- Key strength: 2048-bit RSA
- Telnet: Disabled (transport input ssh only)
- Session timeout: 60 seconds
- Authentication retries: 3 attempts

**Rationale:** SSH encrypts all traffic including credentials.
Telnet is insecure and transmits passwords in plaintext.

### 7.2 Telnet Prohibition

**Requirement:** Telnet shall be disabled on all network devices.

**Technical Implementation:**

- VTY lines: transport input ssh
- Telnet connections: Rejected

**Rationale:** Telnet has no encryption and is vulnerable to
credential theft through packet sniffing.

---

## 8. Management Access Control Policy

### 8.1 Administrative Access Restriction

**Requirement:** Network device management shall be restricted
to IT department personnel only.

**Technical Implementation:**

- ACL: MGMT_ACCESS (Standard ACL)
- Permits: IT VLAN (192.168.10.0/24)
- Denies: All other networks
- Applied: access-class on VTY lines

**Rationale:** Limits attack surface by preventing management
access from compromised user VLANs or Guest network.

### 8.2 Login Banners

**Requirement:** All devices shall display legal warning banners
before authentication.

**Technical Implementation:**

- MOTD banner: Unauthorized access warning
- Login banner: Authorized personnel only

**Rationale:** Provides legal protection, establishes authorized
use policy, and warns of monitoring.

### 8.3 Session Timeout

**Requirement:** Inactive management sessions shall automatically
disconnect after 5 minutes.

**Technical Implementation:**

- Console line: exec-timeout 5 0
- VTY lines: exec-timeout 5 0

**Rationale:** Prevents abandoned sessions from remaining open
and vulnerable to session hijacking.

---

## 9. Attack Surface Reduction Policy

### 9.1 Information Disclosure Prevention

**Requirement:** Network devices shall not disclose topology or
version information to untrusted networks.

**Technical Implementation:**

- Router: CDP disabled globally (no cdp run)
- Switch: CDP disabled on Guest port (Fa0/5)

**Rationale:** CDP broadcasts device information useful for
reconnaissance. Disable on untrusted interfaces.

### 9.2 Unnecessary Service Disable

**Requirement:** All unnecessary services shall be disabled to
reduce attack surface.

**Technical Implementation:**

- Proxy ARP: Disabled on all subinterfaces

**Rationale:** Each running service is a potential attack vector.
Disable services not required for operation.

---

## 10. Roles and Responsibilities

### 10.1 Network Administrator

**Responsibilities:**

- Implement and maintain security controls
- Monitor security events and logs
- Respond to security incidents
- Perform regular security audits
- Update security configurations

**Authority:**

- Full access to all network devices
- Modify security policies as needed
- Grant/revoke user access

### 10.2 IT Support Staff

**Responsibilities:**

- Support department connectivity issues
- Troubleshoot within assigned scope
- Report security concerns

**Authority:**

- Limited access to specific devices
- No policy modification authority

### 10.3 End Users

**Responsibilities:**

- Use network for authorized purposes only
- Report suspicious activity
- Comply with acceptable use policies

**Authority:**

- Access only to assigned department VLAN
- No access to network infrastructure

---

## 11. Compliance and Auditing

### 11.1 Compliance Frameworks

This policy aligns with:

- CIS Cisco IOS Benchmarks
- NIST Cybersecurity Framework
- PCI-DSS (where applicable)
- SOC 2 security controls

### 11.2 Audit Requirements

**Frequency:** Quarterly security audits

**Audit Items:**

- VLAN configuration review
- ACL effectiveness testing
- Password policy compliance
- Service configuration verification
- Access log review

### 11.3 Change Management

All network security changes require:

- Change request documentation
- Security impact assessment
- Testing in non-production environment
- Management approval
- Implementation documentation

---

## 12. Incident Response

### 12.1 Security Incident Definition

A security incident includes:

- Unauthorized access attempts
- Policy violations
- Device compromise
- Network anomalies

### 12.2 Response Procedures

1. Detect and verify incident
2. Contain the threat
3. Investigate root cause
4. Remediate vulnerabilities
5. Document lessons learned
6. Update policies as needed

---

## 13. Policy Review and Updates

### 13.1 Review Schedule

This policy shall be reviewed:

- Annually (minimum)
- After major network changes
- After security incidents
- When compliance requirements change

### 13.2 Update Process

1. Identify need for update
2. Draft proposed changes
3. Review with stakeholders
4. Approve changes
5. Communicate updates
6. Update version and date

---

## 14. Policy Violations

### 14.1 Violation Examples

- Bypassing security controls
- Sharing administrative credentials
- Connecting unauthorized devices
- Disabling security features
- Accessing restricted VLANs

### 14.2 Consequences

Violations may result in:

- Access revocation
- Disciplinary action
- Legal prosecution (where applicable)

---

## 15. Appendices

### Appendix A: Technical Control Mapping

| Policy Requirement     | Technical Control    | Verification Method          |
| ---------------------- | -------------------- | ---------------------------- |
| Network Segmentation   | VLANs 10,20,30,40,99 | show vlan brief              |
| Guest Isolation        | GUEST_ISOLATION ACL  | show access-lists            |
| HR Protection          | PROTECT_HR ACL       | show access-lists            |
| Finance Protection     | PROTECT_FINANCE ACL  | show access-lists            |
| Strong Passwords       | Enable secret Type 5 | show run \| include password |
| SSH Encryption         | SSH v2, 2048-bit RSA | show ip ssh                  |
| Telnet Disable         | transport input ssh  | show run \| section line vty |
| Management Restriction | MGMT_ACCESS ACL      | show access-lists            |
| Login Banners          | MOTD/Login banners   | SSH connection test          |
| Session Timeout        | exec-timeout 5 0     | show run \| section line     |
| CDP Disable            | no cdp run/enable    | show cdp                     |
| Proxy ARP Disable      | no ip proxy-arp      | show ip interface            |

### Appendix B: Document History

| Version | Date       | Author             | Changes                 |
| ------- | ---------- | ------------------ | ----------------------- |
| 1.0     | March 2026 | John Wayne Landong | Initial policy creation |

---

**Document Approval:**

**Note:** This is a personal project demonstrating policy documentation
skills. In production, this would require management approval.

Project Author: John Wayne Landong  
Date: March 15, 2026

---

**End of Network Security Policy**
