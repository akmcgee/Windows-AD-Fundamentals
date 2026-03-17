# 🏢 Active Directory Enterprise Lab — Azure Deployment

![Lab Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![Azure](https://img.shields.io/badge/Platform-Microsoft%20Azure-0078D4)
![Windows Server](https://img.shields.io/badge/OS-Windows%20Server%202025-blue)
![Active Directory](https://img.shields.io/badge/Service-Active%20Directory-lightblue)
![Windows](https://img.shields.io/badge/Client-Windows%2010-lightgrey)

A hands-on enterprise Active Directory deployment and administration lab hosted in Microsoft Azure. Built to simulate real-world IT administration and SOC analyst tasks including identity management, Group Policy enforcement, Kerberos authentication monitoring, and Active Directory security log analysis.

---

## 📋 Table of Contents

- [Lab Overview](#lab-overview)
- [Environment & Architecture](#environment--architecture)
- [Tools & Technologies](#tools--technologies)
- [Lab Objectives](#lab-objectives)
- [Task 1 — Active Directory Architecture](#task-1--understand-active-directory-architecture)
- [Task 2 — Active Directory Users & Computers](#task-2--explore-active-directory-users--computers-aduc)
- [Task 3 — Create and Manage User Accounts](#task-3--create-and-manage-user-accounts)
- [Task 4 — Groups and Group Scope](#task-4--understand-groups-and-group-scope)
- [Task 5 — Organizational Units & Delegation](#task-5--organizational-units-ou--delegation)
- [Task 6 — Domain Authentication & Kerberos](#task-6--domain-authentication--kerberos-basics)
- [Task 7 — Group Policy Fundamentals](#task-7--group-policy-fundamentals)
- [Task 8 — AD Security Logs & Monitoring](#task-8--ad-security-logs--monitoring)
- [Skills Demonstrated](#skills-demonstrated)
- [Screenshots](#screenshots)

---

## 🧪 Lab Overview

This lab was designed to simulate enterprise-level IT administration and security monitoring by:

- Deploying a Windows Server 2025 Domain Controller in Microsoft Azure
- Configuring Active Directory Domain Services, DNS, and Group Policy
- Building an enterprise-style Organizational Unit structure with delegated control
- Managing domain users, groups, and Role-Based Access Control
- Enforcing password complexity policies through Group Policy Objects
- Analyzing Kerberos authentication and Active Directory security events
- Simulating tasks performed by IT support specialists, junior sysadmins, and entry-level SOC analysts

---

## 🖥️ Environment & Architecture

```
┌─────────────────────────────────────────────────────┐
│              AZURE LAB NETWORK                      │
│              Domain: corp.ashlab.local              │
│                                                     │
│  ┌─────────────────────────────────────────────┐   │
│  │         Windows Server 2025                  │   │
│  │         DC01 — 172.17.0.4                    │   │
│  │         Domain Controller                    │   │
│  │         AD DS + DNS + Group Policy           │   │
│  └──────────────────┬──────────────────────────┘   │
│                     │ Domain Join                   │
│                     │ Kerberos Auth                 │
│                     ▼                               │
│  ┌─────────────────────────────────────────────┐   │
│  │         Windows 10 Enterprise                │   │
│  │         Domain-Joined Client VM              │   │
│  │         DNS → 172.17.0.4                     │   │
│  └─────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

| Component | Details |
|---|---|
| Platform | Microsoft Azure Virtual Machines |
| Domain Controller | Windows Server 2025 (AD DS + DNS) |
| Client Machine | Windows 10 Enterprise (Domain-Joined) |
| Network Type | Azure Virtual Network (VNet) |
| Domain Name | corp.ashlab.local |
| DC IP Address | 172.17.0.4 (Private IP) |
| DNS | Client DNS pointed to Domain Controller |

---

## 🛠️ Tools & Technologies

| Category | Tool |
|---|---|
| Platform | Microsoft Azure |
| Domain Controller OS | Windows Server 2025 |
| Client OS | Windows 10 Enterprise |
| Directory Service | Active Directory Domain Services (AD DS) |
| Admin Tool | Active Directory Users & Computers (ADUC) |
| Policy Management | Group Policy Management Console (GPMC) |
| Authentication | Kerberos |
| Security Monitoring | Windows Event Viewer (Event IDs 4624 & 4768) |
| Commands Used | dsa.msc, gpmc.msc, eventvwr.msc, gpupdate /force, klist |

---

## 🎯 Lab Objectives

- Deploy Windows Server 2025 Domain Controller in Microsoft Azure
- Install and configure Active Directory Domain Services and DNS
- Explore and manage Active Directory Users & Computers (ADUC)
- Create and manage domain users, groups, and Organizational Units
- Configure Role-Based Access Control and NTFS permissions
- Delegate administrative control using the Delegation of Control Wizard
- Enforce password complexity policies through Group Policy Objects
- Analyze Kerberos authentication tickets using `klist`
- Monitor and analyze Windows Security Event logs for authentication activity

---

## Task 1 — Understand Active Directory Architecture

**Goal:** Understand what Active Directory is and how it enables centralized identity and access management.

**Key Components:**

| Component | Description |
|---|---|
| Domain | Logical boundary for users and computers |
| Domain Controller (DC) | Server that stores and enforces AD data |
| Forest | Top-level AD structure containing one or more domains |
| LDAP | Protocol used to query Active Directory |
| Kerberos | Default authentication protocol |

**Actions Performed:**
- Logged into Windows Server 2025 Domain Controller hosted in Microsoft Azure
- Opened Server Manager and reviewed installed roles
- Verified Active Directory Domain Services (AD DS) role was installed and operational

---

## Task 2 — Explore Active Directory Users & Computers (ADUC)

**Goal:** Learn how users, groups, and computers are organized in Active Directory.

**Explanation:**
Active Directory Users and Computers (ADUC) is the primary administrative tool used to manage AD objects including user accounts, computer accounts, security groups, and Organizational Units.

**Actions Performed:**
- Opened ADUC using `dsa.msc`
- Explored default containers:
  - Users
  - Computers
  - Domain Controllers
- Reviewed built-in groups including:
  - Domain Admins
  - Domain Users

---

## Task 3 — Create and Manage User Accounts

**Goal:** Create and manage domain user accounts.

**Explanation:**
User accounts in Active Directory represent identities used for authentication and authorization across the domain environment.

**Actions Performed:**
- Created new domain user:
  - Username: `ad_user1`
- Configured password and account settings
- Enabled and disabled the user account to simulate user lifecycle management

---

## Task 4 — Understand Groups and Group Scope

**Goal:** Learn how group-based access control works in Active Directory.

**Group Types:**

| Type | Purpose |
|---|---|
| Security Groups | Assign permissions to resources |
| Distribution Groups | Email distribution only |

**Group Scopes:**

| Scope | Description |
|---|---|
| Domain Local | Permissions within a specific domain |
| Global | Members from same domain, permissions anywhere |
| Universal | Members and permissions across domains |

**Actions Performed:**
- Created a Security Group named `IT_Support` in ADUC
- Added `ad_user1` as a member of the IT_Support group
- Configured folder permissions and assigned access using group-based security
- Enabled and disabled user account to practice lifecycle management

---

## Task 5 — Organizational Units (OU) & Delegation

**Goal:** Understand how enterprises logically organize Active Directory objects and apply delegated administrative permissions.

**Explanation:**
Organizational Units (OUs) are containers used to structure users, groups, and computers into logical departments. OUs allow administrators to organize identities by business function, apply Group Policy Objects, and delegate limited administrative control without granting full domain admin privileges.

**OU Structure Created:**
```
corp.ashlab.local
├── IT
│   └── ad_user1
├── HR
│   └── hr_user
└── Finance
    └── finance_user
```

**Actions Performed:**
- Created Organizational Units: HR, IT, Finance
- Moved domain user accounts into appropriate OUs
- Used the **Delegation of Control Wizard** to assign scoped permissions
- Delegated limited control to HR User on the HR OU:
  - Create, delete, and manage user accounts
  - Reset user passwords and force password change at next logon

---

## Task 6 — Domain Authentication & Kerberos Basics

**Goal:** Understand how users authenticate in Active Directory environments using Kerberos.

**Kerberos Authentication Flow:**
```
1. User logs into domain-joined system
         ↓
2. Domain Controller verifies credentials
         ↓
3. KDC issues Ticket Granting Ticket (TGT)
         ↓
4. TGT used to request Service Tickets
         ↓
5. Service Tickets grant access to network resources
```

**Security Note:** Kerberos authentication is commonly targeted in attacks such as Pass-the-Ticket and Kerberoasting — making monitoring of these events critical in SOC environments.

**Actions Performed:**
- Logged into the domain environment as a domain-authenticated user
- Opened Command Prompt with administrative privileges
- Executed `klist` to view active Kerberos tickets

**Findings:**

| Field | Value |
|---|---|
| Domain | CORP.ASHLAB.LOCAL |
| TGT Issued By | krbtgt/CORP.ASHLAB.LOCAL |
| Encryption Type | AES-256-CTS-HMAC-SHA1-96 |
| Ticket Flags | forwardable, renewable, initial |

---

## Task 7 — Group Policy Fundamentals

**Goal:** Understand how Group Policy enforces security configurations across a domain environment.

**Explanation:**
Group Policy Objects (GPOs) allow administrators to centrally manage security settings within Active Directory. Password policies are commonly enforced through GPOs to ensure users follow secure authentication practices and reduce the risk of weak credentials.

**Actions Performed:**
- Opened Group Policy Management Console using `gpmc.msc`
- Created a new GPO named **Password Policy**
- Configured password complexity settings:
```
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Account Policies
                └── Password Policy
```
- Linked GPO to `corp.ashlab.local` domain
- Verified Security Filtering set to **Authenticated Users**
- Ran `gpupdate /force` on the Windows 10 client to apply policy
- Validated enforcement by attempting a weak password change — **blocked by domain policy** ✅

---

## Task 8 — AD Security Logs & Monitoring

**Goal:** Identify Active Directory authentication events using Windows Security logs for monitoring and analysis.

**Explanation:**
Active Directory records authentication activity in the Windows Security log. Monitoring Event IDs such as 4624 and 4768 helps SOC analysts track successful logins and Kerberos ticket activity across the domain.

**Actions Performed:**
- Opened Event Viewer using `eventvwr.msc`
- Navigated to: `Windows Logs → Security`
- Applied log filter for Event IDs 4624 and 4768

### Event ID 4624 — Successful Logon:

| Field | Value |
|---|---|
| Event ID | 4624 |
| Username | azureadmin |
| Logon Type | 3 (Network Logon) |
| Logon Process | Kerberos |
| Domain | CORP.ASHLAB.LOCAL |

### Event ID 4768 — Kerberos TGT Request:

| Field | Value |
|---|---|
| Event ID | 4768 |
| Username | azureadmin |
| Service Name | krbtgt |
| Target Domain | CORP |
| Status | 0x0 (Success) |
| Encryption Type | 0x12 (AES) |
| KDC | DC01 |

**Result:** Successfully validated the full domain authentication workflow using Kerberos — from TGT request through successful network logon — confirming the domain environment was functioning correctly and authentication events were being logged as expected.

---

## 🧠 Skills Demonstrated

| Category | Skills |
|---|---|
| Active Directory | AD DS deployment, OU design, user/group management, ADUC |
| Group Policy | GPO creation, linking, enforcement, gpupdate, gpresult |
| Access Control | RBAC, NTFS permissions, Delegation of Control Wizard |
| Authentication | Kerberos TGT/TGS flow, klist, domain join, SSO |
| Security Monitoring | Event ID 4624 & 4768 analysis, Windows Security logs |
| Azure | VM deployment, VNet configuration, DNS setup |
| Troubleshooting | Domain join issues, GPO application, permission conflicts |
| Documentation | SOC-style findings, structured lab write-ups |

---

## 🔐 Key Concepts Covered

- Centralized Identity Management
- OU-Based Organizational Structure
- Delegated Administrative Permissions
- Group Policy Security Enforcement
- Kerberos Ticket Granting Process
- Active Directory Authentication Monitoring
- Enterprise Access Control Models

---

## 📸 Screenshots

> Add your Active Directory screenshots here

| Screenshot | Description |
|---|---|
| `azure_vms.png` | Azure VM deployment — DC01 and client VM |
| `aduc_overview.png` | Active Directory Users & Computers interface |
| `ou_structure.png` | Organizational Unit hierarchy |
| `delegation_wizard.png` | Delegation of Control Wizard configuration |
| `gpo_password.png` | Group Policy password complexity settings |
| `event_4624.png` | Event ID 4624 successful logon in Security log |
| `event_4768.png` | Event ID 4768 Kerberos TGT request |
| `klist_output.png` | klist command showing active Kerberos tickets |

---

## 🧾 Key Takeaway

This lab demonstrated how to deploy and administer a fully functional enterprise Active Directory environment in Microsoft Azure. By configuring AD DS, DNS, Group Policy, RBAC, Kerberos authentication, and then analyzing the resulting Windows Security logs — this project reflects the core responsibilities of both junior system administrators and entry-level SOC analysts working in Windows enterprise environments.

---

## 👩🏾‍💻 About

**Ashley McGee**
Aspiring SOC Analyst | A.S. in Information Technology / Cybersecurity (Expected December 2026)
Northeast Wisconsin Technical College | Green Bay, WI

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://linkedin.com/in/ashley-mcgee-972006367)

---

*This lab was completed as part of an ongoing series of hands-on cybersecurity projects.*
