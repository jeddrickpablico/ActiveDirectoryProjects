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

**2.7** Once the server has rebooted, you will notice that the login screen now displays your domain name prefixing the administrator account (e.g., `JEDDRICKPABLICO\Administrator`). Log in using your administrator password to access the newly established domain environment.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/16.PNG" alt="Verifying the domain identity at the Windows Server login screen" width="700">
</p>
<p><i>Figure 2.7: Verifying the domain identity at the Windows Server login screen.</i></p>

**2.8** To verify that the Active Directory management utilities are successfully installed, open the Start menu and navigate to **Windows Administrative Tools** (or search for it directly in the taskbar). From the list of tools, launch **Active Directory Users and Computers (ADUC)**. This console will be the primary interface for managing network objects.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/17.PNG" alt="Launching Active Directory Users and Computers from Administrative Tools" width="700">
</p>
<p><i>Figure 2.8: Launching Active Directory Users and Computers from Administrative Tools.</i></p>

---

## 📁 Phase 3: Architecting a Logical Hierarchy using Organizational Units (OUs)

Before creating user accounts, it is crucial to establish a logical directory structure. Active Directory utilizes **Organizational Units (OUs)** to achieve this. An OU acts as a container—much like a standard file folder—that holds various network objects such as users, computers, servers, and groups. 

Structuring OUs correctly is a foundational security practice. It allows administrators to easily apply Group Policy Objects (GPOs) and cleanly delegate administrative permissions to specific segments of the company without granting blanket domain access.

### 3.1 Establishing Top-Level and Nested OUs
A standard enterprise best practice is to structure the directory geographically, followed by object categories. 

**3.1.1 Top-Level OUs (Geography):** To create your first container, right-click your domain name in ADUC, hover over **New**, and select **Organizational Unit**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/18.PNG" alt="Creating Top-Level OU" width="700">
</p>
<p><i>Figure 3.1.1: Initiating the creation of a Top-Level OU.</i></p>

**3.1.2** In the New Object dialog box, type `USA` for the name and click **OK**. *(Note: Keep the "Protect container from accidental deletion" box checked as a safety measure).*
<p>
  <img src="./images/DomainControllerInstallationAndSetup/19.PNG" alt="Creating Top-Level OU (USA)" width="700">
</p>
<p><i>Figure 3.1.2: Naming the USA Top-Level OU.</i></p>

**3.1.3** Repeat this exact process to establish containers for your other primary regions, such as `Europe` and `Asia`.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/20.PNG" alt="Create Top-Level OU (Europe and Asia)" width="700">
</p>
<p><i>Figure 3.1.3: Completed geographic top-level directory structure.</i></p>

**3.1.4 Nested OUs (Object Types):** Grouping all objects directly inside a geographic OU becomes unmanageable at scale. Instead, inside the `USA` OU, create nested sub-OUs to categorize the assets. Typical nested OUs include:
   * **Computers:** For standard employee workstations.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/21.PNG" alt="Nested OU in USA (Computer)" width="700">
</p>
<p><i>Figure 3.1.4.a: Creating a nested "Computers" OU inside the USA container.</i></p>

   * **Servers:** For infrastructure assets.
   * **Users:** For employee accounts.
   
Repeat this internal nesting structure for the remaining geographic OUs to maintain a uniform architecture across the domain.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/22.PNG" alt="Nested OUs" width="700">
</p>
<p><i>Figure 3.1.4.b: Fully deployed nested OU architecture across all regions.</i></p>

---

### 3.2 Understanding Group Scopes and Types
Once the OU structure is built, we create **Groups** within the departmental `Users` OUs to organize employees. When creating a new Group, Active Directory requires you to define its **Scope** and **Type**.

**Group Scopes (Where the group is applied):**
* **Domain Local:** Used to assign permissions directly to local domain resources (like a specific shared folder or printer). 
* **Global:** Used to group users based on their department or role (e.g., grouping IT staff together). Global groups are then placed inside Domain Local groups to grant them access. This is the most common scope for departmental grouping.
* **Universal:** Used in complex, enterprise-level environments spanning multiple domains, allowing users from one domain to access resources located in an entirely different domain.

<p>
  <img src="./images/DomainControllerInstallationAndSetup/GroupScopeGraphic.png" alt="Group Scope Graphic" width="700">
</p>
<p><i>Figure 3.2.a: Active Directory Group Scopes.</i></p>

**Group Types (What the group does):**
* **Security Groups:** Used to assign permissions and user rights to shared network resources. 
  * *Example:* Giving a "Finance" Security Group read/write access to financial folders, or utilizing Built-in Security Groups (like *Domain Admins* or *Remote Desktop Users*) to grant broad administrative control.
    
