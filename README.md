# ActiveDirectoryProjects

## 📝 Project Overview
This repository contains the documentation, configurations, and deployment strategies utilized during the implementation of my Windows Active Directory (AD) environment built within a personal virtualization homelab. The project serves as a hands-on environment to design, build, and secure enterprise-grade systems architecture, bridging the gap between theoretical network principles and practical deployment.

---

## 🛠️ Infrastructure & Tech Stack
* **Operating Systems:** Windows Server 2022 / Windows Server 2025 (Domain Controllers), Windows 10/11 Enterprise & Pro (Client Machines)
* **Virtualization Platform:** VMware Workstation
* **Core Network Services:** Active Directory Domain Services (AD DS), DNS, Group Policy Management

---

## 🚀 Implemented Features & Core Milestones

### 1. Domain Controller Installation, IAM, & Client Setup
**📖 [View the Full Step-by-Step Project Documentation Here](https://github.com/jeddrickpablico/ActiveDirectoryProjects/blob/main/DomainControllerInstallationAndSetup.md)**

* Configured a static IP environment and established Active Directory Domain Services (AD DS) for the root domain.
* Structured scalable Organizational Units (OUs) reflecting real-world corporate hierarchies (e.g., Administration, HR, IT, Finance).
* Set up Global Security and Distribution groups to govern Role-Based Access Control (RBAC) across the network.
* Provisioned domain user accounts and enforced baseline account security policies.
* Configured and joined a client virtual machine (Windows 10/11) to the Active Directory domain to validate DNS resolution, network connectivity, and secure remote authentication.

### 2. Group Policy Objects (GPOs) & Security Hardening
**📖 [View the Full Step-by-Step Project Documentation Here](https://github.com/jeddrickpablico/ActiveDirectoryProjects/blob/main/GPOProject.md)**

* Navigated the Group Policy Management Console (GPMC) and utilized the architectural differences between Computer vs. User configurations, as well as Policies vs. Preferences.
* Architected and deployed foundational security GPOs, enforcing password complexity standards, blocking external USB storage access, and restricting Control Panel availability to mitigate shadow IT.
* Configured automated user experience preferences, including network drive mapping and standardized corporate desktop wallpapers.
* Executed proper object management by relocating default computer objects into structured OUs for precise policy targeting.
* Validated deployments by forcing GPO updates (`gpupdate /force`) on domain-joined client endpoints to ensure active restriction enforcement.

---
*Note: This repository is actively updated as new security policies, logging architectures, and automation scripts are integrated into the domain.*
