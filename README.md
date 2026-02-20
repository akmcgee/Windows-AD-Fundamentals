 🧪 Active Directory Enterprise Lab – Azure Deployment

## 📌 Overview

This project demonstrates the deployment, administration, and security monitoring of a Windows Active Directory environment hosted in Microsoft Azure.  
The lab focuses on identity management, organizational structure, delegated administration, Group Policy enforcement, and Kerberos-based domain authentication with real-world security logging analysis.

The goal of this project was to simulate enterprise-level administration and security tasks performed by IT support specialists, junior system administrators, and entry-level SOC analysts while reinforcing security-focused Active Directory concepts.

---

🏗️ Lab Environment

**Virtualization/Platform:** Microsoft Azure (Azure Virtual Machines)  
**Domain Controller:** Windows Server 2025 (AD DS + DNS installed)  
**Client Machine(s):** Windows 10 Enterprise (Domain Joined)  
**Network Type:** Azure Virtual Network (VNet)  
**Domain Name:** corp.ashlab.local  

**IP Scheme:**

- Domain Controller (DC01): 172.17.0.4 (Private IP)  
- Client VM: Domain-joined Windows 10  
- DNS Settings: Client DNS pointed to Domain Controller  

---

🎯 Skills Demonstrated

- Active Directory Domain Services (AD DS) Administration  
- Organizational Unit (OU) Design & Delegation of Control  
- Role-Based Access Control (RBAC)  
- NTFS Permission Management  
- Group Policy Management & Password Policy Enforcement  
- Active Directory Security Log Analysis (Event IDs 4624 & 4768)  
- Kerberos Authentication Monitoring  
- Azure Infrastructure Deployment  
- Domain User Lifecycle Management  
- Troubleshooting Domain Join & Identity Issues  

---

🔐 Key Concepts Covered

- Centralized Identity Management  
- OU-Based Organizational Structure  
- Delegated Administrative Permissions  
- Group Policy Security Enforcement  
- Kerberos Ticket Granting Process  
- Active Directory Authentication Monitoring  
- Enterprise Access Control Models  

## 🔐 Key Concepts Covered

- Centralized Identity Management
- OU-Based Organizational Structure
- Delegated Administrative Permissions
- Kerberos Ticket Granting Process
- Enterprise Access Control Models

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

**Actions Performed:**  
- Created a Security Group named **IT_Support** in Active Directory Users and Computers (ADUC)  
- Added **ad_user1** as a member of the IT_Support group  
- Configured folder permissions and assigned access using group-based security permissions
- Enabled and disabled the user account

 **Task 5:** Organizational Units (OU) & Delegation

**Goal:** Understand how enterprises logically organize Active Directory objects and apply delegated administrative permissions.

**Explanation:**  
Organizational Units (OUs) are containers used in Active Directory to structure users, groups, and computers into logical departments. OUs allow administrators to:

- Organize identities by business function
- Apply Group Policy Objects (GPOs)
- Delegate limited administrative control without granting full domain admin privileges

**Actions Performed:**  
- Created Organizational Units:
  - HR
  - IT
  - Finance
- Moved domain user accounts into appropriate OUs:
  - AD User → IT OU
  - HR User → HR OU
  - Finance User → Finance OU
- Used the **Delegation of Control Wizard** in Active Directory Users and Computers to assign scoped administrative permissions
- Delegated limited control to HR User on the HR OU:
  - Create, delete, and manage user accounts
  - Reset user passwords and force password change at next logon

 **Task 6:** Domain Authentication & Kerberos Basics

**Goal:** Understand how users authenticate in Active Directory environments using Kerberos.

**Explanation:**  
Active Directory uses the Kerberos authentication protocol to securely verify identities.  
During authentication:

- A user logs into a domain-joined system
- The Domain Controller verifies credentials
- A Ticket Granting Ticket (TGT) is issued
- Service tickets are used to access network resources

Kerberos authentication is commonly targeted in cybersecurity attacks such as Pass-the-Ticket and Kerberoasting.

**Actions Performed:**  
- Logged into the domain environment as a domain-authenticated user
- Opened Command Prompt with administrative privileges
- Executed the following command:

- Observed active Kerberos tickets issued by the Domain Controller

**Findings:**  
- Verified Kerberos authentication to domain **CORP.ASHLAB.LOCAL**
- Confirmed Ticket Granting Ticket (TGT) issued by **krbtgt/CORP.ASHLAB.LOCAL**
- Encryption type observed: AES-256-CTS-HMAC-SHA1-96
- Ticket flags included:
  - forwardable
  - renewable
  - initial
  - 
  **Task 7:** Group Policy Fundamentals

**Goal:** Understand how Group Policy enforces security configurations across a domain environment.

**Explanation:**  
Group Policy Objects (GPOs) allow administrators to centrally manage security settings within Active Directory. Password policies are commonly enforced through GPOs to ensure users follow secure authentication practices and to reduce the risk of weak credentials.

**Actions Performed:**  
- Opened Group Policy Management Console using **gpmc.msc**  
- Created a new Group Policy Object named **Password Policy**  
- Configured password complexity under:
  - Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Password Policy  
- Linked the GPO to the **corp.ashlab.local** domain  
- Verified Security Filtering set to **Authenticated Users**  
- Ran **gpupdate /force** on the Windows 10 domain-joined client  
- Validated enforcement by attempting a weak password change which was blocked by domain policy


---

**Task 8:** AD Security Logs & Monitoring

**Goal:** Identify Active Directory authentication events using Windows Security logs for monitoring and analysis.

**Explanation:**  
Active Directory records authentication activity within the Windows Security log. Monitoring Event IDs such as 4624 and 4768 helps administrators and SOC analysts track successful logins and Kerberos ticket activity across the domain.

**Actions Performed:**  
- Opened Event Viewer using **eventvwr.msc**  
- Navigated to:
  - Windows Logs → Security  
- Applied log filter for Event IDs:
  - 4624 (Successful Login)
  - 4768 (Kerberos TGT Request)  
- Reviewed authentication details from Event ID 4624:
  - Username: **azureadmin**
  - Logon Type: **3 (Network Logon)**
  - Logon Process: **Kerberos**
  - Domain: **CORP.ASHLAB.LOCAL**  
- Reviewed Kerberos ticket request from Event ID 4768:
  - Username: **azureadmin**
  - Service Name: **krbtgt**
  - Target Domain: **CORP**
  - Status: **0x0 (Success)**
  - Ticket Encryption Type: **0x12 (AES)**  
  - pre_authent
- KDC (Key Distribution Center) identified as **DC01**
- Successful validation of domain authentication workflow using Kerberos