<p>
  <img src="./images/DomainControllerInstallationAndSetup/SecurityGroupsGraphic.png" alt="Security Group Graphic" width="700">
</p>
<p><i>Figure 3.2.b: Active Directory Security Groups.</i></p>

* **Distribution Groups:** Used exclusively for email distribution lists. These groups do *not* possess Security Identifiers (SIDs) and cannot grant network access permissions.
  * *Example:* Creating a `DL-IT Admins` or `All Employees` Distribution Group so an Exchange server can route mass communications to specific collections of people.

<p>
  <img src="./images/DomainControllerInstallationAndSetup/DistributionGroupGraphic.png" alt="Distribution Group Graphic" width="700">
</p>
<p><i>Figure 3.2.c: Active Directory Distribution Groups.</i></p>

#### Creating the Groups

**3.2.1** To create a new group, right-click on your designated `Users` OU, hover over **New**, and click on **Group**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/23.PNG" alt="Creating a Group in Users OU" width="700">
</p>
<p><i>Figure 3.2.1: Initiating Group creation within the Users OU.</i></p>

**3.2.2** In the dialog box, type `IT` (or your desired department) as the **Group name**. Ensure the Group scope is set to **Global** and the Group type is set to **Security**, then click **OK**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/24.PNG" alt="Creating an IT Group in Users OU" width="700">
</p>
<p><i>Figure 3.2.2: Naming the IT Security Group.</i></p>

**3.2.3** To create an email mailing list, initiate the same group creation process, but change the **Group type** to **Distribution**. 
<p>
  <img src="./images/DomainControllerInstallationAndSetup/25.PNG" alt="Creating Distribution List for IT Staff" width="700">
</p>
<p><i>Figure 3.2.3: Creating a Distribution List for IT Staff communications.</i></p>

--- 


## 👥 Phase 4: Provisioning User Accounts and Assigning Security Groups

With the directory architecture and security groups securely in place, user accounts can now be provisioned. 

*Note: In Active Directory, it is a strict best practice to utilize **Role-Based Access Control (RBAC)**. This means you should never assign resource permissions directly to a single user. Instead, you assign users to Groups, and give permissions to those Groups. This makes offboarding, onboarding, and auditing infinitely easier.* 

*(Note on Automation: In modern enterprise environments, manual user creation is rarely done. Bulk user provisioning is typically automated using **PowerShell scripts** that pull data directly from HR databases to ensure accuracy and save time. However, for the sake of simplicity in this foundational lab, we will be creating users manually. Automated PowerShell scripting will be covered in future tutorials.)*

**4.1 Creating the User Object:** Navigate to the specific departmental or regional `Users` OU where the employee belongs. Right-click the empty space, select **New**, and choose **User**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/26.PNG" alt="Creating a new user account" width="700">
</p>
<p><i>Figure 4.1: Initiating manual user creation within a designated OU.</i></p>

**4.2 Defining Credentials:** Fill in the required user identity parameters (First Name, Last Name). For the **User logon name** (the UPN prefix), utilize a standard corporate naming convention, such as `first.last` or `firstinitial+lastname` (e.g., `john.doe`). Click **Next**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/27.PNG" alt="Defining user credentials and logon name" width="700">
</p>
<p><i>Figure 4.2: Establishing the user's primary logon identity.</i></p>

**4.3 Securing the Account:** Assign a temporary complex password. Ensure the **"User must change password at next logon"** checkbox is selected. This is a critical security mandate that prevents the IT administrator from knowing the user's permanent password. Click **Next** and then **Finish**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/28.PNG" alt="Configuring initial password policies" width="700">
</p>
<p><i>Figure 4.3: Enforcing initial account security policies.</i></p>

**4.4 Assigning Group Membership:** The user account now exists, but the user currently lacks access to departmental resources. To fix this, right-click the newly created user profile and select **Add to a group...**.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/29.PNG" alt="Selecting Add to a group" width="700">
</p>
<p><i>Figure 4.4: Opening the group assignment context menu.</i></p>

**4.5 Finalizing Access:** In the object selection box, type the name of the departmental Security or Distribution group you created in Phase 3 (e.g., `IT`). Click **Check Names** to validate the group (the name will become underlined), then click **OK** to successfully grant the user their required network permissions.
<p>
  <img src="./images/DomainControllerInstallationAndSetup/30.PNG" alt="Validating and assigning group membership" width="700">
</p>
<p><i>Figure 4.5: Resolving the group name and finalizing user permissions.</i></p>
