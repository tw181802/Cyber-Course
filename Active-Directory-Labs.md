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

![IMG_1329](https://github.com/user-attachments/assets/af26181b-cfbc-4524-8ae6-fe4c4ff758d4)



## 2. Upload ISO to Virtual Machine

![IMG_1330](https://github.com/user-attachments/assets/b985151c-e975-433a-8ce6-49d222dd8955)
![IMG_1331](https://github.com/user-attachments/assets/ef324d40-05e9-4dce-a54d-d70e016256b5)


1. **Install VMware or VirtualBox**  
   - Install VMware or VirtualBox to set up a virtual machine for the Windows Server installation.
   - `https://www.virtualbox.org/wiki/Downloads`
   - `https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion`

2. **Upload ISO to VMware or VirtualBox**  
   - Open VMware or VirtualBox, create a new virtual machine, and select the downloaded ISO file as the installation media.

3. **Mount the ISO**  
   - Navigate to the VM's settings and find the option to mount an ISO. Select the downloaded ISO file.

4. **Install Windows Server**  
   - Start the virtual machine and begin the installation process by following the on-screen instructions.
   - Select **Yes** to continue, and leave the product key blank when prompted.
     
![IMG_1332](https://github.com/user-attachments/assets/ab751106-2dbe-47f1-9e64-e32ac830c03c)


## 3. Basic Setup and Installation

1. **Select Installation Type**  
   - Choose **Standard Evaluation** during the installation process.
     
![IMG_1334](https://github.com/user-attachments/assets/7100a0e6-8270-4ebb-9e8a-74cf5bd536b3)

2. **Disk Allocation**  
   - Select the disk size to allocate for the Windows Server installation.
   - Choose **New** if no disk is available.
   
![IMG_1335](https://github.com/user-attachments/assets/3dc8311d-b45d-4e9e-938e-cd4a8bc5dc29)
![IMG_1336](https://github.com/user-attachments/assets/9e7d4489-0b62-4f8e-b756-0cd23c1c1a9b)

3. **Create Administrator Account**  
   - Enter a username and password for the administrator account during setup.

![IMG_1337](https://github.com/user-attachments/assets/28532a40-fee8-4dfc-8d32-14e96cb67d20)

4. **Login Screen**  
   - After installation, you will be presented with the login screen. Log in with the administrator credentials you created.
![IMG_1339](https://github.com/user-attachments/assets/4c139eb8-4bca-450b-a269-c8b7001e6eda)


5. **Launch Server Manager and Promote to DC**  
   - Once logged in, type **Server Manager** in the search bar and open it to begin configuring your server.
   
![IMG_1340](https://github.com/user-attachments/assets/5707bd9a-e50d-4f94-bd7b-21081473ce8f)
![IMG_1284](https://github.com/user-attachments/assets/3a971ff7-781e-4d73-aa5f-4b0739d1fd12)

## 4. Adding Users and Computers in Active Directory

1. **Open Active Directory**  
   - In Server Manager, navigate to **Tools > Active Directory Users and Computers**.
![IMG_1264](https://github.com/user-attachments/assets/61f6d427-e61b-4d6c-bceb-e2643394a283)

2. **Create New User**  
   - Right-click on the desired Organizational Unit (OU) and select **New > User**.
   - Fill out the required user information and click **Next** to complete the user creation process.
![IMG_1265](https://github.com/user-attachments/assets/a91b7436-3f48-4ab7-bad8-36b30fb5e8b1)

3. **Edit User Properties**  
   - After the user is created, right-click the user and select **Properties** to edit their attributes as needed.
![IMG_1267](https://github.com/user-attachments/assets/da45da9b-4cce-40d8-a70d-02f8a2169777)
![IMG_1266](https://github.com/user-attachments/assets/365916ed-fdcc-4d68-b108-fde3aa67e666)

## 5. Installing Web Server Role

1. **Add Roles and Features**  
   - In **Server Manager**, go to **Manage > Add Roles and Features**.
![IMG_1251](https://github.com/user-attachments/assets/89392303-e857-4763-aeae-113d968a504f)



2. **Select Web Server Role**  
   - Follow the wizard and select **Web Server (IIS)** under **Roles**.
   - Continue through the wizard: **Next > Next > Next** until completion.

![IMG_1253](https://github.com/user-attachments/assets/368ce2db-ebe0-403f-bac2-4db7aedec5c7)
![IMG_1254](https://github.com/user-attachments/assets/ac280ae4-4ee2-44af-a91e-20e2d330489c)


## 6. Setting Up SCCM and Group Policy Management

1. **Install SCCM Tools**  
   - In **Server Manager**, go to **Tools > Group Policy Management**.
![IMG_1255](https://github.com/user-attachments/assets/f8543932-f0ec-48cc-8994-285ce1684dc1)


2. **Edit Default Domain Policy**  
   - Under **Group Policy Management**, expand the domain and right-click on **Default Domain Policy**.
   - Select **Edit** to configure policy settings for the domain.
![IMG_1256](https://github.com/user-attachments/assets/a80dd84d-b2e8-4453-bb23-72720d1c8f59)
![IMG_1257](https://github.com/user-attachments/assets/d73a8adb-1860-4080-82e0-2490587a6f90)

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

![IMG_1258](https://github.com/user-attachments/assets/88dea036-cff6-4eaf-95e6-036eb4bc89c6)
![IMG_1259](https://github.com/user-attachments/assets/ab0005ee-93c4-4229-926e-94cbf373d1d7)

![IMG_1260](https://github.com/user-attachments/assets/8da98cb1-f5d5-43b3-a0b3-ea214867f3ae)

![IMG_1261](https://github.com/user-attachments/assets/9cb94532-541b-41fc-a84e-79fae7f3483c)
![IMG_1262](https://github.com/user-attachments/assets/293666bf-83f1-404d-9530-e7b6e63d7b59)

## 12. Ticketing and Alerts (SOC)

1. **Snow Ticketing System**  
   - Use the Snow ticketing system to track IT issues and add resolution notes when problems are resolved.
  ![IMG_1318](https://github.com/user-attachments/assets/96151b23-e0f6-43dc-9ad4-2c52b1eefa05)

     ![IMG_1319](https://github.com/user-attachments/assets/0b3be4f3-44fa-4372-b586-29a558f835c0)


2. **Monitor Alerts in Sentinel**  
   - In Microsoft Sentinel, click on **Defender for Endpoint** under **Security.Microsoft.com** to view and investigate alerts.
![IMG_1303](https://github.com/user-attachments/assets/5d36a909-78e8-406d-8e49-96e97f1ee1dc)
![IMG_1304](https://github.com/user-attachments/assets/110c4ab2-d9b2-4a7d-bfab-0763e403dccb)

3. **File Hash and Virus Scanning**  
   - If a suspicious file is detected (e.g., WinRAR with a suspicious hash), run the file through **VirusTotal** to check for potential threats.
![IMG_1309](https://github.com/user-attachments/assets/6bf1dc45-931b-471b-92c7-d9749d68b2a7)
![IMG_1308](https://github.com/user-attachments/assets/0c395b2c-f541-4f44-a651-5e865377f58b)
![IMG_1307](https://github.com/user-attachments/assets/dd0918b0-b8e8-4805-9ba0-31ff60930df9)

4. **Behavioral Analysis and Investigation**  
   - Use the **Investigation Map** in Defender to analyze and trace suspicious behavior on the network.
![IMG_1311](https://github.com/user-attachments/assets/2153a0d0-2cc8-4ce1-85bf-b33a5968b403)


5. **Automate Incident Response**  
   - Use **Runbooks** or **Playbooks** in Azure to automate repetitive security tasks, such as isolating compromised devices.
![IMG_1316](https://github.com/user-attachments/assets/85f6cb96-f71b-487b-9a04-b98b2f191aa2)


## 13. Azure Active Directory (AD)

1. **Creating Users in Azure AD**  
   - Write scripts to automate user creation in **Azure Active Directory** (Azure AD) for seamless user management across cloud and on-premises resources.



![IMG_1272](https://github.com/user-attachments/assets/d6074113-f262-4d23-9697-75b20c1f281f)
![IMG_1271](https://github.com/user-attachments/assets/1cf97e20-7ae7-494b-8506-60f29394a76c)
![IMG_1270](https://github.com/user-attachments/assets/764fafeb-f732-4ebd-a653-a62c7a7c6c42)
![IMG_1269](https://github.com/user-attachments/assets/e5f63488-a377-4d2a-b9e0-abb13d6fe213)


