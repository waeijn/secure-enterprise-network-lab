# Secure Enterprise Network Hardening Lab (Cisco Packet Tracer)

## Overview

This project is a month-long, hands-on cybersecurity lab focused on designing, implementing, and hardening a simulated **enterprise network** using **Cisco Packet Tracer**. The lab emphasizes secure network architecture, access control, device hardening, and policy-driven security controls.

The project is structured to be **resume-safe, realistic, and interview-ready**, with clear weekly deliverables, attack–defense scenarios, and professional documentation hosted on GitHub.

## Project Progress

- [x] Week 1: Secure Network Architecture & Segmentation
- [ ] Week 2: Access Control & Least Privilege
- [ ] Week 3: Device & Network Hardening
- [ ] Week 4: Security Policies & Final Review

---

## Duration & Commitment

- **Length:** 4 weeks
- **Time:** ~12 hours per week (≈48 hours total)

---

## Tools & Technologies

- Cisco Packet Tracer
- Cisco IOS (routers & switches)
- GitHub (version control & documentation)

---

## Certifications Aligned

This project reinforces and applies concepts from:

- **IBM – IT Fundamentals for Cybersecurity Specialization**
  - Network security
  - Operating system & infrastructure security
  - Compliance-aware security controls
- **Cisco – Networking Basics**
- **Cisco – Introduction to Cybersecurity**

---

## Enterprise Scenario

You are tasked with securing a **mid-sized enterprise network** composed of multiple departments after reports of poor segmentation, weak access control, and insecure device configurations.

### Departments

- IT / Network Administration
- Human Resources
- Finance
- Operations
- Guest Network (untrusted)

---

## Core Objectives

- Design a secure enterprise network architecture
- Apply **defense-in-depth** principles
- Enforce **least privilege** through segmentation and ACLs
- Harden routers and switches
- Isolate management and sensitive resources
- Document security decisions clearly and professionally

---

## Weekly Breakdown

### Week 1 – Secure Network Architecture & Segmentation

**Focus:** Eliminating flat networks

**Key Tasks**

- Design enterprise topology
- Create VLANs per department
- Implement trunking and access ports
- Configure inter-VLAN routing
- Disable unused switch ports

**Security Problem**

- Flat network allows unrestricted lateral movement

**Security Controls**

- VLAN segmentation
- Proper port configuration

**Deliverables**

- Baseline and segmented `.pkt` files
- VLAN and trunk configuration screenshots
- `Week1.md` explanation

---

### Week 2 – Access Control & Least Privilege

**Focus:** Controlling traffic flow

**Key Tasks**

- Design inter-department access policy
- Implement standard and extended ACLs
- Restrict access to Finance and HR
- Isolate Guest network

**Security Problem**

- Unauthorized access between departments

**Security Controls**

- Extended ACLs
- Proper ACL placement

**Deliverables**

- Before/after connectivity tests
- ACL configuration screenshots
- `Week2.md` explanation

---

### Week 3 – Device & Network Hardening

**Focus:** Securing infrastructure devices

**Key Tasks**

- Configure strong passwords
- Enable SSH and disable Telnet
- Apply login banners
- Encrypt passwords
- Restrict device management to IT VLAN
- Disable unused services and interfaces

**Security Problem**

- Weak device authentication and open management access

**Security Controls**

- Secure management plane
- Hardened device configurations

**Deliverables**

- Hardened config snippets
- Access attempt screenshots
- `Week3.md` explanation

---

### Week 4 – Security Policies & Final Review

**Focus:** Policy-driven security and validation

**Key Tasks**

- Write a Network Security Policy
- Map technical controls to policy rules
- Perform full network testing
- Validate allowed vs denied traffic
- Final cleanup and review

**Deliverables**

- Final hardened `.pkt` file
- `SECURITY_POLICY.md`
- `Final_Report.md`

---

## Repository Structure

secure-enterprise-network-lab/

│

├── packet-tracer-files/

│ ├── week1_baseline.pkt

│ ├── week1_segmented.pkt

│ ├── week2_acl_hardened.pkt

│ └── final_secure_network.pkt

│

├── docs/

│ ├── Week1.md

│ ├── Week2.md

│ ├── Week3.md

│ ├── SECURITY_POLICY.md

│ └── Final_Report.md

│

├── screenshots/

│ ├── week1/

│ ├── week2/

│ └── week3/

│

└── README.md

---

## Skills Demonstrated

- Enterprise network design
- Network segmentation & VLAN planning
- Access control using ACLs
- Secure router and switch configuration
- Defense-in-depth implementation
- Security documentation and policy writing

---

## How to Use This Repository

1. Open the Packet Tracer files week by week
2. Follow the documentation in the `docs/` folder
3. Review screenshots for verification
4. Use commit history to track progress and learning

---

## Notes

This project is intentionally designed to mirror real-world enterprise security work while staying within Cisco Packet Tracer’s capabilities. It prioritizes clarity, correctness, and professional documentation over gimmicks.

---

## Author

**Waeijn**  
Computer Science Student | Aspiring Software & Cybersecurity Engineer
