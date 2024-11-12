# What is Active Directory (AD)?

Active Directory (AD) is a system created by Microsoft to manage networks in a Windows environment. It keeps track of important information about objects like computers, users, and printers, similar to how a phone book stores contact details. When users log in or access resources, AD verifies their identity using a process called **Kerberos**. Non-Windows devices, such as Linux computers or network devices like firewalls, can also connect to Active Directory through methods like **RADIUS** or **LDAP**.

## AD DS Data Store

The **Active Directory Domain Services (AD DS)** data store is a special database that holds all the directory information about users, services, and applications in a network. It’s stored in a file called `Ntds.dit` and by default, it is located in the `%SystemRoot%\NTDS` folder on domain controllers. Only domain controller systems can access and manage this data.

## Domains

Domains are used to organize and manage objects (like users and computers) in a network. A **domain**:

- Acts as an administrative boundary, meaning you can apply rules and policies to all objects within the domain.
- Is a replication boundary, meaning data between domain controllers is synchronized within the domain.
- Controls access, ensuring only authorized users can access certain resources.

## Trees

A **domain tree** is a collection of domains connected in a hierarchy. In a domain tree:

- All domains share a naming structure with the parent domain.
- A parent domain can have several child domains.
- Domains automatically trust each other for easier management of resources.

## Forests

A **forest** is a larger structure that can contain multiple domain trees. A forest:

- Shares the same technical setup, like the schema (blueprints for the directory) and configuration.
- Has a global catalog, which helps in searching for information across the entire forest.
- Connects all domains within the forest with trust relationships.
- Includes special admin groups like **Enterprise Admins** and **Schema Admins**.

## Organizational Units (OUs)

**Organizational Units (OUs)** are containers inside Active Directory that can hold users, groups, computers, and other OUs. They are used to:

- Organize your network in a logical, hierarchical way, reflecting your company's structure.
- Simplify the management of objects by grouping them together.
- Assign administrative tasks and apply policies to these groups.

## Types of Objects in Active Directory

