# 🛡️ Group Policy Management & Security Hardening Activity

## 🎯 Objectives
The primary objective of this project is to architect, configure, and secure the Active Directory environment using **Group Policy Objects (GPOs)**.

This activity covers the following deployment milestones based on our network setup:
* Installing and navigating the Group Policy Management Console (GPMC).
* Understanding the critical architectural differences between Computer vs. User configurations, and Policies vs. Preferences.
* Creating foundational GPOs (Password Policies, Drive Mapping, Desktop Wallpapers, Control Panel Restrictions, and USB Storage blocks).
* Moving computer objects within Active Directory Users and Computers (ADUC) and linking GPOs to target Organizational Units (OUs).
* Forcing policy updates on the client machine to test and verify domain restrictions.

---

## ⚙️ Prerequisites & Server Preparation
Ensure your Windows Server environment is running and the Active Directory Domain Services (AD DS) role is installed and promoted to a Domain Controller.

---

## 🛠️ Phase 1: Installing and Navigating Group Policy Management Console (GPMC)

The GPMC is the central tool used by administrators to manage all Group Policy settings and apply them to domain assets.

**1.1** If you have not already installed the GPMC, open **Server Manager**, navigate to **Manage > Add Roles and Features**.
<p>
  <img src="./images/GroupPolicyManagement/1.PNG" alt="Installing Group Policy Management via Server Manager" width="700">
</p>
<p><i>Figure 1.1: Verifying the installation of the GPMC feature.</i></p>

**1.2** Select all the default settings. Proceed to the **Features** tab. Ensure **Group Policy Management** is checked and complete the installation.
<p>
  <img src="./images/GroupPolicyManagement/2.PNG" alt="" width="700">
</p>
<p><i>Figure 1.2: </i></p>

**1.3** To launch the console, open the Start Menu, type **Group Policy Management**, and open the application. Alternatively, you can find it under **Windows Administrative Tools**.
<p>
  <img src="./images/GroupPolicyManagement/3.PNG" alt="Opening Group Policy Management Console" width="700">
</p>
<p><i>Figure 1.3</i></p>

