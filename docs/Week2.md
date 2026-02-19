# Week 2: Access Control & Least Privilege

## Overview

Week 2 focuses on implementing traffic control policies using Access
Control Lists (ACLs) to enforce least-privilege access between departments.

## Security Problem

While Week 1 implemented VLAN segmentation, all departments can still
freely communicate through the router. This violates the principle of
least privilege and creates unnecessary risk exposure.

## Access Control Policy

### Business Requirements

| Source     | Allowed Access  | Denied Access              |
| ---------- | --------------- | -------------------------- |
| IT         | All departments | None                       |
| HR         | IT only         | Finance, Operations, Guest |
| Finance    | IT only         | HR, Operations, Guest      |
| Operations | IT only         | HR, Finance, Guest         |
| Guest      | None            | All internal departments   |

### Security Principles Applied

- **Deny by default**: Block all traffic, explicitly permit only what's needed
- **Least privilege**: Minimum access required for job functions
- **Data sensitivity**: Finance and HR are highly restricted
- **Guest isolation**: Untrusted network has zero internal access

## Pre-ACL Testing

Verified that Guest network can currently reach all internal departments,
confirming the security gap that ACLs will address.
