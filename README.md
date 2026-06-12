# ActiveDirectoryProjects

## 📝 Project Overview
This repository contains the documentation, configurations, and deployment strategies utilized during the implementation of my Windows Active Directory (AD) environment built within a personal virtualization homelab. The project serves as a hands-on environment to design, build, and secure enterprise-grade systems architecture, bridging the gap between theoretical network principles and practical deployment.

---

## 🛠️ Infrastructure & Tech Stack
* **Operating Systems:** Windows Server 2022 / Windows Server 2025 (Domain Controllers), Windows 10/11 Pro (Client Machines)
* **Virtualization Platform:** VMware
* **Core Network Services:** Active Directory Domain Services (AD DS), DNS *(To be implemented)*, DHCP *(To be implemented)*

---

## 🚀 Implemented Features & Core Milestones

### 1. Domain Controller Installation & Network Architecture
* Designed and deployed a dedicated private network space for isolated lab security.
* Configured a static IP environment and established Active Directory Domain Services (AD DS) root domains. *(To be implemented)*

### 2. Identity and Access Management (IAM)
* Structured scalable Organizational Units (OUs) reflecting real-world corporate hierarchies (e.g., Administration, HR, IT, Finance).
* Set up Global and Universal security groups to govern Role-Based Access Control (RBAC) across shared resources.

### 3. Group Policy Objects (GPOs) & Security Hardening
* Implemented baseline corporate security GPOs, including restricted Control Panel access and automated screen-lock timeouts.
* Configured specialized drive mapping and folder redirection policies targeting designated OUs.
* Managed software distribution paths to push automated deployments natively across client machines.

---
*Note: This repository is actively updated as new security policies, logging architectures, and automation scripts are integrated into the domain.*
