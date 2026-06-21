# ActiveDirectoryProjects

## 📝 Project Overview
This repository contains the documentation, configurations, and deployment strategies utilized during the implementation of my Windows Active Directory (AD) environment built within a personal virtualization homelab. The project serves as a hands-on environment to design, build, and secure enterprise-grade systems architecture, bridging the gap between theoretical network principles and practical deployment.

---

## 🛠️ Infrastructure & Tech Stack
* **Operating Systems:** Windows Server 2022 / Windows Server 2025 (Domain Controllers), Windows 10/11 Pro (Client Machines)
* **Virtualization Platform:** VMware
* **Core Network Services:** Active Directory Domain Services (AD DS), DNS

---

## 🚀 Implemented Features & Core Milestones

### 1. Domain Controller Installation, IAM, & Client Setup
**📖 [View the Full Step-by-Step Project Documentation Here](https://github.com/jeddrickpablico/ActiveDirectoryProjects/blob/main/DomainControllerInstallationAndSetup.md)**

* Configured a static IP environment and established Active Directory Domain Services (AD DS) for the root domain.
* Structured scalable Organizational Units (OUs) reflecting real-world corporate hierarchies (e.g., Administration, HR, IT, Finance).
* Set up Global Security and Distribution groups to govern Role-Based Access Control (RBAC) across the network.
* Provisioned domain user accounts and enforced baseline account security policies.
* Configured and joined a client virtual machine (Windows 10/11 Pro) to the Active Directory domain to validate DNS resolution, network connectivity, and secure remote authentication.

### 2. Group Policy Objects (GPOs) & Security Hardening *(Upcoming Project)*
* *Note: This phase of the project is currently in development and will be published next.*
* **Planned implementations include:**
  * Baseline corporate security GPOs, including restricted Control Panel access and automated screen-lock timeouts.
  * Specialized drive mapping and folder redirection policies targeting designated OUs.
  * Software distribution paths to push automated deployments natively across client machines.

---
*Note: This repository is actively updated as new security policies, logging architectures, and automation scripts are integrated into the domain.*
