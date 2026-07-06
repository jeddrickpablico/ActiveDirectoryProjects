# 📁 Windows File Services & Permission Management Project

## 🎯 Objectives
The primary objective of this project is to provision, secure, and manage centralized network storage using **Windows File Services**, strict **NTFS/Share Permissions**, and **File Server Resource Manager (FSRM)**.

This activity covers the following deployment milestones based on our network setup:
* Establishing foundational network shares and deploying them to client machines.
* Installing and configuring FSRM to implement storage Quotas and File Screening to restrict unauthorized media.
* Understanding and applying the critical architectural differences between NTFS and Shared permissions.
* Managing advanced permission inheritance to secure confidential departmental data.
* Enabling Access-Based Enumeration (ABE) to securely hide restricted resources from unauthorized users.

---

## ⚙️ Prerequisites & Server Preparation
Ensure your Windows Server environment is running and promoted to a Domain Controller. You must have client endpoints connected to the domain and pre-configured user accounts belonging to specific departmental Security Groups and knowledge on GPOs. Refer to my previous tutorial on [Basic Active Directory Setup Activity](https://github.com/jeddrickpablico/ActiveDirectoryProjects/blob/main/DomainControllerInstallationAndSetup.md) and [Group Policy Management & Security Hardening Activity](https://github.com/jeddrickpablico/ActiveDirectoryProjects/blob/main/GPOProject.md)

---

## 🛠️ Phase 1: File Server Provisioning & Resource Management