- **User**: Represents a person or entity that needs access to the network resources.
- **InetOrgPerson**: Similar to a user, but designed for compatibility with other directory systems.
- **Contact**: Primarily used for storing external email addresses (doesn't grant network access).
- **Group**: Helps manage user permissions and access in bulk, making administration easier.
- **Computer**: Represents a computer on the network, allowing it to be authenticated and tracked for resource access.
- **Printer**: Stores information about printers, making it easier for users to find and connect to them.
- **Shared Folder**: Used for managing shared files and folders, making them searchable based on specific properties.

## Domain Controllers

A **domain controller** is a server that manages and controls access to a network. It runs Active Directory and is set up to handle domain tasks. Domain controllers:

- Store the network's important data (like user accounts and computer information).
- Check usernames and passwords to grant access to the network.
- Share updates with other domain controllers to keep everything up to date.
- Allow admins to manage user accounts and network # Windows Server Setup and Configuration Guide

This guide outlines the steps to set up Windows Server on VMware, configure Active Directory, DHCP, SCCM, and troubleshoot common IT issues.

## 1. Download Windows Server ISO

1. **Find Windows Server ISO File**  
   - Go to the official Microsoft website or trusted source to download the Windows Server ISO file.

## 2. Upload ISO to Virtual Machine

1. **Install VMware or VirtualBox**  
   - Install VMware or VirtualBox to set up a virtual machine for the Windows Server installation.

2. **Upload ISO to VMware or VirtualBox**  
   - Open VMware or VirtualBox, create a new virtual machine, and select the downloaded ISO file as the installation media.

3. **Mount the ISO**  
   - Navigate to the VM's settings and find the option to mount an ISO. Select the downloaded ISO file.

4. **Install Windows Server**  
   - Start the virtual machine and begin the installation process by following the on-screen instructions.
   - Select **Yes** to continue, and leave the product key blank when prompted.

## 3. Basic Setup and Installation

1. **Select Installation Type**  
   - Choose **Standard Evaluation** during the installation process.

2. **Disk Allocation**  
   - Select the disk size to allocate for the Windows Server installation.
   - Choose **New** if no disk is available.

3. **Create Administrator Account**  
   - Enter a username and password for the administrator account during setup.

4. **Login Screen**  
   - After installation, you will be presented with the login screen. Log in with the administrator credentials you created.

5. **Launch Server Manager**  
   - Once logged in, type **Server Manager** in the search bar and open it to begin configuring your server.

## 4. Adding Users and Computers in Active Directory

1. **Open Active Directory**  
   - In Server Manager, navigate to **Tools > Active Directory Users and Computers**.

2. **Create New User**  
   - Right-click on the desired Organizational Unit (OU) and select **New > User**.
   - Fill out the required user information and click **Next** to complete the user creation process.

3. **Edit User Properties**  
   - After the user is created, right-click the user and select **Properties** to edit their attributes as needed.

## 5. Installing Web Server Role

1. **Add Roles and Features**  
   - In **Server Manager**, go to **Manage > Add Roles and Features**.

2. **Select Web Server Role**  
   - Follow the wizard and select **Web Server (IIS)** under **Roles**.
   - Continue through the wizard: **Next > Next > Next** until completion.

## 6. Setting Up SCCM and Group Policy Management

1. **Install SCCM Tools**  
   - In **Server Manager**, go to **Tools > Group Policy Management**.

2. **Edit Default Domain Policy**  
   - Under **Group Policy Management**, expand the domain and right-click on **Default Domain Policy**.
   - Select **Edit** to configure policy settings for the domain.

3. **Software Settings**  
   - Navigate to **Software Settings** under the policy editor to configure software deployment settings.

## 7. Configuring DHCP

1. **Set IP Address Range for DHCP**  
   - Configure the DHCP server with an IP range, for example:  
     - **Range**: 192.168.1.100 - 200  
     - **Exclusions**: 192.168.1.105 - 110  
     - **Reservations**:  
       - 192.168.1.10 reserved for MAC address `1F-B8-DD-92-5A-5F`
   
2. **Add DHCP Reservations**  
   - Go to **Scope > Add Reservation**, and select both DHCP and BOOTP, entering both IP and MAC addresses.

3. **Private IP Addresses**  
   - DHCP can also assign private IP addresses like **169.254.X.X** for internal use.

## 8. Configuring DNS and Hosts File

1. **Update Mail Hosts File for DNS**  
   - Update the mail server records in the `hosts` file to ensure proper DNS resolution for email services.

## 9. Monitoring Server Logs in Event Viewer

1. **View Server Logs**  
   - Open **Event Viewer** to view application, security, and system logs.
   - Use filters to analyze specific logs, especially **Security Logs** for auditing purposes.

2. **Filtering in Azure**  
   - Use Azure to filter and view specific logs and events related to network security or server performance.

## 10. Common IT Help Desk Issues

1. **Troubleshoot Account Issues**  
   - **Account Locked**: Unlock accounts through Active Directory.
   - **Password Expired**: Reset passwords for users as needed.
   - **Two-Factor Authentication (2FA)**: Address issues related to Duo, RSA, or Google Authenticator.

2. **Wi-Fi Issues**  
   - Ensure the **Von profile** is correctly set up on the C drive.
   - Check for any missing **Von certificates**.

3. **Unlock Account**  
   - Use the **Active Directory Users and Computers** console to unlock a user account.

4. **Promote to Domain Controller (DC)**  
   - If the server needs to become a Domain Controller, follow the steps to promote it in **Server Manager**.

## 11. Network Security Groups (NSG)

1. **Review Network Security Groups**  
   - In Azure, check **Inbound** and **Outbound** rules for security group configurations.

2. **Configure Static IP Addresses**  
   - For network settings, right-click **Network Adapter**, select **Properties**, and configure static IP addresses through **IPv4 Properties**.

## 12. Ticketing and Alerts (SOC)

1. **Snow Ticketing System**  
   - Use the Snow ticketing system to track IT issues and add resolution notes when problems are resolved.

2. **Monitor Alerts in Sentinel**  
   - In Microsoft Sentinel, click on **Defender for Endpoint** under **Security.Microsoft.com** to view and investigate alerts.

3. **File Hash and Virus Scanning**  
   - If a suspicious file is detected (e.g., WinRAR with a suspicious hash), run the file through **VirusTotal** to check for potential threats.

4. **Behavioral Analysis and Investigation**  
   - Use the **Investigation Map** in Defender to analyze and trace suspicious behavior on the network.

5. **Automate Incident Response**  
   - Use **Runbooks** or **Playbooks** in Azure to automate repetitive security tasks, such as isolating compromised devices.

## 13. Azure Active Directory (AD)

1. **Creating Users in Azure AD**  
   - Write scripts to automate user creation in **Azure Active Directory** (Azure AD) for seamless user management across cloud and on-premises resources.





