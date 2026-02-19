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

**Virtualization/Platform:** Mircosoft Azure (Azure virtual machines)
**Domain Controller:** Windows server 2025 (AD DS + DNS installed)
**Client Machine(s):** Windows 10 Enterprise (Domain Joined)
**Network Type:** Azure Virtual Network (VNet)
*Domain Name:** corp.ashlab.local
**IP Scheme:**   Domain Controller (DC): 172.17.0.4 (Private IP)
Client VM: 172.17.0.5 (Private IP)
DNS Settings: Client DNS pointed to Domain Controller (172.17.0.4)
## Tools Used
- Server Manager
- Active Directory Users and Computers (ADUC / dsa.msc)
- Group Policy Management (gpmc.msc)
- Event Viewer (eventvwr.msc)
- Command line utilities (ipconfig, nslookup, gpupdate, whoami, dnsflush,etc.)
