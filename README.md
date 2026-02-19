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

**Task 1:** Understand Active Directory Architecture

**Goal:** Understand what Active Directory is and how it enables centralized identity and access management.

**Explanation:**  
Active Directory (AD) is a directory service used by organizations to centrally manage users, computers, permissions, and authentication.  
Key components include:

- **Domain:** Logical boundary for users and computers  
- **Domain Controller (DC):** Server that stores and enforces AD data  
- **Forest:** Top-level AD structure containing one or more domains  
- **LDAP:** Protocol used to query Active Directory  
- **Kerberos:** Default authentication protocol  

**Actions Performed:**  
- Logged into Windows Server 2025 Domain Controller hosted in Microsoft Azure  
- Opened **Server Manager** and reviewed installed roles  
- Verified **Active Directory Domain Services (AD DS)** role was installed and operational

**Task 2:** Explore Active Directory Users & Computers (ADUC)

**Goal:** Learn how users, groups, and computers are organized in Active Directory.

**Explanation:**  
Active Directory Users and Computers (ADUC) is the primary administrative tool used to manage AD objects such as:

- User accounts  
- Computer accounts  
- Security groups  
- Organizational Units (OUs)  

**Actions Performed:**  
- Opened ADUC using **dsa.msc**  
- Explored default containers:
  - Users
  - Computers
  - Domain Controllers  
- Reviewed built-in groups including:
  - Domain Admins
  - Domain Users

**Task 3:** Create and Manage User Accounts

**Goal:** Create and manage domain user accounts.

**Explanation:**  
User accounts in Active Directory represent identities used for authentication and authorization across the domain environment.

**Actions Performed:**  
- Created a new domain user:
  - Username: ad_user1  
- Configured password and account settings

**Task 4:** Understand Groups and Group Scope

**Goal:** Learn how group-based access control works in Active Directory.

**Explanation:**  
Groups simplify permission management by allowing administrators to assign access rights to multiple users at once instead of configuring permissions individually.

**Group Types:**
- **Security Groups:** Used to assign permissions to resources
- **Distribution Groups:** Used for email distribution only

**Group Scopes:**
- **Domain Local:** Permissions within a specific domain
- **Global:** Members from the same domain
- **Universal:** Members across multiple domains

**Actions Performed:**  
- Created a Security Group named **IT_Support** in Active Directory Users and Computers (ADUC)  
- Added **ad_user1** as a member of the IT_Support group  
- Configured folder permissions and assigned access using group-based security permissions
- Enabled and disabled the user account

 
