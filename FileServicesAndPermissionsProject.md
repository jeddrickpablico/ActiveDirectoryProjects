# 📁 Windows File Services & Permission Management Project

## 🎯 Objectives
The primary objective of this project is to provision, secure, and manage centralized network storage using **Windows File Services**, strict **NTFS/Share Permissions**, and **File Server Resource Manager (FSRM)**.

This activity covers the following deployment milestones based on our network setup:
* Understanding the architectural differences between NTFS and Shared permissions, inheritance, and network access methods.
* Establishing foundational network shares and deploying them to client machines.
* Installing and configuring FSRM to implement storage Quotas and File Screening to restrict unauthorized media.
* Understanding and applying the critical architectural differences between NTFS and Shared permissions.
* Managing advanced permission inheritance to secure confidential departmental data.
* Enabling Access-Based Enumeration (ABE) to securely hide restricted resources from unauthorized users.

---

## ⚙️ Prerequisites & Server Preparation
Ensure your Windows Server environment is running and promoted to a Domain Controller. You must have client endpoints connected to the domain and pre-configured user accounts belonging to specific departmental Security Groups and knowledge on GPOs. Refer to my previous tutorial on [Basic Active Directory Setup Activity](https://github.com/jeddrickpablico/ActiveDirectoryProjects/blob/main/DomainControllerInstallationAndSetup.md) and [Group Policy Management & Security Hardening Activity](https://github.com/jeddrickpablico/ActiveDirectoryProjects/blob/main/GPOProject.md)

---

## 📖 Phase 1: Core Concepts of File & Folder Sharing

In a Windows Server environment utilizing Active Directory (AD), file and folder sharing is the foundation of collaborative enterprise storage. Rather than storing files on isolated individual computers, organizations host data on centralized file servers. By leveraging Active Directory, administrators can use security groups (e.g., "HR-Department" or "IT-Admins") to efficiently manage who can view, modify, or delete specific data. This ensures that sensitive information remains secure while allowing employees seamless access to the resources they need to perform their jobs.

### 1.1 Permissions and Access Control
Permissions dictate exactly what a user or group can do with a file or folder once they have access to it. The standard permission levels include:
*   **Read:** Allows users to view files and folder contents.
*   **Write:** Allows users to create new files and modify existing content.
*   **Execute:** Allows users to run application files (like `.exe` or scripts).
*   **Full Control:** Grants complete power over the file or folder, including the ability to change permissions and take ownership.

These permissions are evaluated differently depending on how the user is accessing the data—either Locally (logged directly into the server hosting the files) or over the Network (accessing from a remote workstation).

### 1.2 Types of Permissions: NTFS vs. Share Permissions
When sharing a folder across a network, administrators must configure two distinct sets of permissions. Understanding the difference between these two is critical for securing a file server:

**NTFS Permissions**
These are the foundational security settings of the file system itself.
*   **Where it applies:** Applies to both local users (on the file system) and network users.
*   **Configuration:** Managed in the **Security tab** of a folder's properties.
*   **Scope:** Can be applied to the parent folder, individual subfolders, and even specific files.
*   **Granular Control:** Very detailed (Full Control, Modify, Read & Execute, etc.).


**Share Permissions**
These act as the "front door" to the folder when accessed over the network.
*   **Where it applies:** *Only* applies to users accessing the folder remotely via the network. If a user logs into the server locally, share permissions are bypassed entirely.
*   **Configuration:** Managed in the **Sharing tab** of a folder's properties.
*   **Scope:** Applies only to the shared folder level (no subfolder control).
*   **Granular Control:** Very basic (Full Control, Change, Read).

> 🛑 **The Key Rule of Permissions: NTFS + Share**
>
> When a user accesses a file over the network, both Share and NTFS permissions are evaluated together. The golden rule is that **NTFS and Share permissions combine, and the most restrictive applies.**
> 
> *Example:* If a user has "Full Control" via Share Permissions, but only "Read" via NTFS permissions, their effective access will be limited strictly to "Read".
>
> **Because of this rule, the modern enterprise best practice is to grant "Everyone - Full Control" on the Share tab, and then lock down all actual security and access control granularly using the NTFS Security tab.**
> 

### 1.3 Permission Inheritance
By default, permissions flow downwards. A child object (a subfolder) automatically **inherits** the permissions set on the parent folder by default.

*   **Explicit vs. Inherited:** **Explicit permissions** are those assigned directly to a specific file or folder. Explicit permissions always take priority over inherited ones.
*   **Disabling Inheritance:** If a specific subfolder (like an "Executive Payroll" folder inside an "HR" drive) needs completely different, stricter access levels than its parent, administrators can disable inheritance to break the chain and apply distinct explicit permissions.
*   **Enterprise Scaling and ABE:** Relying heavily on breaking inheritance and setting explicit permissions everywhere can become an administrative nightmare in large companies. Instead of relying purely on complex explicit permissions to hide data, large environments utilize Access-Based Enumeration (ABE). ABE dynamically hides folders from a user's view if they do not have the NTFS permissions to read them, ensuring a clean and secure network environment without overly complicating the folder permission structure.

### 1.4 Sharing Methods
Once a folder is shared and secured, users can access it via two primary methods using a **UNC (Universal Naming Convention)** path:
1.  **Network (Direct Access):** Users access the shared folder directly via a network path.
2.  **Mapped Drive:** For easier, everyday access, a shared network folder can be "mapped" to a specific drive letter on the user's computer (e.g., making the company share appear as the Z: drive alongside their local C: drive).

Regardless of the method used, both rely on a UNC (Universal Naming Convention) path to locate the resource, formatted as `\\ServerName\SharedFolderName`.

---
