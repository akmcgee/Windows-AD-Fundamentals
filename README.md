# Active Directory Domain Administration Lab (Windows Server / Azure)
## Overview
This lab covers core Active Directory (AD) fundamentals by building and managing a real AD environment like it’s used in enterprise networks. Key focus areas include users/groups, OUs, authentication concepts (Kerberos), Group Policy, and basic AD security event review.

## Lab Goals
- Build familiarity with AD concepts and architecture (domain, DC, DNS)
- Manage identities (users, groups, computers)
- Organize resources using Organizational Units (OUs)
- Apply policies with Group Policy (GPO)
- Review AD-related security logs/events

## Environment

**Virtualization/Platform:** Azure
**Domain Controller:** Windows server 2025
**Client Machine(s):** Windows 10
**Network Type:** (NAT / Host-only / Internal / Azure VNet)  
**Domain Name:** corp.ashlab.local
**IP Scheme:** (DC IP, Client IPs, DNS settings)

## Tools Used
- Server Manager
- Active Directory Users and Computers (ADUC / dsa.msc)
- Group Policy Management (gpmc.msc)
- Event Viewer (eventvwr.msc)
- Command line utilities (ipconfig, nslookup, gpupdate, whoami, etc.)
