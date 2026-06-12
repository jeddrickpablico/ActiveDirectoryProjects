# Basic Active Directory Setup Activity

## 🎯 Objectives
The primary objective of this project is to architect and deploy a foundational Windows Active Directory (AD) domain from scratch. 

*Note: A proper DNS and DHCP infrastructure will not be implemented during this initial phase. These core network services will be manually configured in a future project module.*

This activity covers the following deployment milestones:
* Installing the Active Directory Domain Services (AD DS) role on Windows Server 2022.
* Promoting the standalone server to a Domain Controller (DC) to establish a new forest and root domain (e.g., `JeddrickPablico.local`).
* Architecting a logical hierarchy using Organizational Units (OUs) to represent distinct departments (e.g., IT, HR, Sales).
* Provisioning manual user accounts and assigning security groups within the directory structure.

---

## ⚙️ Prerequisites & Server Preparation
Before installing the AD DS role, the server environment must be properly staged. This implementation is executed on a Windows Server 2022 instance hosted within a VMware Workstation virtual machine. Ensure your VM is configured with a static IP address prior to beginning the installation.

---

## 🛠️ Phase 1: Installing Active Directory on Windows Server 2022

Installing the AD DS role places the necessary binaries and management tools onto your server. It is the first step before the server can actively manage network identities.

**1.1** To begin, launch the **Server Manager**. This is the central administrative console for Windows Server. You can find it by typing "Server Manager" into the Start menu search bar.

<p>
  <img src="./images/DomainControllerInstallationAndSetup/1.PNG" alt="Search Server Manager" width="700">
</p>
<p><i>Figure 1.1: Launching the Server Manager application.</i></p>

**1.2** Once the Server Manager dashboard loads, look to the top right corner. Click on **Manage**, and then select **Add Roles and Features** from the drop-down menu. 
<p>
  <img src="./images/DomainControllerInstallationAndSetup/2.PNG" alt="Click Manage then Add Roles and Features" width="700">
</p>
<p><i>Figure 1.2: Navigating to the Add Roles and Features Wizard.</i></p>

**1.3** The wizard's introductory screen (Figure 1.3) will appear. Click **Next** to proceed, leaving the default **Role-based or feature-based installation** option selected until you reach the **Server Roles** tab.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/3.PNG" alt="Click Next Leaving the Default Options Checked" width="700">
</p>
<p><i>Figure 1.3: Proceeding through the installation type and server selection.</i></p>

**1.4** In the Server Roles list, check the box for **Active Directory Domain Services**. This is the core service responsible for authenticating users, applying security policies, and storing network resource data.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/4.PNG" alt="Click Active Directory Domain Services" width="700">
</p>
<p><i>Figure 1.4: Selecting the AD DS role.</i></p>

**1.5** As soon as you select AD DS, a secondary window will prompt you to install required management tools (such as the Remote Server Administration Tools, or RSAT). Click **Add Features** to include these necessary components.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/5.PNG" alt="Click Add Features" width="700">
</p>
<p><i>Figure 1.5: Adding required AD DS administrative features.</i></p>

**1.6** While our primary focus is AD DS, we will also prepare the server for future networking labs. Check the box for **Remote Access** (used for VPN and routing capabilities). *Note: We will install the DNS and DHCP server roles in a separate, dedicated tutorial.* Click **Next**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/6.PNG" alt="Remote Access" width="700">
</p>
<p><i>Figure 1.6: Selecting the Remote Access role for future lab modules.</i></p>

**1.7** In the Features tab, ensure that **Group Policy Management** is checked. This crucial feature allows administrators to deploy security configurations and scripts across the entire domain. Click **Next**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/7.PNG" alt="Group Policy Management" width="700">
</p>
<p><i>Figure 1.7: Verifying Group Policy Management is selected.</i></p>

**1.8** Continue clicking **Next** through the informational screens. Once you arrive at the specific Role Services configuration for Remote Access, ensure the necessary checkboxes (such as DirectAccess and VPN) are selected, click **Add Features** if prompted again, and proceed.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/8.PNG" alt="Adding necessary features for Remote Access" width="700">
</p>
<p><i>Figure 1.8: Configuring Role Services for Remote Access.</i></p>

