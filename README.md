# Secure Enterprise Network Hardening Lab

> A comprehensive cybersecurity project demonstrating enterprise network security design, implementation, and hardening using Cisco technologies.

[![Project Status](https://img.shields.io/badge/Status-Complete-success)]()
[![Cisco Packet Tracer](https://img.shields.io/badge/Tool-Cisco%20Packet%20Tracer-blue)]()
[![Documentation](https://img.shields.io/badge/Documentation-Complete-brightgreen)]()

**Author:** John Wayne Landong  
**Duration:** February 2026 - March 2026  
**Type:** Personal Cybersecurity Lab

---

## Table of Contents

- [Overview](#overview)
- [Project Objectives](#project-objectives)
- [Network Architecture](#network-architecture)
- [Security Controls](#security-controls)
- [Key Features](#key-features)
- [Technical Skills Demonstrated](#technical-skills-demonstrated)
- [Project Structure](#project-structure)
- [Documentation](#documentation)
- [Testing & Validation](#testing--validation)
- [Certifications](#certifications)
- [How to Use This Repository](#how-to-use-this-repository)
- [Key Takeaways](#key-takeaways)
- [Future Enhancements](#future-enhancements)
- [Contact](#contact)

---

## Overview

This project demonstrates the **end-to-end design and implementation** of a secure enterprise network infrastructure. Over four weeks, I built a comprehensive security architecture from the ground up, implementing **defense-in-depth principles** across network segmentation, access control, device hardening, and policy documentation.

### Enterprise Scenario

Simulated mid-sized enterprise network with:

- **5 Departments:** IT, HR, Finance, Operations, Guest Network
- **Security Challenge:** Poor segmentation, weak access control, insecure device configurations
- **Solution:** Multi-layered security architecture with VLAN segmentation, ACL enforcement, and hardened infrastructure

---

## Project Objectives

1. **Eliminate flat network vulnerabilities** through VLAN segmentation
2. **Enforce least-privilege access** using Access Control Lists (ACLs)
3. **Harden infrastructure devices** with strong authentication and encryption
4. **Enable secure management** via SSH and access restrictions
5. **Document security controls** in formal policy framework
6. **Validate implementation** through comprehensive testing

---

## Network Architecture

### Topology

```
                                     R1-Core (4331 Router)
                                     [GigabitEthernet0/0/0]
                                               |
                                        [802.1Q Trunk]
                                               |
                                     SW1-Core (2960 Switch)
                                      [GigabitEthernet0/1]
                                               |
        ┌──────────────────┼───────────────────┼───────────────────┼──────────────────┐
        |                  |                   |                   |                  |
    [Fa0/1]             [Fa0/2]             [Fa0/3]             [Fa0/4]            [Fa0/5]
    VLAN 10             VLAN 20             VLAN 30             VLAN 40            VLAN 99
     PC-IT               PC-HR            PC-Finance          PC-Operations       PC-Guest

```

### VLAN Design

| VLAN | Department       | Subnet          | Security Level |
| ---- | ---------------- | --------------- | -------------- |
| 10   | IT/Network Admin | 192.168.10.0/24 | Privileged     |
| 20   | Human Resources  | 192.168.20.0/24 | Restricted     |
| 30   | Finance          | 192.168.30.0/24 | Restricted     |
| 40   | Operations       | 192.168.40.0/24 | Standard       |
| 99   | Guest Network    | 192.168.99.0/24 | Untrusted      |
| 999  | Blackhole        | N/A             | Disabled Ports |

---

## Security Controls

### Week 1: Network Segmentation

- ✓ 5 departmental VLANs implemented
- ✓ Router-on-a-Stick inter-VLAN routing
- ✓ 802.1Q trunking configuration
- ✓ 20 unused ports disabled and assigned to blackhole VLAN

### Week 2: Access Control & Least Privilege

- ✓ Guest network completely isolated from internal resources
- ✓ HR and Finance accessible only by IT department
- ✓ Extended ACLs enforcing department-level policies
- ✓ Default-deny security posture

### Week 3: Device & Network Hardening

- ✓ Strong password policy (12+ chars, Type 5 MD5 encryption)
- ✓ SSH v2 enabled with 2048-bit RSA keys
- ✓ Telnet disabled completely
- ✓ Management access restricted to IT VLAN only
- ✓ Login banners with legal warnings
- ✓ CDP and Proxy ARP disabled on untrusted interfaces
- ✓ 5-minute session timeout configured

### Week 4: Security Policy & Validation

- ✓ Formal Network Security Policy document
- ✓ 17 comprehensive security tests performed
- ✓ 100% configuration accuracy validated
- ✓ Complete technical documentation

---

## Key Features

### Defense-in-Depth Architecture

Multiple independent security layers:

1. **Network Segmentation** - VLAN isolation
2. **Access Control** - ACL traffic filtering
3. **Device Authentication** - Strong passwords + encryption
4. **Encrypted Management** - SSH v2 only
5. **Management Restrictions** - IT VLAN access only
6. **Attack Surface Reduction** - Disabled unnecessary services

### Access Control Matrix

| Source         | IT  | HR  | Finance | Ops | Guest |
| -------------- | --- | --- | ------- | --- | ----- |
| **IT**         | ✓   | ✓   | ✓       | ✓   | ✓     |
| **HR**         | ✓   | ✓   | ✗       | ✓   | ✗     |
| **Finance**    | ✓   | ✗   | ✓       | ✓   | ✗     |
| **Operations** | ✓   | ✗   | ✗       | ✓   | ✗     |
| **Guest**      | ✗   | ✗   | ✗       | ✗   | ✗     |

### Production-Ready Configurations

- All configurations syntactically correct
- Follows Cisco IOS best practices
- Aligned with CIS Benchmarks
- Ready for physical hardware deployment

---

## Technical Skills Demonstrated

### Networking

- VLAN design and implementation
- Router-on-a-Stick configuration
- 802.1Q trunking
- Inter-VLAN routing
- IP addressing and subnetting

### Security

- Extended Access Control Lists (ACLs)
- Least-privilege access design
- Device hardening techniques
- SSH configuration and encryption
- Password policy implementation
- Attack surface reduction

### Cisco IOS

- Router configuration (Cisco 4331)
- Switch configuration (Cisco 2960)
- CLI navigation and troubleshooting
- Show commands and verification
- Configuration backup and management

### Professional Skills

- Security policy writing
- Technical documentation
- Test case development
- Project management
- Git version control
- Markdown proficiency

---

## Project Structure

```
secure-enterprise-network-lab/
│
├── packet-tracer-files/
│   ├── week1_baseline.pkt          # Flat network (before)
│   ├── week1_segmented.pkt         # VLAN segmentation
│   ├── week2_acl_hardened.pkt      # Access control
│   ├── week3_device_hardened.pkt   # Device hardening
│   └── final_secure_network.pkt    # Complete secure network
│
├── docs/
│   ├── Week1.md                    # Segmentation documentation
│   ├── Week2.md                    # Access control documentation
│   ├── Week3.md                    # Hardening documentation
│   ├── SECURITY_POLICY.md          # Formal security policy
│   ├── Testing_Results.md          # 17 test cases with evidence
│   └── Final_Report.md             # Comprehensive project report
│
├── screenshots/
│   ├── week1/  (10 screenshots)
│   ├── week2/  (7 screenshots)
│   ├── week3/  (21 screenshots)
│   └── week4/  (17 screenshots)
│
├── .gitignore
├── LICENSE
└── README.md
```

**Total Deliverables:**

- 5 Packet Tracer network files
- 6 comprehensive documentation files
- 55 verification screenshots
- 40+ Git commits with clear history
- 3000+ lines of professional documentation

---

## Documentation

### Core Documents

| Document                                      | Description                                    |
| --------------------------------------------- | ---------------------------------------------- |
| [Week1.md](docs/Week1.md)                     | Network architecture and VLAN segmentation     |
| [Week2.md](docs/Week2.md)                     | Access control policies and ACL implementation |
| [Week3.md](docs/Week3.md)                     | Device hardening and secure management         |
| [SECURITY_POLICY.md](docs/SECURITY_POLICY.md) | Formal network security policy (15 sections)   |
| [Testing_Results.md](docs/Testing_Results.md) | Comprehensive testing with 17 test cases       |
| [Final_Report.md](docs/Final_Report.md)       | Complete project report and analysis           |

### Documentation Highlights

- **Professional formatting** with clear structure
- **Evidence-based** with screenshot verification
- **Technical depth** with configuration examples
- **Compliance mapping** to industry frameworks
- **Limitations documented** with mitigation strategies

---

## Testing & Validation

### Testing Scope

- **17 comprehensive test cases** covering all security controls
- **100% configuration accuracy** validated
- **Evidence-based approach** with screenshot documentation

### Test Categories

1. **Network Segmentation** (4 tests) - VLAN configuration and routing
2. **Access Control** (4 tests) - ACL enforcement and isolation
3. **Device Authentication** (3 tests) - Password encryption and SSH
4. **Management Access** (4 tests) - Access restrictions and banners
5. **Service Hardening** (2 tests) - CDP and Proxy ARP

### Results

✓ All configurations validated as syntactically correct  
✓ All controls aligned with security policy  
✓ Production-ready for physical Cisco hardware  
! 5 Packet Tracer simulator limitations documented

---

## Certifications

This project applies knowledge from:

### IBM - IT Fundamentals for Cybersecurity Specialization (January 2026)

- Introduction to Cybersecurity Tools & Cyberattacks
- Operating Systems: Overview, Administration, and Security
- Cybersecurity Compliance Framework, Standards & Regulations
- Computer Networks and Network Security

### Cisco

- **Networking Basics** (January 2026)
- **Introduction to Cybersecurity** (December 2025)

---

## How to Use This Repository

### For Recruiters/Employers

1. Review [Final_Report.md](docs/Final_Report.md) for project overview
2. Check [SECURITY_POLICY.md](docs/SECURITY_POLICY.md) for policy writing skills
3. Examine [Testing_Results.md](docs/Testing_Results.md) for validation methodology
4. Browse weekly documentation for technical depth

### For Learning/Reference

1. Clone the repository
2. Open `.pkt` files in Cisco Packet Tracer
3. Follow weekly documentation for step-by-step implementation
4. Review screenshots for configuration verification
5. Use as template for similar projects

### For Technical Review

1. Examine configurations in Packet Tracer files
2. Verify ACL logic and placement
3. Review device hardening commands
4. Validate against Cisco IOS best practices

---

## Key Takeaways

### Security Principles Applied

- **Defense-in-Depth:** Multiple independent security layers
- **Least Privilege:** Minimum access required for job function
- **Secure by Default:** Default-deny policies with explicit permits
- **Separation of Duties:** Management vs. user access segregation

### Professional Skills Developed

- Enterprise network security architecture
- Cisco IOS configuration and troubleshooting
- Security policy documentation
- Testing and validation methodology
- Git-based project management

### Compliance Alignment

- CIS Cisco IOS Benchmarks
- NIST Cybersecurity Framework
- PCI-DSS requirements
- SOC 2 security controls

---

## Future Enhancements

### Short-Term

- [ ] Add Voice VLAN for IP phones
- [ ] Implement Server VLAN for internal services
- [ ] Enable ACL logging for security events
- [ ] Add time-based ACL restrictions

### Advanced Features

- [ ] 802.1X port-based authentication
- [ ] DHCP snooping and Dynamic ARP Inspection
- [ ] Port security with MAC address limiting
- [ ] SNMP monitoring configuration
- [ ] Syslog server integration

### Physical Deployment

- [ ] Migrate to physical Cisco hardware
- [ ] Implement redundancy (HSRP/VRRP)
- [ ] Add wireless infrastructure
- [ ] Integrate firewall and WAN connectivity

---

## Contact

**John Wayne Landong**

- Email: johnwaynelandong@gmail.com
- LinkedIn: https://www.linkedin.com/in/johnwaynelandong
- GitHub: https://github.com/waeijn
- Portfolio: https://johnwaynelandong.vercel.app

---

## License

This project is created for educational and portfolio purposes.

---

## Acknowledgments

- **Cisco Networking Academy** for Packet Tracer
- **IBM** and **Cisco** for certification training
- **Anthropic** for Claude AI assistance in learning
- **GitHub** for version control and hosting

---

## Project Stats

![Lines of Config](https://img.shields.io/badge/Config%20Lines-200%2B-blue)
![Documentation](https://img.shields.io/badge/Documentation-3000%2B%20lines-green)
![Screenshots](https://img.shields.io/badge/Screenshots-55-orange)
![Test Cases](https://img.shields.io/badge/Test%20Cases-17-red)
![Commits](https://img.shields.io/badge/Commits-40%2B-purple)

---

<div align="center">

**If you found this project helpful, please consider giving it a star!**

_Built with passion for cybersecurity and network engineering_

</div>