**1.9** Review your selections on the **Confirmation** screen and click **Install**. The installation process will take a few minutes to copy the binaries to your system. **Crucial Step:** Once the progress bar is full, DO NOT close the wizard. 
<p>
  <img src="./images/DomainControllerInstallationAndSetup/9.PNG" alt="Confirmation" width="700">
</p>
<p><i>Figure 1.9: Finalizing the role installation.</i></p>

---

## 🚀 Phase 2: Promoting the Server to a Domain Controller

Installing the AD DS role does not automatically make the server a Domain Controller. Promotion is the process that generates the Active Directory database (`NTDS.DIT`) and establishes the server's authority over the network.

**2.1** With the installation wizard still open, look for the alert link indicating that configuration is required. Click the hyperlink text that reads **Promote this server to a domain controller**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/10.PNG" alt="Promote this server to a domain controller" width="700">
</p>
<p><i>Figure 2.1: Initiating the Active Directory Domain Services Configuration Wizard.</i></p>

**2.2** In the Deployment Configuration window, select **Add a new forest**, as we are building this environment from scratch. Enter your desired root domain name (e.g., `JeddrickPablico.local`). 
* *Note:* Using a `.local` suffix is a standard best practice for isolated, private homelabs to prevent routing conflicts with live internet domains. Click **Next**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/11.PNG" alt="Adding a forest and entering your root domain name" width="700">
</p>
<p><i>Figure 2.2: Defining the new AD forest and root domain name.</i></p>

**2.3** Leave the functional levels at their default settings. You will be required to create a **Directory Services Restore Mode (DSRM)** password. Make sure this is a secure, memorable password. DSRM acts as an offline "Safe Mode" specifically for Active Directory, allowing an administrator to repair or recover a corrupted database. Click **Next**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/12.PNG" alt="Entering password for DSRM" width="700">
</p>
<p><i>Figure 2.3: Securing the directory with a DSRM password.</i></p>

**2.4** Active Directory is fundamentally dependent on DNS to function. However, because our lab objectives state that we will manually set up a standalone DNS Server in a future tutorial, leave the DNS delegation option **unchecked** for now and click **Next**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/13.PNG" alt="DNS Option Unchecked" width="700">
</p>
<p><i>Figure 2.4: Bypassing DNS delegation for future manual configuration.</i></p>

**2.5** The wizard will automatically generate a NetBIOS domain name (e.g., `JEDDRICKPABLICO`). This is a legacy, flat naming convention required to support older applications and operating systems. Leave it as the default and click **Next**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/14.PNG" alt="Default Option" width="700">
</p>
<p><i>Figure 2.5: Accepting the auto-generated NetBIOS name.</i></p>

**2.6** Proceed through the database path selections (leaving the default `C:\Windows\NTDS` locations) and review your choices. The wizard will execute a **Prerequisites Check** to ensure the server meets all technical requirements. Once you see the green checkmark indicating a successful pass, click **Install**. 

*The server will now promote itself, build the directory partitions, and automatically reboot to apply the new Domain Controller identity.*
<p>
  <img src="./images/DomainControllerInstallationAndSetup/15.PNG" alt="Prerequisite Check" width="700">
</p>
<p><i>Figure 2.6: Passing the prerequisite check and beginning the promotion.</i></p>

**2.7** Once the server has rebooted, you can see that at the login page to the left side of administor, you can see the domain name i.e. JEDDRICKPABLICO/administrator. Log in with your password
<p>
  <img src="./images/DomainControllerInstallationAndSetup/16.PNG" alt="Domain name beside administrator" width="700">
</p>
<p><i>Figure 2.7: Domain name beside administrator.</i></p>


**2.8** To check if Active Directory tools are installed, click the windows button and click Windows Administrative Tools. You can also tye "Windows Administrative Tools" in the search bar. Click **Active Directory Users and Computers**
<p>
  <img src="./images/DomainControllerInstallationAndSetup/17.PNG" alt="Verifying Successful Installation of Active Directory Tools" width="700">
</p>
<p><i>Figure 2.7: Verifying Successful Installation of Active Directory Tools.</i></p>

## Phase 3: Architecting a logical hierarchy using Organizational Units (OUs) to represent distinct departments (e.g., IT, HR, Sales).
